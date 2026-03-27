# Geometry And Collision Guide

Scope: `newton/_src/geometry/`.

- This folder owns runtime geometry types, collision broad phase, narrow phase, raycast, SDF, hydroelastic contact generation, remeshing, and terrain helpers.
- Keep the collision split clear:
  - broad phase: candidate pair generation
  - narrow phase: contact generation and reduction
  - `contact_data.py`: intermediate payloads
  - `types.py`: geometry containers and enums
- USD import does not start here. Import enters through `ModelBuilder.add_usd()` plus helpers in `_src/utils` and `_src/usd`. This folder consumes finalized geometry during collision.
- `Mesh.build_sdf()`, `sdf_utils.py`, and hydroelastic code paths are coupled. Do not change one without checking the others.
- Preserve contact buffer and capacity semantics. Many downstream paths rely on active counts rather than fully cleared buffers.
- Important tests include the contact, raycast, SDF, hydroelastic, terrain, and remesh suites under `newton/tests/`.
