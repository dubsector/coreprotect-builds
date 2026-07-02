# Patches

Source-level modifications applied to the upstream [CoreProtect](https://github.com/PlayPro/CoreProtect) checkout at build time. The build workflow fetches the patch for the exact commit it's running from and applies it with `git apply`; if it fails to apply cleanly (e.g. upstream moved the relevant code), the build fails rather than silently shipping an unmodified jar.

## `unlock-community-edition.patch`

Forces `VersionUtils.isCommunityEdition()` to return `false`, which unlocks the `auto-purge` config option that upstream otherwise gates behind a donation key, and marks the build's `project.branch` as `patched`. This is the entire diff from upstream — see the repository [README](../README.md#modifications) for context and the [Support PlayPro](../README.md#support-playpro) section for how to support the upstream developers.
