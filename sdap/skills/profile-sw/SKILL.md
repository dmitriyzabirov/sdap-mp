---
name: profile-sw
description: Software domain gate profile - build and verify checks for S7/S8, seal for S9.
---
# Software profile
- S7 build: code compiles, linter clean, types check.
- S8 verify: unit + integration tests (L3 adds property-based + coverage threshold).
- S9 seal: git commit (L2 signed commit, L3 notarized).
