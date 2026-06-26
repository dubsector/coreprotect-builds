# coreprotect-builds

Automated builds of [CoreProtect](https://github.com/PlayPro/CoreProtect) with Community Edition restrictions removed.

## Releases

- **Stable** — built from the latest upstream tagged release
- **Dev** — built from upstream master, checked daily

## How it works

A GitHub Actions workflow runs daily, checks for upstream changes, applies patches to remove CE restrictions, and publishes a new release only if something changed.
