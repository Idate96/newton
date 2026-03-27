# Newton Development Guidelines

- `newton/_src/` is internal. Examples and docs must not import from `newton._src`. Expose user-facing symbols via public modules (`newton/geometry.py`, `newton/solvers.py`, etc.).
- Breaking changes require a deprecation first. Do not remove or rename public API symbols without deprecating them in a prior release.
- Prefix-first naming for autocomplete: `ActuatorPD` (not `PDActuator`), `add_shape_sphere()` (not `add_sphere_shape()`).
- Prefer nested classes for self-contained helper types/enums.
- PEP 604 unions (`x | None`, not `Optional[x]`). Annotate Warp arrays with concrete dtypes (`wp.array(dtype=wp.vec3)`).
- Follow Google-style docstrings. Types in annotations, not docstrings. `Args:` use `name: description`.
  - Sphinx cross-refs (`:class:`, `:meth:`) with shortest possible targets. Prefer public API paths; never use `newton._src`.
  - SI units for physical quantities in public API docstrings: `"""Particle positions [m], shape [particle_count, 3]."""`. Joint-dependent: `[m or rad]`. Spatial vectors: `[N, N·m]`. Compound arrays: per-component. Skip non-physical fields.
- Run `docs/generate_api.py` when adding public API symbols.
- Avoid new required dependencies. Strongly prefer not adding optional ones. Use Warp, NumPy, or stdlib when possible.
- Create a feature branch before committing. Never commit directly to `main`. Use `<username>/feature-desc`.
- Imperative mood in commit messages ("Fix X", not "Fixed X"), ~50 char subject, body wraps at 72 chars explaining what and why.
- Verify regression tests fail without the fix before committing.
- Pin GitHub Actions by SHA: `action@<sha>  # vX.Y.Z`. Check `.github/workflows/` for allowlisted hashes.
- In SPDX copyright lines, use the year the file was first created. Do not create date ranges or update the year when modifying a file.

Run `uvx pre-commit run -a` to lint and format before committing. Use `uv` for commands; fall back to `venv` or `conda` only if `uv` is unavailable.

Always use `unittest`, not `pytest`.

```bash
# Examples
uv sync --extra examples
uv run -m newton.examples basic_pendulum

# Tests
uv run --extra dev -m newton.tests
uv run --extra dev -m newton.tests -k test_viewer_log_shapes
uv run --extra dev -m newton.tests -k test_basic.example_basic_shapes
uv run --extra dev --extra torch-cu12 -m newton.tests

# Benchmarks
uvx --with virtualenv asv run --launch-method spawn main^!
```

## Agent Navigation

Read this file first, then read the nearest `AGENTS.md` under the folder you plan to edit.

- `newton/AGENTS.md`: public package surface and top-level repo map
- `newton/_src/AGENTS.md`: internal implementation map
- `newton/_src/core/AGENTS.md`: low-level shared types and enums
- `newton/_src/sim/AGENTS.md`: runtime object lifecycle
- `newton/_src/sim/ik/AGENTS.md`: inverse kinematics pipeline
- `newton/_src/geometry/AGENTS.md`: geometry and collision internals
- `newton/_src/math/AGENTS.md`: Warp-safe math helpers and spatial conventions
- `newton/_src/solvers/AGENTS.md`: solver contracts and backend map
- `newton/_src/sensors/AGENTS.md`: sensor update order and render-backed sensors
- `newton/_src/viewer/AGENTS.md`: viewer and recorder backends
- `newton/_src/utils/AGENTS.md`: importers, selection, and asset helpers
- `newton/_src/usd/AGENTS.md`: schema resolvers and USD attribute mapping
- `newton/examples/AGENTS.md`: example discovery, CLI, and test contract
- `newton/examples/basic/AGENTS.md`: introductory public-API examples
- `newton/examples/robot/AGENTS.md`: imported robot, policy, and controller demos
- `newton/examples/sensors/AGENTS.md`: public sensor and sensor-viewer demos
- `newton/examples/selection/AGENTS.md`: batched articulation and selection demos
- `newton/examples/cloth/AGENTS.md`: cloth and Style3D-focused demos
- `newton/examples/cable/AGENTS.md`: cable-focused demos
- `newton/examples/contacts/AGENTS.md`: contact and stacking demos
- `newton/examples/diffsim/AGENTS.md`: differentiable simulation demos
- `newton/examples/ik/AGENTS.md`: inverse-kinematics demos
- `newton/examples/mpm/AGENTS.md`: MPM and particle-material demos
- `newton/examples/multiphysics/AGENTS.md`: cross-subsystem demos
- `newton/examples/softbody/AGENTS.md`: soft-body demos
- `newton/tests/AGENTS.md`: unittest runner, device fanout, and example smoke tests
- `asv/AGENTS.md`: benchmark structure and performance invariants
- `docs/AGENTS.md`: public docs tooling and local-agent-doc boundaries
- `.github/AGENTS.md`: workflows, templates, and release automation boundaries
- `scripts/AGENTS.md`: repo-local helper scripts
- `scripts/ci/AGENTS.md`: CI helper scripts
- `docs/agent_reference/README.md`: longer-lived local reference index

## Working Rules For Agents

- Prefer public imports (`newton.*`) in examples, tests, and public docs. Only use `_src` when editing internals.
- If you add or change public API, update the relevant wrapper module, regenerate API pages with `uv run python docs/generate_api.py`, and update README or docs if the change is user-visible.
- If you change a subsystem's invariants, architecture, or extension points, update the nearest `AGENTS.md` in the same change.
- Keep local agent docs in `docs/agent_reference/` concise and internal-facing. Keep `docs/` user-facing unless you intentionally promote material into the public site.

## PR Instructions

- If opening a pull request on GitHub, use the template in `.github/PULL_REQUEST_TEMPLATE.md`.
- If a change modifies user-facing behavior, append an entry at the end of the correct category (`Added`, `Changed`, `Deprecated`, `Removed`, `Fixed`) in `CHANGELOG.md`'s `[Unreleased]` section. Use imperative present tense ("Add X") and avoid internal implementation details.
- For `Deprecated`, `Changed`, and `Removed` entries, include migration guidance: "Deprecate `Model.geo_meshes` in favor of `Model.shapes`".

## Examples

- Follow the `Example` class format.
  - Implement `test_final()`, which runs after the example completes to verify simulation state is valid.
  - Optionally implement `test_post_step()`, which runs after every step for per-step validation.
- Register new examples in `README.md` with `python -m newton.examples <name>` and a 320x320 screenshot.
