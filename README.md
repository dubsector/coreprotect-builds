# coreprotect-builds

Automated builds of [CoreProtect](https://github.com/PlayPro/CoreProtect) with Community Edition restrictions removed.

## Releases

- **Stable** — built from the latest upstream tagged release
- **Dev** — built from upstream master, checked daily

## How it works

A GitHub Actions workflow runs daily, checks for upstream changes, applies patches to remove CE restrictions, and publishes a new release only if something changed.

## Security audit

Scanned with [zizmor](https://docs.zizmor.sh) v1.26.1 — **0 findings**.

The workflow is hardened as follows:

- All actions pinned to commit hashes (not mutable tags)
- Top-level `permissions: {}` deny-all, with least-privilege grants per job
- `persist-credentials: false` on all checkout steps
- No Maven dependency cache (eliminates cache-poisoning attack surface)
- No third-party release actions — uses the built-in `gh` CLI instead
- Template expressions passed via `env:` rather than inline in `run:` shells
