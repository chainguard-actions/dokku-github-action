<!-- markdownlint-disable -->

# Hardening Report: dokku--github-action/v1.8.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **dokku--github-action/v1.8.0** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All action references in build.yaml use mutable version tags instead of full 40-character SHA commit pins, making the workflow vulnerable to supply-chain attacks if a tag is moved. Unpinned references: `actions/checkout@v5` (line 17), `docker/metadata-action@v5` (line 21), `docker/setup-qemu-action@v3` (line 32), `docker/setup-buildx-action@v3` (line 33), `docker/login-action@v3` (line 37), `docker/build-push-action@v6` (line 42).

Locations:

- `.github/workflows/build.yaml:17`
- `.github/workflows/build.yaml:21`
- `.github/workflows/build.yaml:32`
- `.github/workflows/build.yaml:33`
- `.github/workflows/build.yaml:37`
- `.github/workflows/build.yaml:42`

### unpinned-uses (severity: high)

Several action references in lint.yaml use mutable version tags instead of full 40-character SHA commit pins. Unpinned references: `actions/checkout@v5` (lines 19, 28, 35). Note: brpaz/hadolint-action, avto-dev/markdown-lint, and ibiqlik/action-yamllint are correctly pinned to full SHAs.

Locations:

- `.github/workflows/lint.yaml:19`
- `.github/workflows/lint.yaml:28`
- `.github/workflows/lint.yaml:35`

### missing-permissions (severity: medium)

build.yaml has no top-level `permissions:` key and none of its jobs define job-level permissions. Without explicit permissions, the workflow runs with the default (potentially broad) GITHUB_TOKEN permissions, which may include write access to repository contents.

Locations:

- `.github/workflows/build.yaml:1`

### missing-permissions (severity: medium)

lint.yaml has no top-level `permissions:` key and none of its jobs (hadolint, markdown-lint, yamllint) define job-level permissions. Without explicit permissions, the workflow runs with the default (potentially broad) GITHUB_TOKEN permissions.

Locations:

- `.github/workflows/lint.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all four findings across both workflow files:

build.yaml:
- Pinned actions/checkout@v5 → @93cb6efe18208431cddfb8368fd83d5badbf9bfd # v5
- Pinned docker/metadata-action@v5 → @c299e40c65443455700f0fdfc63efafe5b349051 # v5
- Pinned docker/setup-qemu-action@v3 → @c7c53464625b32c7a7e944ae62b3e17d2b600130 # v3
- Pinned docker/setup-buildx-action@v3 → @8d2750c68a42422c14e847fe6c8ac0403b4cbd6f # v3
- Pinned docker/login-action@v3 → @c94ce9fb468520275223c153574b00df6fe4bcc9 # v3
- Pinned docker/build-push-action@v6 → @10e90e3645eae34f1e60eeb005ba3a3d33f178e8 # v6
- Added top-level permissions: contents: read
- Added job-level permissions: contents: read, packages: write (docker job may push images)

lint.yaml:
- Pinned all three actions/checkout@v5 references → @93cb6efe18208431cddfb8368fd83d5badbf9bfd # v5
- Added top-level permissions: contents: read
- Added job-level permissions: contents: read for all three lint jobs (hadolint, markdown-lint, yamllint)

