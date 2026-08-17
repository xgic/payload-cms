# XGIC Payload CMS

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![Payload CMS](https://img.shields.io/badge/Payload%20CMS-3.x+-000000?logo=payloadcms&logoColor=white)](https://payloadcms.com)
[![Dev Containers](https://img.shields.io/badge/Dev_Containers-ready-blue?logo=visualstudiocode)](https://containers.dev/)
[![Producer release](https://img.shields.io/github/v/release/xgic/payload-cms-dev?label=payload-cms-dev&logo=github)](https://github.com/xgic/payload-cms-dev/releases)
[![GHCR image](https://img.shields.io/badge/GHCR-payload--cms--dev-blue?logo=github)](https://github.com/users/xgic/packages/container/package/payload-cms-dev)
[![Use this template](https://img.shields.io/badge/GitHub-Use_this_template-24292f?logo=github)](https://github.com/xgic/payload-cms/generate)

## The optimal way to start Payload CMS projects

**For humans and AI coding assistants.**

This repository is XGIC’s **recommended starting point** for new [Payload CMS](https://payloadcms.com) applications. It gives you a **reproducible Dev Container**, a **pinned multi-arch environment image**, and a **single CLI brand**—so people and agents share the same, documented operations instead of fighting host toolchains and ad-hoc scripts.

| You want… | You get… |
|-----------|----------|
| A clean app repository on day one | **Use this template** → your product remote, not a fork of image-build history |
| Minutes to a working workspace | Pull `ghcr.io/xgic/payload-cms-dev` · **Reopen in Container** · run `xgic` |
| The same path for AI and humans | Modular **XGIC CLI** (`xgic` / `xgic payload …`) + [AGENTS.md](AGENTS.md) |
| Long-horizon maintainability | Image evolution in the producer; app code stays thin and focused |

```text
ghcr.io/xgic/payload-cms-dev:0.3.1
```

Image producer and CI: **[xgic/payload-cms-dev](https://github.com/xgic/payload-cms-dev)** · Multi-repo standards: **[xgic/ai](https://github.com/xgic/ai)**

---

## Quick start

Minimal path (details below):

1. **[Use this template](https://github.com/xgic/payload-cms/generate)** → create and clone **your** repository.  
2. Open the folder in **VS Code** → **Dev Containers: Reopen in Container**.  
3. In the container terminal:

```bash
xgic --version
xgic check
xgic up --profile postgres   # when your stack needs Compose Postgres
xgic payload env
xgic payload dev
```

**Full walkthrough (all options, troubleshooting, AI prompts):** [Step-by-step: start a project](#step-by-step-start-a-payload-cms-project-with-this-template)

---

## Vision

Modern CMS work fails more often from **environment drift** than from product ideas. Teams reinstall Node toolchains, disagree on database versions, and paste brittle shell recipes into AI chats. XGIC’s approach is different:

1. **One published environment** — versioned on GHCR, reviewed and CI-gated in the producer repository.  
2. **One thin template** — this repository: app-focused extensions and a pinned image.  
3. **One CLI brand** — **XGIC CLI** for lifecycle and Payload operations, designed for **humans and agents**.  

The result is a professional, open-source path to **reproducible Payload CMS development**: pull an image, open a container, run a small set of documented commands.

---

## Why start here (not from a blank machine)

| Benefit | Detail |
|---------|--------|
| **Fastest path to a working workspace** | Pre-built image; no multi-stage Dockerfile rebuild in every app repo |
| **Reproducible pins** | Semver image tags (e.g. `0.3.0`) match producer releases |
| **AI-operable** | Stable command surface in [AGENTS.md](AGENTS.md); agents use `xgic` instead of inventing scripts |
| **Clear ownership** | App code lives in *your* repo; image improvements land in [payload-cms-dev](https://github.com/xgic/payload-cms-dev); CLI logic in modular packages |
| **Open-source rigor** | Apache-2.0, CODEOWNERS, public-safe docs, human-reviewed PRs |

---

## Prerequisites

| Tool | Notes |
|------|--------|
| [Docker Desktop](https://www.docker.com/products/docker-desktop) or Docker Engine | Required for Dev Containers |
| [Visual Studio Code](https://code.visualstudio.com/) | Or a Dev Containers–compatible editor |
| [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) | VS Code marketplace |
| GitHub account | For **Use this template** |

Optional: [GitHub CLI](https://cli.github.com/) (`gh`) if you prefer creating the repo from the terminal.

---

## Step-by-step: start a Payload CMS project with this template

### Option A — GitHub “Use this template” (recommended)

#### 1. Create your repository

1. Open **[https://github.com/xgic/payload-cms](https://github.com/xgic/payload-cms)**.  
2. Click **Use this template** → **Create a new repository**.  
3. Choose owner, name (e.g. `my-payload-app`), and visibility.  
4. Create the repository (do **not** needlessly add an extra “include all branches” unless you know you need it).

#### 2. Clone your new repository

```bash
git clone https://github.com/<you>/<your-repo>.git
cd <your-repo>
```

#### 3. Open in VS Code and enter the Dev Container

```bash
code .
```

When prompted, choose **Reopen in Container**, or run:

**Dev Containers: Reopen in Container** from the Command Palette  
(<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> / <kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd>).

VS Code will **pull** `ghcr.io/xgic/payload-cms-dev:0.3.1` (first pull may take several minutes).

#### 4. Configure and scaffold (first session — explicit CLI)

This template ships configuration for `xgic payload` under `.devcontainer/`:

| File | Role |
|------|------|
| `create-payload-config.json` | `layout: app-root`, `projectDir: "."`, template, DB adapter |
| `create-payload-config.schema.json` | IntelliSense / validation |
| `docker-compose.yml` | Local Compose shape (DB profiles + optional app service image) |

**Layout:** this template scaffolds the Payload + Next.js app at the **repository root** (Payload/Next.js best practice). The image producer repo uses a gitignored `app/` directory instead — do not copy that pattern here.

In the integrated terminal **inside** the container:

```bash
xgic --version
xgic check

# Create .devcontainer/.env with fresh local credentials (required once)
xgic payload env --regenerate --yes
xgic payload env

# Scaffold the Payload app at repo root (non-silent; fails loudly)
xgic payload setup
```

You should see modular XGIC CLI output and a successful project create (or a clear error). Setup is **not** auto-run on container start.

#### 5. Start Payload development

```bash
# Bring up Compose DB sidecars when using postgres/mongodb profiles:
xgic up --profile postgres

# Primary daily command — smart start for the Payload app
xgic payload dev
```

Open the app URL reported by the process (commonly port **3000**; this template forwards `3000`).

#### 6. Work in your application repository

- Commit **your** Payload application code to **your** repository.  
- Keep this template’s Dev Container pin intentional (see [Image pins](#image-pins)).  
- Open PRs with human review before merging to your default branch.  
- Do **not** commit production secrets, private hosts, or deploy credentials in this public template.

---

### Option B — Clone this template repository directly

Use when you are improving the template itself or exploring without “Use this template”:

```bash
git clone https://github.com/xgic/payload-cms.git
cd payload-cms
code .
# Dev Containers: Reopen in Container
```

For a **new product**, Option A is preferred so your git remote is already *your* project.

---

### Option C — GitHub CLI

```bash
gh repo create <you>/<your-repo> --template xgic/payload-cms --public --clone
cd <your-repo>
code .
# Dev Containers: Reopen in Container
```

---

## Image pins

`.devcontainer/devcontainer.json` currently pins:

```text
ghcr.io/xgic/payload-cms-dev:0.3.1
```

| Tag | Use when |
|-----|----------|
| `:0.3.1` (semver) | **Default for app work** — matches producer [v0.3.1](https://github.com/xgic/payload-cms-dev/releases/tag/v0.3.1) |
| `:latest` / `:main` | You deliberately want rolling producer `main` (less reproducible) |

```bash
docker pull ghcr.io/xgic/payload-cms-dev:0.3.1
```

To change the pin, edit the `image` field in `.devcontainer/devcontainer.json`, commit, and reopen/rebuild the container.

If a tag is missing, check [producer releases](https://github.com/xgic/payload-cms-dev/releases) or contribute to the image in [payload-cms-dev](https://github.com/xgic/payload-cms-dev).

---

## XGIC CLI: optimize Payload development (humans and AI)

The image installs modular **XGIC CLI** packages. Living docs use the **`xgic` brand only** (no supported dual brand).

### Command map

| Goal | Command |
|------|---------|
| Help / version | `xgic --help` · `xgic --version` |
| Health / diagnostics | `xgic check` · `xgic info` · `xgic env` |
| Compose up / down | `xgic up` · `xgic down` (add `--profile postgres` when needed) |
| Logs / shell | `xgic logs` · `xgic shell` |
| Payload env status | `xgic payload env` |
| Regenerate local env secrets | `xgic payload env --regenerate --yes` |
| Ensure project scaffold | `xgic payload setup` (**explicit**; uses `.devcontainer/create-payload-config.json`) |
| **Daily app start** | **`xgic payload dev`** |
| Schema helper | `xgic payload schema` |
| Reset project + DB volume | `xgic payload reset --dry-run` then `--yes` |

Destructive commands support **dry-run first**—use it.

### Recommended daily loop (human)

```bash
xgic check
xgic up --profile postgres   # if required for your stack
xgic payload env
xgic payload dev
# edit collections, admin UI, APIs...
# commit in your app repo
xgic down                    # when finished for the day
```

### Recommended session loop (AI coding assistants)

Instruct agents to **read [AGENTS.md](AGENTS.md) first**, then operate only through documented `xgic` commands.

**High-signal prompts**

1. “Read AGENTS.md. Run `xgic check` and summarize any failures.”  
2. “Run `xgic payload env` (no secret values). Confirm whether we should `xgic up --profile postgres`.”  
3. “Start the app with `xgic payload dev` and report the listening URL/port.”  
4. “Before resetting anything, run `xgic payload reset --dry-run` and list what would be removed.”  
5. “Do not invent Make targets or host-global Node installs; use XGIC CLI only.”  

**What agents must not do**

- Rebuild or publish the producer image from this template (use [payload-cms-dev](https://github.com/xgic/payload-cms-dev)).  
- Implement new `xgic` subcommands here (use [payload-cms-cli](https://github.com/xgic/payload-cms-cli) / [dev-cli](https://github.com/xgic/dev-cli) / [cli](https://github.com/xgic/cli)).  
- Put private hosts, tokens, or internal tracker IDs in public issues/PRs ([BASE-STANDARDS](https://github.com/xgic/ai/blob/main/docs/BASE-STANDARDS-FOR-ORCHESTRATED-REPOS.md)).

### Optional host install (diagnostics only)

Prefer the Dev Container. For host-side CLI experiments:

```bash
uv venv .venv
# Windows: .venv\Scripts\activate
# Unix:    source .venv/bin/activate
uv pip install \
  "xgic-cli>=0.2.0,<0.3" \
  "xgic-dev-cli>=0.2.0,<0.3" \
  "xgic-payload-cms-cli>=0.2.0,<0.3"
xgic --version
```

Publishing policy for those packages: [python-package-release.md](https://github.com/xgic/ai/blob/main/docs/python-package-release.md).

---

## Architecture

This template is the **application-facing** entry in XGIC’s dual-repo Dev Container model: a thin consumer of a published image—not an image builder.

```text
You (human or AI)
    │
    ▼
xgic/payload-cms  ──image:──►  ghcr.io/xgic/payload-cms-dev
    │                                    ▲
    │                                    │ builds / publishes
    │                           xgic/payload-cms-dev
    │
    └── inside container: xgic · xgic payload · pnpm · node · db clients
```

| Repository | Role |
|------------|------|
| [xgic/payload-cms-dev](https://github.com/xgic/payload-cms-dev) | **Producer** (`*-dev`): Dockerfile, Compose, CI, publishes `ghcr.io/xgic/payload-cms-dev` |
| **This repo** — [xgic/payload-cms](https://github.com/xgic/payload-cms) | **Template**: thin `devcontainer.json`, app-focused extensions, docs for application teams |

| CLI package | Role |
|-------------|------|
| [xgic/cli](https://github.com/xgic/cli) | Thin core + `xgic` entrypoint |
| [xgic/dev-cli](https://github.com/xgic/dev-cli) | Compose lifecycle: `xgic up` / `down` / `check` / … |
| [xgic/payload-cms-cli](https://github.com/xgic/payload-cms-cli) | Product commands: `xgic payload …` |

---

## XGIC standards

Portfolio rules that govern this project (and how it relates to the producer and CLI modules):

| Topic | Document |
|-------|----------|
| Dual-repo naming (`*-dev` producer vs clean template) | [ADR-0001](https://github.com/xgic/ai/blob/main/docs/adr/0001-xgic-gitlab-architecture-and-repository-naming.md) |
| Modular XGIC CLI; no supported dual brand | [ADR-0005](https://github.com/xgic/ai/blob/main/docs/adr/0005-modular-xgic-cli-and-retirement-of-xde.md) |
| Public-safe docs, PR process, quality attributes | [BASE-STANDARDS](https://github.com/xgic/ai/blob/main/docs/BASE-STANDARDS-FOR-ORCHESTRATED-REPOS.md) |
| Component catalog | [Ecosystem catalog](https://github.com/xgic/ai/blob/main/docs/ecosystem/catalog.md) |
| Community health (CODEOWNERS, security norms) | [Community health](https://github.com/xgic/ai/blob/main/docs/community-health.md) |
| Agent instructions for this template | [AGENTS.md](AGENTS.md) |

Hub home: [https://github.com/xgic/ai](https://github.com/xgic/ai)

---

## App-focused VS Code extensions

This template installs a **minimal, domain-focused** set (Payload / TypeScript / GraphQL / data)—not the full producer infra set:

| Extension | Purpose |
|-----------|---------|
| Tailwind CSS IntelliSense | Admin UI styling workflows |
| npm IntelliSense | Package imports |
| ESLint / Prettier | Quality and formatting |
| GraphQL | API development |
| TypeScript (Next) | Language service |
| SQLTools + PostgreSQL driver | Database exploration |
| Code Spell Checker / ErrorLens | Clarity while coding |

Docker-heavy tooling lives primarily on the **producer** for contributors who edit Dockerfiles—see [payload-cms-dev](https://github.com/xgic/payload-cms-dev).

---

## Troubleshooting

| Symptom | What to try |
|---------|-------------|
| Image pull fails | Confirm Docker is running; `docker pull ghcr.io/xgic/payload-cms-dev:0.3.1`; check [package page](https://github.com/users/xgic/packages/container/package/payload-cms-dev) |
| `xgic: command not found` in a one-off `docker run` | Use a **non-login** shell so image `PATH` is preserved, or open via Dev Containers (recommended) |
| Need a clean project/DB | `xgic payload reset --dry-run` then `--yes` only after review |
| Image definition bug | File an issue or PR on [payload-cms-dev](https://github.com/xgic/payload-cms-dev), not only in your app repo |
| CLI behavior bug | File on the relevant modular CLI repository |

Rebuild guidance (rare for this template—you usually **re-pull** the image):

- **Reopen in Container** after pin changes  
- Producer contributors use **Rebuild Without Cache** when editing the Dockerfile  

---

## Contributing to *this* template

Improvements to **template docs**, **image pin**, or **app-focused extensions** belong here.

1. Branch from `main`, Conventional Commits, **labels required**.  
2. PR with human UI review (agents draft; humans merge).  
3. See [CONTRIBUTING.md](CONTRIBUTING.md) and [AGENTS.md](AGENTS.md).

---

## License

Copyright 2026 XGIC.  
Licensed under the [Apache License, Version 2.0](LICENSE).  
See [NOTICE](NOTICE).

---

**XGIC** — Principal architecture for open-source developer platforms: modular CLI, dual-repo Dev Containers, and workflows that stay operable for both people and AI.
