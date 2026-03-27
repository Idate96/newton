# Viewer Guide

Scope: `newton/_src/viewer/`.

- Public entry point is `newton.viewer`. This folder implements viewer and recorder backends.
- Common lifecycle:
  - `set_model()`
  - `begin_frame()`
  - `log_state()`
  - `end_frame()`
- `ViewerBase` owns world offsets, geometry and instance caches, visibility state, and common overlays. Assume model topology is mostly fixed after `set_model()` unless you are explicitly re-binding.
- Backend roles:
  - `viewer_gl.py`: interactive renderer and UI
  - `viewer_file.py`: recording sink
  - `viewer_usd.py`: USD export
  - `viewer_rerun.py` and `viewer_viser.py`: external integrations
- `ViewerGL` contains performance-critical fast paths for batched uploads. Be cautious about changes that accidentally fall back to slower base behavior.
- Viewer-side mutation is limited. `apply_forces()` is the main built-in path that pushes forces back into simulation state.
- Re-test world offsets, picking, geometry batching, recorder backends, and viewer-specific examples after nontrivial changes.
