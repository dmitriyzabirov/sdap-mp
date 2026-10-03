# Spec-driven agentic pipeline — runnable skeleton

A multi-domain (software / hardware / mechanical) build run as a state machine.
Steps S1–S9, each behind a gate (`pass` / `rollback` / `escalate`), with cheap-first
model routing that climbs only on failure.

## How to run
1. Drop this folder into a Claude Code project (it reads `CLAUDE.md` and `.claude/` automatically).
2. Put your real requirements in `spec/requirements-v1.md` (an example is there now).
3. Start the run:  `use the orchestrator to run the pipeline`
4. Change a requirement later:  `/change "telemetry must update every 100 ms"`

## What's here
- `CLAUDE.md` — the rules: the LEVEL knob, model ladders, the three economy rules, domain skipping.
- `config/models.json` — the model routing table (ladders, level ceilings, escalation policy).
- `.claude/agents/` — `orchestrator` (pinned to sonnet) + four tier-pinned workers (haiku/sonnet/opus/fable).
- `.claude/skills/step-*` — one skill per step S1–S9 (transform + "gate passes when…").
- `.claude/skills/profile-{sw,hw,me}` — per-domain build/verify/seal checks.
- `.claude/skills/{gate-run,impact-analysis,cache-check,baseline-seal,traceability-update}` — the machinery.
- `.claude/commands/change.md` — the `/change` loop.
- `state/` — `nodes.json` (status + rung per node), `traceability.json`, `run-log.jsonl`, `escalations.md`.

## The two ideas to keep in mind
**Cheap first, strong only when needed.** Every step starts on the cheapest model in
its ladder. A `rollback` bumps it one tier; only when the top tier (capped by LEVEL) also
fails does it escalate to you. The orchestrator never leaves the cheapest model.

**Recompute only what's dirty.** A change re-runs the minimal affected subtree via
`impact-analysis`; everything else stays `cached`. That, plus per-step dirty-subtree-only
context, is the whole token-economy story.

## The LEVEL knob (in `state/nodes.json`)
- **L1** — smoke tests, one path, model ceiling = sonnet. Start here.
- **L2** — full deconflict + tests, human signs off S3 and S9, ceiling = opus.
- **L3** — strict coverage, human at every gate, cryptographic seal, ceiling = fable.

Same steps at all three; only gate rigor and the model ceiling move.

## Notes
- Worker model strings in the agent frontmatter (`claude-haiku-4-5`, etc.) may need
  adjusting to whatever your Claude Code build accepts; the ladder logic is in `config/models.json`.
- `fable` sits above `opus` only at L3; if your account can't route it, L3's ceiling
  falls back to `opus` — change one line in `config/models.json`.

## License
Apache License 2.0 (see `LICENSE`). Copies and derivative works must keep the copyright notice, the license text and the `NOTICE` file, and mark changed files. Copyright 2026 Dmitrii Zabirov.
