# XGIC Payload CMS (template)

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![Payload CMS](https://img.shields.io/badge/Payload%20CMS-3.x+-000000?logo=payloadcms&logoColor=white)](https://payloadcms.com)

> **Official XGIC end-user template** — thin VS Code Dev Container consumer of the published image  
> [`ghcr.io/xgic/payload-cms-dev`](https://github.com/xgic/payload-cms-dev/pkgs/container/payload-cms-dev).

This repository is the **application-facing** template ([ADR-0001](https://github.com/xgic/ai/blob/main/docs/adr/0001-xgic-gitlab-architecture-and-repository-naming.md) clean template).  
Image build, Dockerfile, and producer CI live in **[xgic/payload-cms-dev](https://github.com/xgic/payload-cms-dev)**.

## Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop) or Docker Engine
- [Visual Studio Code](https://code.visualstudio.com/)
- [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension

## Quick start

1. Use this repository as a **GitHub Template** (or clone it).
2. Open the folder in VS Code and **Reopen in Container**.
3. Inside the container:

```bash
xgic --version
xgic check
xgic payload env
xgic payload dev
```

## Architecture

| Layer | Repository |
|-------|------------|
| Dev Container **image producer** (`*-dev`) | [xgic/payload-cms-dev](https://github.com/xgic/payload-cms-dev) |
| **This template** (end user) | [xgic/payload-cms](https://github.com/xgic/payload-cms) |
| XGIC CLI core | [xgic/cli](https://github.com/xgic/cli) |
| Dev lifecycle CLI | [xgic/dev-cli](https://github.com/xgic/dev-cli) |
| Payload product CLI | [xgic/payload-cms-cli](https://github.com/xgic/payload-cms-cli) |

CLI brand: **XGIC CLI** (`xgic`) only — see [ADR-0005](https://github.com/xgic/ai/blob/main/docs/adr/0005-modular-xgic-cli-and-retirement-of-xde.md).

## Image pin

`.devcontainer/devcontainer.json` references:

```text
ghcr.io/xgic/payload-cms-dev:latest
```

Prefer a **semver pin** for production-like reproducibility once tags are published. Until the first GHCR release is available, use the producer repository’s local Dev Container build path documented in [payload-cms-dev](https://github.com/xgic/payload-cms-dev).

## Multi-repo standards

- https://github.com/xgic/ai  
- Agent notes: [AGENTS.md](AGENTS.md)

## License

Apache-2.0 — see [LICENSE](LICENSE).
