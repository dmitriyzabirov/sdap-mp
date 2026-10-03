---
description: Add or change a requirement and re-run only the affected (dirty) parts.
---

A new or changed requirement: $ARGUMENTS

1. Run `step-intake` to fold it into a new `spec/requirements-vN.md` version.
2. Run `impact-analysis`: walk `state/traceability.json`, mark every affected node
   `dirty` in `state/nodes.json`. Leave everything else `proven` (it stays cached).
3. Hand control to the `orchestrator`: it recomputes only dirty nodes, and re-runs
   S5/S6 against ALL existing specs — a new requirement can conflict with old ones.
4. Re-seal (S9) into a new baseline version with the delta logged.

Do not recompute anything that impact-analysis did not mark dirty.
