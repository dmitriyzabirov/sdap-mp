---
name: step-intake
description: S1. Normalize the customer's raw requirements into a clean, versioned requirements document and surface every ambiguity.
---
# S1 - Intake
Input: raw customer requirements (prose).
Do: clean and structure it; assign a version; list open questions and any assumptions you had to make.
Output: `spec/requirements-vN.md` + `spec/open-questions.md`.
Gate passes when: every critical ambiguity is either resolved or written down as an explicit, labeled assumption. No silent guesses.
