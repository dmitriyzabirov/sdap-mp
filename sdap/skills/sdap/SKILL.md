---
name: sdap
description: SDAP (Spec-Driven Agentic Pipeline) — build software from specs as an S1-S9 state machine with pass/rollback/escalate gates, cheap-first model routing, and recompute-only-dirty economy. Use to run or drive the pipeline in a project. Start with /sdap:run.
---

# SDAP — Spec-Driven Agentic Pipeline

A spec-driven, multi-domain (software / hardware / mechanical) build run as a state machine.
Steps S1-S9 each transform an input, then pass a **gate**: `pass` / `rollback(to, reason)` / `escalate`.

## Run it (two commands)
- **`/sdap:run`** — scaffolds working files (`config/`, `state/`, `spec/`) into this project if missing,
  then drives the S1-S9 build via the `orchestrator`.
- **`/sdap:change "<new requirement>"`** — fold a new/changed requirement, recompute only the dirty subtree, re-seal.

Put real requirements in `spec/requirements-v1.md`; set LEVEL in `state/nodes.json`.

## The single knob: LEVEL (`state/nodes.json` → `level`)
Same steps at every level; only gate rigor and the model ceiling change.
- **L1** — smoke. One agent path, deconflict light, smoke tests. Ceiling: sonnet.
- **L2** — full. Deconflict (S5/S6) run, unit+integration tests, human signs off S3 + S9. Ceiling: opus.
- **L3** — strict. + property/edge coverage threshold, human at every gate, cryptographic seal. Ceiling: fable.

## Model routing — "cheap first, strong only when needed" (`config/models.json`)
Every step has a **ladder** cheap→strong, truncated at the level ceiling.
- A step's first attempt always uses the cheapest rung.
- On `rollback`/gate-fail, the orchestrator bumps one rung and retries the same step on a stronger model.
- When the top rung (ceiling) also fails → escalate to a human.
- The orchestrator itself is pinned to the cheapest model — it routes, it does not reason about domain content.

## Three economy rules (hard)
1. A step receives **only its dirty input subtree**, never the whole project.
2. A `proven`/`cached` node is **never recomputed**.
3. Every step **starts at ladder[0]**; it climbs only on failure.

## Domain skipping
`step-allocate` (S3) marks which domains are `live` in `state/nodes.json`. Steps S4-S8 run per live
domain only. An absent domain has no node → no worker spawned → zero tokens; it is permanently "clean".

## The steps
S1 Intake · S2 Decompose · S3 Allocate · S4 Spec · S5 Deconflict (within domain) · S6 Cross-domain
deconflict · S7 Build · S8 Verify · S9 Seal. Each step's exact transform and "gate passes when…"
clause lives in its `step-<name>` skill.

## Change loop
`/sdap:change "<new requirement>"` → fold into a new `spec/requirements-vN.md` → `impact-analysis` marks
the minimal dirty set → orchestrator recomputes only those, re-running S5/S6 against ALL existing specs → re-seal.

## Naming
The customer's input document is **requirements** (`spec/requirements-vN.md`), referred to as **req**.
"Spec" is reserved for the S4 formal specs.
