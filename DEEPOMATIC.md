# Deepomatic fork of mobile-forge

Recipes used by the mobile native-wheel pipeline in Deepomatic/mobile-inference
(`tools/mobile-wheels`). The pipeline builds the exact versions pinned in
deepomatic-workflows `uv.lock` for the targets in [`targets.toml`](targets.toml).

## Branches

| Branch | Role | Who updates it |
|---|---|---|
| `main` | Pure mirror of `flet-dev/mobile-forge@main`. Never edited. | Weekly upstream sync (fast-forward only) |
| `deepomatic` (default) | `main` + our commits: recipes, `targets.toml`, our agent skill. The only build source. | Only the pipeline's LLM-free push job, after L3 is green |
| `auto/<pkg>-<ver>` | Candidate recipe fixes from the agent loop | Pipeline push job |
| `python3.12` | Frozen Feb-2025 snapshot of flet's old branch | Nobody |

Upstream changes reach `deepomatic` by **merging** `main` (never a rebase:
force pushes are forbidden on `deepomatic`). Keep our changes out of upstream
files where possible (this file instead of `README.rst`) to keep merges clean.

## Protection

- `deepomatic`: deletion and force push are blocked for everyone; ordinary
  pushes are restricted to the repository-admin role (the pipeline push token).
- `python3.12`: frozen (no update, no force push, no deletion).
- GitHub Actions is disabled on this fork: builds run in Deepomatic/mobile-inference.

## Rules for recipes

This repository is public: no secrets, internal URLs or private sources.
Every source must come from PyPI or carry a recipe-pinned sha256.
