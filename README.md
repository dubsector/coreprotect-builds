# coreprotect-builds

[![Build](https://github.com/dubsector/coreprotect-builds/actions/workflows/build.yml/badge.svg)](https://github.com/dubsector/coreprotect-builds/actions/workflows/build.yml)
[![Zizmor](https://github.com/dubsector/coreprotect-builds/actions/workflows/zizmor.yml/badge.svg)](https://github.com/dubsector/coreprotect-builds/actions/workflows/zizmor.yml)
[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/dubsector/coreprotect-builds/badge)](https://securityscorecards.dev/viewer/?uri=github.com/dubsector/coreprotect-builds)
[![Security Policy](https://img.shields.io/badge/Security-Policy-green)](SECURITY.md)
[![Dependabot](https://img.shields.io/badge/Dependabot-enabled-025E8C?logo=dependabot)](https://github.com/dubsector/coreprotect-builds/network/updates)

Automated builds of [CoreProtect](https://github.com/PlayPro/CoreProtect) compiled from source.

## Support PlayPro

These builds patch out the donation-key check (`validDonationKey()`) so the plugin runs without one. That check exists because PlayPro relies on donations to keep developing CoreProtect — if you're getting value out of these builds, please consider supporting them directly:

- [Patreon](https://www.patreon.com/coreprotect)
- [Donation keys](https://coreprotect.net/donate/)

## Releases

- **Stable** — built from the latest upstream tagged release
- **Dev** — built from upstream master, checked daily

## How it works

1. **Check** — polls upstream daily; compares latest master commit and latest release tag against existing releases
2. **Build** — compiles from source using JDK 25
3. **Smoke test** — spins up a Paper and Folia server and verifies CoreProtect loads without errors (Java version auto-detected from the server JAR)
4. **Publish** — only if both smoke tests pass; stable and dev are published as separate releases

Stable releases are tagged `stable-{tag}` and dev releases are tagged `dev-{short_sha}`.

## Verifying releases

Every JAR is signed with [Sigstore](https://sigstore.dev) and includes a [SLSA provenance attestation](https://slsa.dev). You can verify before using:

```sh
# Verify SLSA provenance attestation via GitHub CLI
gh attestation verify CoreProtect-<version>.jar --repo dubsector/coreprotect-builds

# Verify cosign bundle
cosign verify-blob CoreProtect-<version>.jar \
  --bundle CoreProtect-<version>.jar.sigstore.json
```

Both the `.sigstore.json` bundle and `.intoto.jsonl` provenance file are attached to every release.

## Security

- Workflow YAML is scanned on every push with [zizmor](https://docs.zizmor.sh) — view reports under **Security → Code scanning**
- All GitHub Actions are pinned to exact commit SHAs
- Least-privilege permissions on every job (`permissions: {}` at workflow level)
- Dependencies kept current via [Dependabot](https://docs.github.com/en/code-security/dependabot)
- Supply chain posture tracked by [OpenSSF Scorecard](https://securityscorecards.dev/viewer/?uri=github.com/dubsector/coreprotect-builds)

To report a security issue see [SECURITY.md](SECURITY.md).

## License

This repository contains build automation scripts for CoreProtect. The compiled binaries distributed here are a Modified Version of [CoreProtect](https://github.com/PlayPro/CoreProtect) (see [Support PlayPro](#support-playpro) above for the specific change), copyright the PlayPro contributors, distributed under the terms of the [Artistic License 2.0](LICENSE). See the upstream repository for the original source.
