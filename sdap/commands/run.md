---
description: Run SDAP (Spec-Driven Agentic Pipeline) in this project — scaffold working files if missing, then drive the S1-S9 build.
---

Run the Spec-Driven Agentic Pipeline in the current project.

1. If `config/models.json` or `state/nodes.json` are missing, scaffold the working files from the
   plugin template into the project **without overwriting anything that exists**:
   `cp -nR ${CLAUDE_PLUGIN_ROOT}/template/. .` — then report what was created vs already present.
2. Requirements live in `spec/requirements-v1.md`. If it is still the shipped placeholder, ask the
   user to put real requirements in before building.
3. LEVEL knob is in `state/nodes.json` (`L1` default | `L2` | `L3`).
4. Hand control to the `orchestrator` agent to run the S1-S9 state machine.

Change a requirement later: `/sdap:change "<new requirement>"`. Rules & step semantics: the `sdap` skill.
