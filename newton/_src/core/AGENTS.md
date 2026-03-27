# Core Internals Guide

This folder holds low-level types and helpers used across nearly every Newton subsystem.

## Important Files

- `types.py`: shared enums, vector and transform aliases, device helpers, and axis utilities.
- `__init__.py`: the low-level symbols re-exported into `newton.__init__`.

## Rules For This Folder

- Keep dependencies minimal. This layer should stay lightweight and broadly reusable.
- Changes here are high blast-radius changes. Expect follow-on edits in `sim/`, `geometry/`, `math/`, and public exports.
- Be explicit about units, dtypes, and coordinate conventions. These helpers shape the rest of the codebase.

## Validation

- Run targeted tests that touch the affected consumers, not just the local module.
- If a public symbol changes here, update the corresponding exports in `newton/__init__.py` or `newton/math.py`.
