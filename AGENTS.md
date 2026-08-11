# AI Agent Instructions — XGIC Payload CMS (template)

Public repository. Multi-repo standards: https://github.com/xgic/ai  
Naming: [ADR-0001](https://github.com/xgic/ai/blob/main/docs/adr/0001-xgic-gitlab-architecture-and-repository-naming.md)  
CLI: [ADR-0005](https://github.com/xgic/ai/blob/main/docs/adr/0005-modular-xgic-cli-and-retirement-of-xde.md)

## Product

This repository is a **thin end-user Dev Container template**.

| Concern | Where it lives |
|---------|----------------|
| Image / Dockerfile / producer CI | https://github.com/xgic/payload-cms-dev |
| CLI framework | https://github.com/xgic/cli |
| Compose lifecycle (`xgic up` / `down` / `check`) | https://github.com/xgic/dev-cli |
| Payload commands (`xgic payload …`) | https://github.com/xgic/payload-cms-cli |

**Do not** add Dockerfile image builds or in-tree CLI packages here.

## Session startup (inside container)

1. `xgic --help`
2. `xgic check`
3. `xgic payload env`
4. Daily: `xgic payload dev`

## Rules

**Public GitHub writes:** Before `gh issue create|edit`, `gh pr create|edit`, or any public comment, complete the **mandatory public-safe draft gate** in https://github.com/xgic/ai/blob/main/docs/BASE-STANDARDS-FOR-ORCHESTRATED-REPOS.md (fictional placeholders only).

- Public-safe content only.
- Human UI review before merge to `main`.
- Conventional Commits; **labels required**.
- Prefer full `https://github.com/xgic/...` URLs.
- CLI changes → modular CLI repos; image changes → `payload-cms-dev`.
