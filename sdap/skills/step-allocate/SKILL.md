---
name: step-allocate
description: S3. Assign each function to a domain (SW/HW/ME) and record the interfaces between domains. Sets which domains are live.
---
# S3 - Allocate
Input: `spec/functions.md`.
Do: assign each function to exactly one domain; describe every cross-domain interface
(signal levels, currents, dimensions, timing, thermal). Set `live` domains and append
the per-domain S4-S8 nodes (+ S6, S9) into `state/nodes.json`. Update `state/traceability.json`.
Output: `spec/allocation.md` + updated state.
Gate passes when: every function has one owning domain and every interface is described.
L2+: requires human approval - the cheapest/lightest/most-reliable split is judgment, not fact.
