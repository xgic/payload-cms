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
| Docker Compose lifecycle (`xgic up` / `down` / `check`) | https://github.com/xgic/dev-cli |
| Payload commands (`xgic payload …`) | https://github.com/xgic/payload-cms-cli |

**Do not** add Dockerfile image builds or in-tree CLI packages here.

## Docker Compose-first reopen

Supported attach path is **Docker Compose**, not a standalone `image` in `devcontainer.json`.

- `dockerComposeFile`: `.devcontainer/docker-compose.yml`
- Service: `xgic-payload-cms-dev`
- Workspace: `/workspace` · `remoteUser`: `node`
- Image pin: `image: ghcr.io/xgic/payload-cms-dev:0.3.3` on the Docker Compose service
- Default project: `name: xgic-payload-cms-dev` plus env `XGIC_COMPOSE_PROJECT` / `XGIC_COMPOSE_FILE` / `XGIC_PRIMARY_SERVICE`
- Postgres starts with Reopen (`runServices` + `depends_on` health). Mongo remains `--profile mongodb`.

Consumers who fork or rename must update Docker Compose `name:`, container/volume/network names, the `XGIC_*` env, and `composeProjectName` together.

Standalone `image` reopen produces non-deterministic container names (Docker’s default `adjective_noun` style) and detaches the DB from the IDE project. Rebuild once if a workspace is still on that anti-pattern.

## Session startup (inside container)

1. `xgic --help`
2. `xgic check`
3. Edit `.devcontainer/create-payload-config.json` if needed (`projectName`, `template`, `dbAdapter`; keep `layout: app-root` / `projectDir: "."`; keep `composeProjectName` aligned with Docker Compose `name:`)
4. `xgic payload env --regenerate --yes` when `.devcontainer/.env` is missing
5. `xgic payload setup` — app-root scaffold (Payload/Next at repo root)
6. After named-volume recreate: `pnpm install` (see [docs/dev-performance.md](docs/dev-performance.md))
7. Daily: `xgic payload dev` (requires setup first)

Git DX is Compose-start only (chown `ssh-home` → `configure-git-dx.sh --quiet`; failure is non-fatal). Prefer HTTPS + VS Code host credential helper. Optional SSH agent overlay: `.devcontainer/docker-compose.git-dx.yml` (Docker Desktop sock only — never on plain Linux Engine). **Do not** reintroduce host `initializeCommand` / `postStartCommand` hooks. Production deploy details never belong in this public repo.

Do **not** dual-support `DATABASE_URI` in app code. Credential regenerate / `DATABASE_URL` sync is [payload-cms-cli#26](https://github.com/xgic/payload-cms-cli/issues/26). Producer contract: [payload-cms-dev#50](https://github.com/xgic/payload-cms-dev/issues/50). This reopen fix: [#10](https://github.com/xgic/payload-cms/issues/10).

## Rules

**Public GitHub writes:** Before `gh issue create|edit`, `gh pr create|edit`, or any public comment, complete the **mandatory public-safe draft gate** in https://github.com/xgic/ai/blob/main/docs/BASE-STANDARDS-FOR-ORCHESTRATED-REPOS.md (fictional placeholders only).

- Public-safe content only.
- Human UI review before merge to `main`.
- Conventional Commits; **labels required**.
- Prefer full `https://github.com/xgic/...` URLs.
- CLI changes → modular CLI repos; image changes → `payload-cms-dev`.
