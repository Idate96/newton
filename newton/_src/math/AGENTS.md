# Math Guide

Scope: `newton/_src/math/`.

- Public entry point is `newton.math`. This folder contains the real implementations.
- Most helpers are `@wp.func` or otherwise Warp-facing. Keep them kernel-safe and device-friendly.
- `spatial.py` is correctness-critical. Newton's spatial-vector conventions differ from Warp's ordering, so treat conversions there as architecture-level behavior.
- If you add a new public helper:
  - implement it here
  - re-export it from `newton/math.py`
  - regenerate API pages with `uv run python docs/generate_api.py`
- After nontrivial changes, run spatial math tests and any dependent IK or solver tests.
