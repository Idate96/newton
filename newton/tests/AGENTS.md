# Test Suite Guide

This folder contains Newton's `unittest`-based regression suite.

## Important Files

- `__main__.py`: test entry point using the bundled parallel runner.
- `test_examples.py`: subprocess-based regression coverage for runnable examples.
- `unittest_utils.py`: device selection, helpers, and shared test utilities.
- `assets/` and `golden_data/`: test fixtures and reference outputs.

## Rules For This Folder

- Use `unittest`, not `pytest`.
- Prefer targeted subsystem tests named `test_<area>.py`.
- If you change an example, add or update the corresponding case in `test_examples.py` when needed.
- If you change viewer or sensor output that is checked against reference data, update the corresponding golden data carefully and explain why.
- Keep tests deterministic and reasonably scoped. Example tests are already time-budgeted and run as subprocesses.

## Common Commands

```bash
uv run --extra dev -m newton.tests
uv run --extra dev -m newton.tests -k test_viewer_log_shapes
uv run --extra dev -m newton.tests -k test_basic.example_basic_shapes
uv run --extra dev --extra torch-cu12 -m newton.tests
```
