# Multiphysics Examples Guide

This folder contains demos that intentionally cross subsystem boundaries.

## What Lives Here

- Softbody-to-cloth interaction
- Gift-wrapping style composite scene

## Expectations

- These examples are integration tests in demo form. Changes here often mean something moved in more than one subsystem.
- If a change spans solvers, geometry, sensors, or viewers, make sure the example still tells a clear story rather than becoming a stress test with no diagnostic value.

## Validation

- Run the affected example regression plus the subsystem tests for each changed area.
