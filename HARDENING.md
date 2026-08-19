<!-- markdownlint-disable -->

# Hardening Report: dokku--github-action/v1.6.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **dokku--github-action/v1.6.1** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple `uses:` references in .github/workflows/build.yaml are pinned to mutable version tags instead of full 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if those tags are moved. Failing references: `actions/checkout@v4` (line 17), `docker/metadata-action@v5` (line 21), `docker/setup-qemu-action@v3` (line 33), `docker/setup-buildx-action@v3` (line 34), `docker/login-action@v3` (line 38), `docker/build-push-action@v6` (line 43).

Locations:

- `.github/workflows/build.yaml:17`
- `.github/workflows/build.yaml:21`
- `.github/workflows/build.yaml:33`
- `.github/workflows/build.yaml:34`
- `.github/workflows/build.yaml:38`
- `.github/workflows/build.yaml:43`

### unpinned-uses (severity: high)

Three `uses:` references in .github/workflows/lint.yaml are pinned to the mutable tag `@v4` instead of a full 40-character commit SHA. Failing references: `actions/checkout@v4` (lines 18, 27, 36). The other three actions in this file are correctly SHA-pinned.

Locations:

- `.github/workflows/lint.yaml:18`
- `.github/workflows/lint.yaml:27`
- `.github/workflows/lint.yaml:36`

### missing-permissions (severity: medium)

.github/workflows/build.yaml has no top-level `permissions:` key and no job-level `permissions:` key on the `docker` job. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary.

Locations:

- `.github/workflows/build.yaml:1`

### missing-permissions (severity: medium)

.github/workflows/lint.yaml has no top-level `permissions:` key and no job-level `permissions:` key on any of its three jobs (`hadolint`, `markdown-lint`, `yamllint`). Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary.

Locations:

- `.github/workflows/lint.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 4 findings across both workflow files:

build.yaml:
- Pinned actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 # v4
- Pinned docker/metadata-action@v5 → @c299e40c65443455700f0fdfc63efafe5b349051 # v5
- Pinned docker/setup-qemu-action@v3 → @c7c53464625b32c7a7e944ae62b3e17d2b600130 # v3
- Pinned docker/setup-buildx-action@v3 → @8d2750c68a42422c14e847fe6c8ac0403b4cbd6f # v3
- Pinned docker/login-action@v3 → @c94ce9fb468520275223c153574b00df6fe4bcc9 # v3
- Pinned docker/build-push-action@v6 → @10e90e3645eae34f1e60eeb005ba3a3d33f178e8 # v6
- Added top-level `permissions: contents: read`

lint.yaml:
- Pinned all three actions/checkout@v4 references → @11d5960a326750d5838078e36cf38b85af677262 # v4
- Added top-level `permissions: contents: read`
- Left the already-SHA-pinned brpaz/hadolint-action, avto-dev/markdown-lint, and ibiqlik/action-yamllint references unchanged

