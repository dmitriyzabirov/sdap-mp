---
name: traceability-update
description: Keeps state/traceability.json current - the req -> function -> domain -> spec -> artifact -> test links that impact-analysis and cache-check rely on.
---
# Traceability update
After any step that creates or changes a node, add/update its link row so the chain
req -> function -> domain -> spec -> artifact -> test stays complete. A missing link
makes impact-analysis guess - which breaks economy.
