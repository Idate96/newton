# USD Guide

Scope: `newton/_src/usd/`.

- This folder is the authored-attribute and schema translation layer for USD-related workflows.
- `SchemaResolver` and `SchemaResolverManager` map authored USD attributes into Newton keys by prim category. Resolver priority changes can affect import behavior repo-wide.
- Keep mappings explicit for Newton, PhysX, and MuJoCo schemas. Avoid silent fallbacks that hide missing authored data.
- Reuse `usd/utils.py` for prim lookup, transforms, mesh and tetmesh extraction, and custom-attribute harvesting rather than reimplementing stage traversal logic.
- Coordinate closely with `_src/utils/import_usd.py` when resolver outputs change. Tests such as `test_import_usd.py`, `test_schema_resolver.py`, and site-related USD tests should move with those changes.
