# Internal Source Guide

Scope: everything under `newton/_src/`.

- `_src` is the implementation layer, not the public API. If a change should be user-facing, expose it through `newton/*.py`.
- Choose the right subsystem before editing:
  - `core`: shared enums, axis helpers, and low-level types
  - `sim`: build-time objects, runtime buffers, articulation utilities
  - `sim/ik`: inverse kinematics objectives and optimizers
  - `geometry`: collision and geometry primitives
  - `math`: Warp-safe utility and spatial math
  - `solvers`: stepping backends
  - `sensors`: measurement APIs
  - `viewer`: visualization and recorder backends
  - `utils`: importers, selection, download helpers, mesh and texture utilities
  - `usd`: schema and authored-attribute translation
- Keep cross-layer edits explicit. If a runtime change affects examples, tests, benchmarks, or docs, update them in the same change.
- Avoid turning internal helper paths into de facto API. Prefer adding a public wrapper if downstream code needs a new capability.
- Update the nearest folder `AGENTS.md` when you materially change local invariants or extension points.
