---
name: step-build
description: S7 (domain-scoped). Produce this domain's REAL, runnable artifact under its profile — no fakery.
---
# S7 - Build
Input: this domain's frozen spec.
Do: generate the artifact (code / board / CAD) under `profile-<domain>`; one checkpoint per module.
Output: `artifacts/<domain>/...`.

Build for real — no fakery. What you claim is built MUST actually work:
- Persist state to disk (file/DB); never ship in-memory-only where the spec implies persistence.
- Load external config/content from its source files at runtime; do NOT hardcode data that belongs in a config/niche/source.
- Implement real security (hash + verify auth) where the spec asks; never leave auth mocked/skipped.
- If a part is genuinely out of scope, mark it NOT built and rollback — never present a stub, mock, or placeholder as done.

Gate passes when: the artifact builds and clears the profile's build checks
(SW: compile+lint+types; HW: routing+DRC; ME: CAD+manufacturability). A mock/stub passed off as complete = rollback, not a build.
