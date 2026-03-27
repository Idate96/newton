# IK Examples Guide

This folder demonstrates the public inverse-kinematics API.

## What Lives Here

- Franka IK
- Custom objectives
- Cube stacking
- H1 IK

## Expectations

- Prefer the public `newton.ik` API and public articulation helpers.
- Keep objective construction and optimizer choice visible in the example.
- If you change IK objectives, optimizers, or public solver behavior, update these examples together with the API change.

## Validation

- Run IK-related tests and the changed example regression.
