# CI Script Guide

This folder contains small helper scripts used by GitHub Actions.

## Important Files

- `update_docs_switcher.py`: maintains `switcher.json` for versioned docs deployment.

## Rules For This Folder

- Treat these scripts as workflow plumbing, not general-purpose utilities.
- Keep input validation strict. A workflow helper should fail loudly on malformed release metadata.
- If you change release docs layout or switcher semantics, update the corresponding workflow and `docs/AGENTS.md` together.
