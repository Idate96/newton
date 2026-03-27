# Differentiable Simulation Examples Guide

This folder covers differentiable workflows and gradient-sensitive demos.

## What Lives Here

- Ball, bear, cloth, drone, soft-body, and spring-cage optimization or control examples.

## Expectations

- Treat differentiability as the point of the example, not a side effect.
- Avoid introducing non-differentiable shortcuts or hidden side effects when editing these examples.
- If a solver or math helper changes gradient behavior, revisit these examples explicitly.

## Validation

- Run the diffsim-related tests and the affected example regression.
