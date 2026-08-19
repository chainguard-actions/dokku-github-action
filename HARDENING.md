<!-- markdownlint-disable -->

# Hardening Report: dokku--github-action/v1.7.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **dokku--github-action/v1.7.0** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All 6 `uses:` references in build.yaml use mutable version tags instead of full 40-character SHA commit hashes, making the workflow vulnerable to supply-chain attacks if any of those action tags are moved or compromised. Unpinned references: `actions/checkout@v4`, `docker/metadata-action@v5`, `docker/setup-qemu-action@v3`, `docker/setup-buildx-action@v3`, `docker/login-action@v3`, `docker/build-push-action@v6`.

Locations:

- `.github/workflows/build.yaml:15`
- `.github/workflows/build.yaml:20`
- `.github/workflows/build.yaml:30`
- `.github/workflows/build.yaml:32`
- `.github/workflows/build.yaml:36`
- `.github/workflows/build.yaml:41`

### unpinned-uses (severity: high)

Three `uses:` references in lint.yaml use the mutable tag `@v4` instead of a full 40-character SHA commit hash. The `actions/checkout@v4` step appears in all three jobs (hadolint, markdown-lint, yamllint) and is unpinned. The other three actions in this file are correctly SHA-pinned.

Locations:

- `.github/workflows/lint.yaml:18`
- `.github/workflows/lint.yaml:28`
- `.github/workflows/lint.yaml:40`

### missing-permissions (severity: medium)

build.yaml has no top-level `permissions:` key and none of its jobs define a `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary.

Locations:

- `.github/workflows/build.yaml:1`

### missing-permissions (severity: medium)

lint.yaml has no top-level `permissions:` key and none of its jobs (hadolint, markdown-lint, yamllint) define a `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary.

Locations:

- `.github/workflows/lint.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 4 findings across build.yaml and lint.yaml:

1. build.yaml - Pinned all 6 unpinned action references to full 40-char commit SHAs:
   - actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262
   - docker/metadata-action@v5 → @c299e40c65443455700f0fdfc63efafe5b349051
   - docker/setup-qemu-action@v3 → @c7c53464625b32c7a7e944ae62b3e17d2b600130
   - docker/setup-buildx-action@v3 → @8d2750c68a42422c14e847fe6c8ac0403b4cbd6f
   - docker/login-action@v3 → @c94ce9fb468520275223c153574b00df6fe4bcc9
   - docker/build-push-action@v6 → @10e90e3645eae34f1e60eeb005ba3a3d33f178e8

2. build.yaml - Added top-level `permissions: {}` block.

3. lint.yaml - Pinned all 3 unpinned actions/checkout@v4 references to @11d5960a326750d5838078e36cf38b85af677262 (the other 3 actions were already SHA-pinned).

4. lint.yaml - Added top-level `permissions: {}` block.

