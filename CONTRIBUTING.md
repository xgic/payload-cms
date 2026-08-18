# Contributing — XGIC Payload CMS (template)

Thanks for contributing.

## Scope

This repo is a **thin template**. Prefer:

| Change type | Target repository |
|-------------|-------------------|
| Dev Container image / Dockerfile / compose producer | [payload-cms-dev](https://github.com/xgic/payload-cms-dev) |
| CLI commands / libraries | [cli](https://github.com/xgic/cli), [dev-cli](https://github.com/xgic/dev-cli), [payload-cms-cli](https://github.com/xgic/payload-cms-cli) |
| Template Docker Compose-first `devcontainer.json` / `.devcontainer/docker-compose.yml`, app extensions, template docs | **this repo** |

## Process

1. Open an issue (public-safe language only).
2. Branch from `main`; Conventional Commits.
3. PR with labels; **human UI merge** only.
4. Standards: https://github.com/xgic/ai

## Public-safe

No private hosts, paths, tracker IDs, or secrets in issues/PRs.  
Gate: https://github.com/xgic/ai/blob/main/docs/BASE-STANDARDS-FOR-ORCHESTRATED-REPOS.md

## Maintainer notes

- [docs/repository-settings.md](docs/repository-settings.md) — branch protection and CI gates
- [README standards (hub)](https://github.com/xgic/ai/blob/main/docs/readme-standards.md)
