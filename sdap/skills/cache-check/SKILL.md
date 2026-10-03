---
name: cache-check
description: Decides whether a node can be skipped because its inputs are unchanged and it is already proven. Enforces idempotency / token economy.
---
# Cache check
Input: a node + the hashes of its input subtree.
- If status is `proven` AND the input hash matches the stored hash -> return `cached` (skip).
- Otherwise -> return `recompute`.
Never recompute proven work whose inputs did not move.
