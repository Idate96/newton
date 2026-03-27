# Newton Local Agent Reference

This directory supplements the hierarchical `AGENTS.md` files with a small amount
of cross-cutting context. The main workflow is still:

1. Read the repo root [`AGENTS.md`](../../AGENTS.md).
2. Read the nearest `AGENTS.md` under the folder you plan to edit.
3. Use this directory only when you need a repo-wide map or maintenance rules
   that would make a local folder guide too large.

## Repo Map

- [`newton/`](../../newton): public package surface
- [`newton/_src/`](../../newton/_src): internal implementation tree
  - [`core/`](../../newton/_src/core): shared enums, axes, and low-level types
  - [`sim/`](../../newton/_src/sim): `ModelBuilder`, `Model`, `State`, `Control`, `Contacts`, articulation
  - [`sim/ik/`](../../newton/_src/sim/ik): inverse kinematics pipeline
  - [`geometry/`](../../newton/_src/geometry): geometry types and collision
  - [`math/`](../../newton/_src/math): Warp-safe helper math and spatial conventions
  - [`solvers/`](../../newton/_src/solvers): backend stepping implementations
  - [`sensors/`](../../newton/_src/sensors): measurement-producing APIs
  - [`viewer/`](../../newton/_src/viewer): viewer and recorder backends
  - [`utils/`](../../newton/_src/utils): importers, selection, assets, mesh helpers
  - [`usd/`](../../newton/_src/usd): schema resolvers and authored-attribute translation
- [`newton/examples/`](../../newton/examples): runnable demos and smoke-test targets
  - `basic/`, `robot/`, `sensors/`, `selection/`, `cloth/`, `cable/`, `contacts/`, `diffsim/`, `ik/`, `mpm/`, `multiphysics/`, `softbody/`
- [`newton/tests/`](../../newton/tests): unittest-based regression suite
- [`asv/`](../../asv): performance benchmarks
- [`docs/`](../../docs): public Sphinx documentation
- [`.github/`](../../.github): workflows, templates, and automation
- [`scripts/`](../../scripts): repo-local helper scripts
  - [`ci/`](../../scripts/ci): CI and docs-release helpers
- [`.github/`](../../.github): GitHub workflows, issue templates, and PR template
- [`scripts/`](../../scripts): CI-facing helper scripts

## Common Edit Workflows

- Public API addition:
  - implement the internal behavior
  - expose it through the right public module
  - run `uv run python docs/generate_api.py`
  - update docs, examples, and changelog if users will see it
- Runtime or solver change:
  - update the nearest `_src` guide if invariants or extension points changed
  - run targeted runtime, solver, and sensor or viewer tests as needed
  - update ASV coverage if performance behavior is part of the change
- Example change:
  - keep the public API boundary intact
  - preserve the `Example` contract
  - update README screenshots and `newton/tests/test_examples.py` coverage
- Docs change:
  - keep public docs user-facing
  - keep local agent docs short and structural

## Current Folder Guides

- [`AGENTS.md`](../../AGENTS.md)
- [`newton/AGENTS.md`](../../newton/AGENTS.md)
- [`newton/_src/AGENTS.md`](../../newton/_src/AGENTS.md)
- [`newton/_src/core/AGENTS.md`](../../newton/_src/core/AGENTS.md)
- [`newton/_src/sim/AGENTS.md`](../../newton/_src/sim/AGENTS.md)
- [`newton/_src/sim/ik/AGENTS.md`](../../newton/_src/sim/ik/AGENTS.md)
- [`newton/_src/geometry/AGENTS.md`](../../newton/_src/geometry/AGENTS.md)
- [`newton/_src/math/AGENTS.md`](../../newton/_src/math/AGENTS.md)
- [`newton/_src/solvers/AGENTS.md`](../../newton/_src/solvers/AGENTS.md)
- [`newton/_src/sensors/AGENTS.md`](../../newton/_src/sensors/AGENTS.md)
- [`newton/_src/viewer/AGENTS.md`](../../newton/_src/viewer/AGENTS.md)
- [`newton/_src/utils/AGENTS.md`](../../newton/_src/utils/AGENTS.md)
- [`newton/_src/usd/AGENTS.md`](../../newton/_src/usd/AGENTS.md)
- [`newton/examples/AGENTS.md`](../../newton/examples/AGENTS.md)
- [`newton/examples/basic/AGENTS.md`](../../newton/examples/basic/AGENTS.md)
- [`newton/examples/robot/AGENTS.md`](../../newton/examples/robot/AGENTS.md)
- [`newton/examples/sensors/AGENTS.md`](../../newton/examples/sensors/AGENTS.md)
- [`newton/examples/selection/AGENTS.md`](../../newton/examples/selection/AGENTS.md)
- [`newton/examples/cloth/AGENTS.md`](../../newton/examples/cloth/AGENTS.md)
- [`newton/examples/cable/AGENTS.md`](../../newton/examples/cable/AGENTS.md)
- [`newton/examples/contacts/AGENTS.md`](../../newton/examples/contacts/AGENTS.md)
- [`newton/examples/diffsim/AGENTS.md`](../../newton/examples/diffsim/AGENTS.md)
- [`newton/examples/ik/AGENTS.md`](../../newton/examples/ik/AGENTS.md)
- [`newton/examples/mpm/AGENTS.md`](../../newton/examples/mpm/AGENTS.md)
- [`newton/examples/multiphysics/AGENTS.md`](../../newton/examples/multiphysics/AGENTS.md)
- [`newton/examples/softbody/AGENTS.md`](../../newton/examples/softbody/AGENTS.md)
- [`newton/tests/AGENTS.md`](../../newton/tests/AGENTS.md)
- [`asv/AGENTS.md`](../../asv/AGENTS.md)
- [`docs/AGENTS.md`](../../docs/AGENTS.md)
- [`.github/AGENTS.md`](../../.github/AGENTS.md)
- [`scripts/AGENTS.md`](../../scripts/AGENTS.md)
- [`scripts/ci/AGENTS.md`](../../scripts/ci/AGENTS.md)
- [`.github/AGENTS.md`](../../.github/AGENTS.md)
- [`scripts/AGENTS.md`](../../scripts/AGENTS.md)
- [`scripts/ci/AGENTS.md`](../../scripts/ci/AGENTS.md)

## Maintenance Rules

- If you add a new subsystem directory with its own editing invariants, add a
  local `AGENTS.md` there.
- If you materially change a subsystem's contracts, update the nearest guide in
  the same change.
- Keep user-facing docs and examples free of `_src` imports.
- Prefer short, actionable guidance over exhaustive prose. The goal is to help
  downstream agents choose the right layer quickly.
