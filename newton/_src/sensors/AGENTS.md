# Sensor Guide

Scope: `newton/_src/sensors/`.

- Public entry point is `newton.sensors`. This folder implements the sensor classes.
- Update order matters:
  - construct sensors before allocating `State` or `Contacts` if they auto-request extended attributes
  - make sure contact data is current before calling `SensorContact.update()`
- Keep the sensor roles distinct:
  - `SensorContact`: contact-force aggregation
  - `SensorFrameTransform`: relative transforms
  - `SensorIMU`: acceleration and angular velocity
  - `SensorRaycast`: simpler depth-oriented camera
  - `SensorTiledCamera`: full render-backed multi-channel camera
- Preserve multi-world and multi-camera tensor shape conventions. `SensorTiledCamera` is especially easy to break with transpose mistakes.
- `SensorTiledCamera` is not a thin wrapper. Changes there usually affect `warp_raytrace` rendering code too.
- Update sensor examples and sensor tests together when behavior changes.
