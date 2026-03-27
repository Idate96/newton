# GitHub Workflow Guide

This folder contains issue templates, the PR template, and GitHub Actions workflows.

## Rules For This Folder

- Pin actions by SHA and keep the version comment when applicable.
- Keep workflow behavior aligned with the repo policies in the root `AGENTS.md`, especially for docs deployment, changelog expectations, and testing.
- If you change docs or release automation, update `docs/AGENTS.md` and any helper scripts in `scripts/ci/`.
- If you change required checks or workflow structure, make sure contributor-facing docs still describe the real workflow.

## Important Files

- `PULL_REQUEST_TEMPLATE.md`
- `workflows/docs-dev.yml`
- `workflows/docs-release.yml`
- `workflows/ci.yml`, `workflows/pr.yml`, and GPU benchmark or test workflows
