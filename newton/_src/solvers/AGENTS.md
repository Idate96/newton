# Solver Guide

Scope: `newton/_src/solvers/`.

- Public entry point is `newton.solvers`. This folder implements the backends.
- `solver.py` defines `SolverBase`, common integration helpers, and the main contracts:
  - `step()`
  - `notify_model_changed()`
  - `register_custom_attributes()`
- Choose the right backend before editing:
  - `semi_implicit`: simple maximal-coordinate baseline
  - `xpbd`: iterative constraint projection
  - `mujoco`: MuJoCo and MuJoCo Warp bridge
  - `vbd`, `style3d`, `implicit_mpm`: cloth, soft-body, and particle-heavy paths
  - `featherstone`, `kamino`: articulated and constrained specializations
- Keep `SolverNotifyFlags` handling correct when model properties, inertias, or joint layouts mutate.
- Some backends require builder or model setup before construction, or custom attributes before state allocation. Preserve those setup requirements when refactoring.
- Backend capability docs in `newton/solvers.py` and `docs/api/newton_solvers.rst` must stay synchronized with the real implementation.
- Run backend-specific tests and relevant ASV benchmarks after performance-sensitive changes.
