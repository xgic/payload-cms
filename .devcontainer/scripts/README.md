# Git DX helpers (Compose start)

Copied from the producer exemplar
[xgic/payload-cms-dev](https://github.com/xgic/payload-cms-dev)
(`.devcontainer/scripts/`). Keep behavior in sync when the producer
changes Git DX.

- `configure-git-dx.sh` — host-conditional `safe.directory`, GitHub
  `known_hosts`, HTTPS prefer by default
- `align_docker_sock_gid.py` — match the image `docker` group to the
  engine socket GID
- `lib/` — shared logging and mount detection

Invoked once from the Compose primary `command` (not from
`devcontainer.json` lifecycle hooks). Failure is non-fatal so keep-alive
still starts.

Optional SSH agent overlay (Docker Desktop sock only):
`../docker-compose.git-dx.yml`.
