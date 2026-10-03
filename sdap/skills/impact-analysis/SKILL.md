---
name: impact-analysis
description: Given a changed requirement, walks the traceability matrix and marks the minimal set of dirty nodes so only affected work re-runs. The engine of the change loop and of token economy.
---
# Impact analysis
Input: the new requirements version + `state/traceability.json`.
1. Find which req ids changed or were added.
2. Follow links req -> function -> domain -> spec -> artifact -> test. Every node on a
   touched chain becomes `dirty`.
3. ALWAYS mark the owning S5 and S6 dirty if any spec changed - a new requirement can
   break an old interface even when its own chain looks isolated.
4. Everything off the touched chains stays `proven` -> orchestrator marks it `cached` and skips.
5. Write the dirty set to `state/nodes.json`; output "N dirty of M total".
Principle: mark the minimum actually affected. Over-mark and you burn tokens; under-mark and you ship an inconsistency.
