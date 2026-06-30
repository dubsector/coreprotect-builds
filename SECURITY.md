# Security Policy

## Reporting a Vulnerability

This repository contains automated build workflows and does not ship production code of its own.
If you discover a security issue in the **build pipeline or release process** (e.g. a supply-chain risk, a compromised action, or an issue with how artifacts are signed/attested), please report it privately:

- Open a [GitHub Security Advisory](https://github.com/dubsector/coreprotect-builds/security/advisories/new) in this repository.

For vulnerabilities in **CoreProtect itself**, please report upstream to the [PlayPro/CoreProtect](https://github.com/PlayPro/CoreProtect) project.

## Verifying Release Artifacts

Every JAR published by this repository is signed with [Sigstore](https://sigstore.dev) and includes a build provenance attestation.

**Verify with the GitHub CLI:**
```sh
gh attestation verify CoreProtect-<version>.jar --repo dubsector/coreprotect-builds
```

**Verify the cosign bundle:**
```sh
cosign verify-blob CoreProtect-<version>.jar --bundle CoreProtect-<version>.jar.sigstore.json
```

The `.intoto.jsonl` provenance file attached to each release can be inspected to confirm the exact workflow run, commit SHA, and repository that produced the artifact.
