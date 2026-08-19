<!-- markdownlint-disable -->

# Hardening Report: dokku--github-action/v1.9.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **dokku--github-action/v1.9.0** was hardened automatically. 4 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in build.yaml use mutable version tags instead of full 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if any of those actions are compromised or their tags are moved. Unpinned references: `actions/checkout@v5` (line 17), `docker/metadata-action@v5` (line 21), `docker/setup-qemu-action@v3` (line 31), `docker/setup-buildx-action@v3` (line 33), `docker/login-action@v3` (line 37), `docker/build-push-action@v6` (line 42).

Locations:

- `.github/workflows/build.yaml:17`
- `.github/workflows/build.yaml:21`
- `.github/workflows/build.yaml:31`
- `.github/workflows/build.yaml:33`
- `.github/workflows/build.yaml:37`
- `.github/workflows/build.yaml:42`

### unpinned-uses (severity: high)

The `actions/checkout@v5` reference in lint.yaml uses a mutable version tag instead of a full 40-character commit SHA. It appears in all three jobs (hadolint, markdown-lint, yamllint). The other three `uses:` references in this file are correctly SHA-pinned.

Locations:

- `.github/workflows/lint.yaml:19`
- `.github/workflows/lint.yaml:26`
- `.github/workflows/lint.yaml:37`

### missing-permissions (severity: medium)

build.yaml has no top-level `permissions:` key and none of its jobs define a `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary (e.g. write access to contents). A minimal permissions block such as `permissions: {}` or scoped permissions (e.g. `contents: read`) should be added.

Locations:

- `.github/workflows/build.yaml:1`

### missing-permissions (severity: medium)

lint.yaml has no top-level `permissions:` key and none of its jobs (hadolint, markdown-lint, yamllint) define a `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary. A minimal permissions block such as `permissions: {}` or `contents: read` should be added.

Locations:

- `.github/workflows/lint.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 4 findings across 2 workflow files:

build.yaml:
- Pinned actions/checkout@v5 → @93cb6efe18208431cddfb8368fd83d5badbf9bfd # v5
- Pinned docker/metadata-action@v5 → @c299e40c65443455700f0fdfc63efafe5b349051 # v5
- Pinned docker/setup-qemu-action@v3 → @c7c53464625b32c7a7e944ae62b3e17d2b600130 # v3
- Pinned docker/setup-buildx-action@v3 → @8d2750c68a42422c14e847fe6c8ac0403b4cbd6f # v3
- Pinned docker/login-action@v3 → @c94ce9fb468520275223c153574b00df6fe4bcc9 # v3
- Pinned docker/build-push-action@v6 → @10e90e3645eae34f1e60eeb005ba3a3d33f178e8 # v6
- Added top-level `permissions: contents: read`

lint.yaml:
- Pinned all 3 occurrences of actions/checkout@v5 → @93cb6efe18208431cddfb8368fd83d5badbf9bfd # v5 (hadolint, markdown-lint, yamllint jobs)
- Added top-level `permissions: contents: read`
- The other three action references (brpaz/hadolint-action, avto-dev/markdown-lint, ibiqlik/action-yamllint) were already SHA-pinned and left unchanged.

### Iteration 2

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all unpinned `uses:` references across 7 example workflow files:
- `actions/checkout@v5` → `@93cb6efe18208431cddfb8368fd83d5badbf9bfd # v5` (all 7 files)
- `dokku/github-action@master` → `@6a74219fbab2441a36df6a32a61d72f05d43a21b # master` (all 7 files, 3 occurrences in review-app.yaml)
- `docker/setup-qemu-action@v3` → `@c7c53464625b32c7a7e944ae62b3e17d2b600130 # v3` (build-and-deploy.yaml)
- `docker/setup-buildx-action@v3` → `@8d2750c68a42422c14e847fe6c8ac0403b4cbd6f # v3` (build-and-deploy.yaml)
- `docker/login-action@v3` → `@c94ce9fb468520275223c153574b00df6fe4bcc9 # v3` (build-and-deploy.yaml)
- `docker/build-push-action@v6` → `@10e90e3645eae34f1e60eeb005ba3a3d33f178e8 # v6` (build-and-deploy.yaml)
- `styfle/cancel-workflow-action@0.12.1` → `@85880fa0301c86cca9da44039ee3bb12d3bedbfa # 0.12.1` (cancel-previous-runs.yaml)

All SHAs were resolved using lookup_action_sha. No unpinned references remain.

