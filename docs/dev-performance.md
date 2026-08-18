# Dev performance (Windows Docker Desktop)

## Symptom

`pnpm install` and the first Payload `/admin` compile can be very slow when the
workspace is a **Windows path bind-mounted** into Docker Desktop (9p/VirtioFS).
`xgic payload dev` may report Ready while Turbopack is still walking the
module graph.

## Recommended long-term host

Run the project on a **native Linux filesystem** (Linux host, or a dedicated
development VM with the repo on that VM’s disk). Do not treat a Windows
bind mount as the production-minded default.

## Temporary volume bridge (this template)

Until the workspace lives on a native Linux filesystem, Compose mounts Linux
**named volumes** over the app-root module graph:

| Host-visible path | Container path | Volume |
|-------------------|----------------|--------|
| (named volume) | `/workspace/node_modules` | `xgic-payload-cms-dev-node-modules` |
| (named volume) | `/workspace/.next` | `xgic-payload-cms-dev-next` |

This is intentional and temporary. Ownership of those volumes is corrected
**only when** the mount is not already owned by uid `1000` (`node`).

After you recreate those volumes (or the first time they are empty):

```bash
pnpm install
```

App-root layout means the paths are `/workspace/node_modules` and
`/workspace/.next` — not a `website/` subdirectory.

## Credentials (not a performance workaround)

| File | Role |
|------|------|
| `.devcontainer/.env` | Compose interpolation (`POSTGRES_*`) + container env |
| repo-root `.env` (after setup) | Payload/Next (`DATABASE_URL`, secrets) |

After `xgic payload env --regenerate`, both files must agree, and a Postgres
volume initialized with an older password must be recreated (local data wipe).
CLI sync of those files is tracked in
[payload-cms-cli#26](https://github.com/xgic/payload-cms-cli/issues/26).

Do **not** teach application code to accept both `DATABASE_URI` and
`DATABASE_URL`.

## Related

- Template Compose-first reopen: [#10](https://github.com/xgic/payload-cms/issues/10)
- Producer consumer contract: [payload-cms-dev#50](https://github.com/xgic/payload-cms-dev/issues/50)
- Windows Git `safe.directory` / SSH agent: [#9](https://github.com/xgic/payload-cms/issues/9),
  [payload-cms-dev#49](https://github.com/xgic/payload-cms-dev/issues/49)
