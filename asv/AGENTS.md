# Benchmark Guide

This folder contains Airspeed Velocity benchmarks used for performance tracking.

## Layout

- `benchmarks/compilation/`: compilation and load-time costs.
- `benchmarks/setup/`: scene or model construction costs.
- `benchmarks/simulation/`: runtime costs for major simulation workloads.
- Top-level helpers such as `benchmark_ik.py` and `benchmark_mujoco.py` support reusable benchmark logic.

## Rules For This Folder

- Add or update a benchmark when a change is explicitly about performance or changes a hot path substantially.
- Keep benchmark scenarios focused and repeatable. They should measure one family of work, not an end-to-end kitchen sink.
- Use representative devices and skip logic rather than letting unsupported environments fail noisily.
- If a benchmark needs shared helper code, put it in a small reusable helper module instead of duplicating setup across files.

## Common Command

```bash
uvx --with virtualenv asv run --launch-method spawn main^!
```
