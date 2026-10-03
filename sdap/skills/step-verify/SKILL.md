---
name: step-verify
description: S8 (domain-scoped). Prove the artifact meets its S4 criteria by ACTUALLY RUNNING the tests; on change, run regression.
---
# S8 - Verify
Input: the artifact + its S4 acceptance criteria.
Do: derive tests from S4, then **actually execute them** with a real shell command (e.g. `node test.js`,
`npm test`, `pytest`) and capture the real stdout + exit code. On a change, also re-run untouched modules (regression).
Output: a test report that quotes the **real command and its real output** (actual pass/fail counts).
Gate passes when: the tests were really executed AND all S4-derived tests pass (real green); on a change,
regression on untouched nodes also passes.
NEVER simulate, assume, or self-report results. A report without real execution output = automatic `rollback`.
If the harness itself can't run (port clash, missing dep, server-start race), that is a `rollback` to fix the
harness — not a pass.
Tests MUST be idempotent: they reset their own data/state at startup and stay green on two consecutive runs; a suite that passes only against a clean checkout (red on leftover state) = `rollback`.
This is the moment "proven" is earned.
