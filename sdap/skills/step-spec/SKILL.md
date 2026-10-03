---
name: step-spec
description: S4 (domain-scoped). Turn this domain's functions into a formal, measurable spec.
---
# S4 - Spec
Input: the functions allocated to THIS domain + the interface list.
Do: write inputs, outputs, guarantees, and numeric acceptance criteria. Apply `profile-<domain>`.
Output: `spec/specs/<domain>/*.md`.
Gate passes when: no vague word ("fast","reliable") appears without a number, and every
criterion can be turned into a test. This is what makes "proven" mean something at S8.
