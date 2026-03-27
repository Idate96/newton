# Documentation Guide

This folder contains the public documentation site and the local agent-reference index.

## Split The Two Doc Layers

- Public docs: `index.rst`, `guide/`, `concepts/`, `integrations/`, `tutorials/`, and `api/`.
- Local agent docs: `agent_reference/` plus the folder-local `AGENTS.md` files across the repo.

## Rules For Public Docs

- Public docs and examples must not import `newton._src` directly.
- If you add public API symbols, keep `docs/generate_api.py` and the generated API pages in sync.
- If you change user-facing behavior, update the relevant guide or concept page, not only the API docstring.
- Keep deployment assumptions aligned with the GitHub workflows in `.github/workflows/docs-dev.yml` and `.github/workflows/docs-release.yml`.

## Local Build And Serve

```bash
uv run --extra docs --extra sim sphinx-build -j auto -b html docs docs/_build/html
python docs/serve.py
```

## Important Files

- `conf.py`: Sphinx configuration, extensions, and version-switcher setup.
- `generate_api.py`: API page generation for public modules.
- `serve.py`: local static server with correct MIME handling.
- `agent_reference/README.md`: repo-local index for downstream agents.

## When To Update This Folder

- Public API changes
- Docs build or deployment changes
- New tutorials, guides, or concept pages
- Changes to the local agent-reference strategy
