# IK Guide

Scope: `newton/_src/sim/ik/`.

- Public entry point is `newton.ik`. This folder is the implementation.
- `IKSolver` is an orchestrator:
  - sample or select initial seeds
  - expand batched problems
  - evaluate FK and costs
  - run LM or L-BFGS
  - pick the best seed per problem
- Keep Jacobian modes coherent across the full stack:
  - `AUTODIFF`
  - `ANALYTIC`
  - `MIXED`
- Add new objectives in `ik_objectives.py`. Per-problem data should live in device arrays indexed by `problem_idx`, not in Python-side per-problem objects.
- If you change the objective contract, batch layout, or residual packing, update both optimizer backends and shared helpers in `ik_common.py`.
- `ik_solver.py` should stay focused on orchestration. Backend-specific numerical behavior belongs in `ik_lm_optimizer.py` or `ik_lbfgs_optimizer.py`.
- Good regression anchors are `newton/tests/test_ik.py`, `newton/tests/test_ik_lbfgs.py`, and related IK benchmarks.
