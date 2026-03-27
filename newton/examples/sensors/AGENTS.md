# Sensor Examples Guide

This folder demonstrates the public sensor APIs and sensor-driven visualization workflows.

## What Lives Here

- Contact sensing
- IMU sensing
- Tiled camera rendering and display

## Expectations

- Prefer `newton.sensors` public classes.
- Make output layout and units obvious in the example.
- If a sensor requires custom CLI flags, extend the shared parser pattern instead of creating a one-off argument flow.

## Validation

- Run the corresponding `test_sensor_*` tests and the example regression when you change one of these examples.
