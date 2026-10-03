---
name: step-decompose
description: S2. Break the requirements into functions the system must perform, still domain-neutral.
---
# S2 - Decompose
Input: `spec/requirements-vN.md`.
Do: list the functions the system must perform. Do NOT yet say software/hardware/mechanical.
Output: `spec/functions.md` (each function gets an id, traced back to a req id).
Gate passes when: every requirement maps to >=1 function, no function is orphaned, and no domain word has crept in.
