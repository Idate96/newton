# Examples Guide

Scope: `newton/examples/`.

- Discovery is filesystem-based. Every `example_*.py` file under a category folder becomes `python -m newton.examples <short_name>`.
- Keep examples on public API only. Do not import `newton._src`.
- Example contract:
  - expose an `Example` class
  - optionally define `create_parser()`
  - use `newton.examples.init()` and `newton.examples.run()`
  - implement `test_final()`
  - optionally implement `test_post_step()`
- The in-viewer browser and reset logic live in `newton/examples/__init__.py`. Be careful when changing discovery, naming, or startup flow.
- New examples usually need all of the following:
  - a README entry
  - a 320x320 screenshot
  - coverage in `newton/tests/test_examples.py`
- Use `newton.examples.get_asset()` for bundled assets and `newton.utils.download_asset()` only when an example intentionally depends on external assets or policies.
- Family-specific guides already exist under:
  - `basic/`
  - `robot/`
  - `sensors/`
  - `selection/`
  - `cloth/`
  - `cable/`
  - `contacts/`
  - `diffsim/`
  - `ik/`
  - `mpm/`
  - `multiphysics/`
  - `softbody/`
- Read the family guide before editing a specific example domain.
