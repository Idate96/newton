# Newton Package Guide

Scope: everything under `newton/`.

- The supported import surface is the package root and the thin public modules:
  - `newton`
  - `newton.geometry`
  - `newton.ik`
  - `newton.math`
  - `newton.selection`
  - `newton.sensors`
  - `newton.solvers`
  - `newton.usd`
  - `newton.utils`
  - `newton.viewer`
- `newton/_src` is the implementation tree. If a change should be consumable by users, re-export it through a public wrapper and keep `__all__` aligned.
- High-level package map:
  - `_src/core`: shared enums, axis helpers, and other low-level types
  - `_src/sim`: model building, runtime state, articulation, and IK
  - `_src/geometry`: geometry types, collision, raycast, SDF, hydroelastic
  - `_src/utils`: importers, selection, assets, mesh and texture helpers
  - `_src/usd`: schema resolvers and authored-attribute mapping
  - `_src/solvers`: backend-specific stepping
  - `_src/sensors`: measurement-producing APIs
  - `_src/viewer`: viewer, recorder, and export backends
  - `_src/math`: Warp-compatible helpers and spatial conventions
  - `examples`: runnable demos and smoke-test targets
  - `tests`: unittest-based regressions
- Example family folders under `newton/examples/*` already carry more specific local guides. Read those when editing a specific family.
- Preferred edit flow for new user-facing behavior:
  - implement or modify the internal subsystem
  - expose the symbol through the correct public module
  - run `uv run python docs/generate_api.py` if the public API changed
  - update docs, examples, and changelog entries as needed
- Do not teach public docs or examples to import from `_src`.
- Read the nearest subsystem guide before editing deeper folders.
