# Selection Examples Guide

This folder demonstrates `newton.selection.ArticulationView` and multi-world batched editing workflows.

## Expectations

- Preserve the mental model that selection is a high-level, public batching API layered on top of world-aware model data.
- Keep masks, labels, world ids, and per-world reset flows readable. Silent world-mixing bugs are hard to spot here.
- Prefer examples that show how to mutate articulated scenes through the public selection API, not through `_src`.

## Validation

- Run `test_selection.py` and any example regression covering the changed behavior.
