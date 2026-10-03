---
name: step-deconflict
description: S5 (domain-scoped). Check that this domain's own modules are mutually consistent.
---
# S5 - Deconflict (within domain)
Input: this domain's specs.
Do: check internal contracts - no module expecting what another never provides, no cycles.
Output: annotations on the domain specs; a short consistency note.
Gate passes when: internal contracts line up; no cycles or contradictions inside the domain.
