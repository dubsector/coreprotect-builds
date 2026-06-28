# coreprotect-builds

Automated builds of [CoreProtect](https://github.com/PlayPro/CoreProtect).

## Releases

- **Stable** — built from the latest upstream tagged release
- **Dev** — built from upstream master, checked daily

## How it works

A GitHub Actions workflow runs daily, checks for upstream changes, and publishes a new release only if something changed. Each build goes through Paper and Folia smoke tests before being published — the required Java version is detected automatically from the server version. If the plugin fails to load or logs errors on startup, the release is blocked.

## Security

The workflow is scanned on every push with [zizmor](https://docs.zizmor.sh). You can view the latest report under the **Security → Code scanning** tab of this repo.
