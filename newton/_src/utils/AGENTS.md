# Utils Guide

Scope: `newton/_src/utils/`.

- This folder holds importers (`import_usd`, `import_urdf`, `import_mjcf`), selection, asset download helpers, and mesh or texture utilities.
- Importer boundary:
  - `ModelBuilder.add_*()` methods delegate here
  - importer return structures are part of the internal contract, especially for diagnostics, path maps, and selection
- `import_usd.py` returns path maps and schema-derived metadata used by downstream code. If you refactor those results, update all callers together.
- `selection.py` provides `ArticulationView`. It assumes compatible articulation layouts across selected worlds and uses label-based indexing rather than ad hoc raw indices.
- `download_assets.py` is the sanctioned path for external example assets and policies. Keep external-asset workflows explicit.
- If you add user-facing import, selection, or helper behavior, re-export it from `newton.usd`, `newton.selection`, or `newton.utils` as appropriate.
