# SDAP — decisions log

Engineering decisions for the Spec-Driven Agentic Pipeline **itself** (the build tool).
Separate from any project's ARCHITECTURE.md: those record the product being built; this records the tool.
Canonical SDAP source = this plugin dir (`~/.claude/local-plugins/sdap-mp/sdap/`) — the `Downloads/spec-pipeline` original is the seed.

Append: `date · decision · why`.

- 2026-07-02 · `step-verify` (S8) must ACTUALLY run tests — no simulation / self-reported results (else `rollback`); tests must also be idempotent/self-cleaning (green on two consecutive runs) · caught an L1 build faking "all pass" + a 14/6 flake against leftover data.
- 2026-07-02 · `step-build` (S7) forbids mocks/stubs/hardcoded-config passed off as done (`rollback`) · L1 build shipped in-memory storage, hardcoded niche, mocked auth.
- 2026-07-02 · `config/models.json` model IDs refreshed: `haiku→claude-haiku-4-5-20251001`, `sonnet→claude-sonnet-5` (opus/fable already current) · README warns model strings go stale.
- 2026-07-02 · Two executors, one source: canonical = the plugin skills + `config/models.json`. Terminal `/sdap:run` (plugin orchestrator) and the in-session Workflow runner both read them; the Workflow runner will read skills+config (wire on next run) instead of hardcoding prompts, to avoid drift.
- 2026-07-02 · Seal (S9) stays thin: baseline snapshot + audit record only, trusting S8's real verdict (economy rule #2: never recompute proven). Re-verifying the full suite at seal is redundant — it was Workflow over-caution after the fakery episode, dropped.
- 2026-07-02 · Packaged as a user-scope Claude Code plugin `sdap` (marketplace `sdap-mp`) + an in-session Workflow runner, so it runs from chat without a nested `claude` session. Namespacing (plugin skills → `sdap:*`) worked in practice; no fix needed.
- 2026-10-03 · `config/models.json` model IDs refreshed again: `sonnet→claude-sonnet-5-5`, `opus→claude-opus-5-5`, `fable→claude-fable-5-1` (haiku unchanged); plugin version 0.1.1; `version` kept only in `plugin.json` · the marketplace now lives in its own private GitHub repo (`dmitriyzabirov/sdap-mp`) so a team gets one pinned version; stale model strings otherwise break S7/S8 routing.
- 2026-10-03 · license Apache-2.0 (`LICENSE`, `NOTICE` at the repo root and inside `sdap/`, which is what a plugin install copies); repo made public; plugin version 0.1.2 · the owner wants authorship preserved: Apache keeps the notice through `NOTICE` and adds an express patent grant and no trademark rights.

## Deferred / optional
- Per-node tier memory: start historically-hard nodes higher to skip wasted cheap attempts, paired with periodic downward retry (in case upstream changes made a node easier). Trades cost for speed. Not implemented — current model always starts each node at `ladder[0]` (cheapest).
- 2026-07-18 · ladders start at sonnet, orchestrator sonnet (was haiku): radiotext sim build showed haiku failing every S7 milestone (fake AT1 downsample, flat SNR, synthetic capacity adjacency, skipped M5 mandates) while S4/S5 doc steps passed; net cost of haiku-first on build steps was negative. haiku tier kept for manual override.
