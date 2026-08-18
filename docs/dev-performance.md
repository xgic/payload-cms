# Dev performance (bind-mounted workspaces)

## Symptom

`pnpm install` and the first Payload `/admin` compile can be very slow when the
workspace is **bind-mounted** from the Docker host into the Dev Container and
that host filesystem has high latency for large Node module graphs.
`xgic payload dev` may report Ready while Turbopack is still walking the
module graph.

This template supports **Windows and Linux Docker hosts equally**. Named volumes
below improve DX on either host whenever bind-mount I/O dominates.

## Named volumes for the module graph

Docker Compose mounts **named volumes** over the app-root module graph so
Turbopack and package installs use container-native storage while application
source stays on the workspace bind mount:

| Host-visible path | Container path | Volume |
|-------------------|----------------|--------|
| (named volume) | `/workspace/node_modules` | `xgic-payload-cms-dev-node-modules` |
| (named volume) | `/workspace/.next` | `xgic-payload-cms-dev-next` |

Ownership of those volumes is corrected **only when** the mount is not already
owned by uid `1000` (`node`).

After you recreate those volumes (or the first time they are empty):

```bash
pnpm install
```

App-root layout means the paths are `/workspace/node_modules` and
`/workspace/.next` — not a `website/` subdirectory.

## Credentials (not a performance workaround)

| File | Role |
|------|------|
| `.devcontainer/.env` | Docker Compose interpolation (`POSTGRES_*`) + container env |
| repo-root `.env` (after setup) | Payload/Next (`DATABASE_URL`, secrets) |

After `xgic payload env --regenerate`, both files must agree, and a Postgres
volume initialized with an older password must be recreated (local data wipe).
CLI sync of those files is tracked in
[payload-cms-cli#26](https://github.com/xgic/payload-cms-cli/issues/26).

Do **not** teach application code to accept both `DATABASE_URI` and
`DATABASE_URL`.

## Related

- Template Docker Compose-first reopen: [#10](https://github.com/xgic/payload-cms/issues/10)
- Producer consumer contract: [payload-cms-dev#50](https://github.com/xgic/payload-cms-dev/issues/50)
- Host-conditional Git `safe.directory` / SSH agent: [#9](https://github.com/xgic/payload-cms/issues/9),
  [payload-cms-dev#49](https://github.com/xgic/payload-cms-dev/issues/49)
