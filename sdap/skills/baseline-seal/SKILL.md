---
name: baseline-seal
description: Helper for S9 - writes the baseline snapshot and the delta against the previous baseline.
---
# Baseline seal
Write `state/baseline-vN.json`: level, requirements version, per-node status+hash,
and the delta vs baseline-v(N-1). Append the audit summary to `state/run-log.jsonl`.
