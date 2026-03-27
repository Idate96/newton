# Runtime Architecture Guide

Scope: `newton/_src/sim/`.

- The core lifecycle is:
  - `ModelBuilder`: authoring-time scene graph
  - `finalize()`: compile Python-side data into runtime arrays
  - `Model`: static source of truth for geometry, topology, materials, worlds, and custom-attribute metadata
  - `model.state()`, `model.control()`, `model.contacts()`: allocate runtime buffers
  - `model.collide(...)` or `CollisionPipeline.collide(...)`
  - `solver.step(state_in, state_out, control, contacts, dt)`
- Treat `Model` as static. If model dimensions or requested attributes change, reallocate `State`, `Control`, and `Contacts`.
- Request extended state and contact attributes before allocation. Late requests do not patch existing buffers.
- Use `ModelBuilder` for authoring and importer changes. Do not hand-edit compiled model arrays unless you are fixing finalization logic itself.
- `CollisionPipeline` is the reusable collision subsystem. `Model.collide()` is a convenience wrapper around it.
- Articulation helpers (`eval_fk`, `eval_ik`, `eval_jacobian`, `eval_mass_matrix`) depend on the same runtime layout as `State` and joint buffers. Keep those conventions aligned.
- World semantics are important:
  - world `-1` means global/shared entities
  - multi-world tables and offsets affect collision, selection, sensors, and viewers
- Public entry points are re-exported from `newton/__init__.py`. If behavior becomes user-facing, update wrappers, tests, and docs together.
- Read `sim/ik/AGENTS.md` before changing IK internals.
