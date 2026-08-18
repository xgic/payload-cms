# Repository settings (template)

Public operational notes for maintainers of [xgic/payload-cms](https://github.com/xgic/payload-cms).

## Branch protection

`main` is protected via a repository **ruleset** (mirrors XGIC producer norms where applicable):

| Rule | Intent |
|------|--------|
| No force-push / no deletion of `main` | History integrity |
| Pull request required (1 approval) | Human UI review |
| Linear history | Clean default branch |
| Required signatures | Verified commits |
| Required status check **Lint** | JSON + Docker Compose-first contract (no standalone `image`, pin on Docker Compose service) |

Image build status checks live on [payload-cms-dev](https://github.com/xgic/payload-cms-dev) (Lint / Test / Release Validation).

## Labels

Apply PR labels consistently (`documentation`, `bug`, `enhancement`, `chore`, …). Create additional labels as needed to match producer taxonomy.

## Related

- [AGENTS.md](../AGENTS.md)
- [CONTRIBUTING.md](../CONTRIBUTING.md)
- [xgic/ai BASE-STANDARDS](https://github.com/xgic/ai/blob/main/docs/BASE-STANDARDS-FOR-ORCHESTRATED-REPOS.md)
- [README standards (hub)](https://github.com/xgic/ai/blob/main/docs/readme-standards.md)
