---
name: step-seal
description: S9. Snapshot the proven state as a baseline and write the audit record.
---
# S9 - Seal
Input: all proven artifacts + the run log.
Do: snapshot the agreed state as `state/baseline-vN.json`; record what was done, by which
agent, with which tools, and which gates passed.
Output: `state/baseline-vN.json` + audit entries in `state/run-log.jsonl`.
Gate passes when: the record is written. L2+: human sign-off. L3: cryptographic notarization.
