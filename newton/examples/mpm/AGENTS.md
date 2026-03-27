# MPM Examples Guide

This folder exercises MPM and MPM-adjacent particle workflows.

## What Lives Here

- Granular and viscous material examples
- Grain rendering
- Beam twist
- Multi-material and snow-ball setups
- Two-way coupling and robot interaction

## Expectations

- These examples are performance-sensitive and visually diagnostic.
- Be explicit about material behavior and coupling mode when editing an example.
- Solver changes here should usually trigger benchmark thinking as well as regression testing.

## Validation

- Run MPM-related tests and the affected example regression.
- Consider the relevant `asv` benchmark if performance changed.
