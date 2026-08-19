<!-- markdownlint-disable -->

# Hardening Report: dokku--github-action/v1.10.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **dokku--github-action/v1.10.0** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple `uses:` references in .github/workflows/build.yaml are pinned to mutable version tags instead of full 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if those tags are moved. Unpinned references: `actions/checkout@v6`, `docker/metadata-action@v6`, `docker/setup-qemu-action@v4`, `docker/setup-buildx-action@v4`, `docker/login-action@v4`, `docker/build-push-action@v7`.

Locations:

- `.github/workflows/build.yaml:17`
- `.github/workflows/build.yaml:21`
- `.github/workflows/build.yaml:33`
- `.github/workflows/build.yaml:35`
- `.github/workflows/build.yaml:39`
- `.github/workflows/build.yaml:43`

### unpinned-uses (severity: high)

Multiple `uses:` references in .github/workflows/lint.yaml are pinned to mutable version tags instead of full 40-character commit SHAs. Unpinned references: `actions/checkout@v6` appears in all three jobs (hadolint, markdown-lint, yamllint).

Locations:

- `.github/workflows/lint.yaml:18`
- `.github/workflows/lint.yaml:30`
- `.github/workflows/lint.yaml:43`

### missing-permissions (severity: medium)

.github/workflows/build.yaml has no top-level `permissions:` key and no job-level `permissions:` on any job. Without explicit permissions, the workflow runs with the default (potentially broad) token permissions.

Locations:

- `.github/workflows/build.yaml:1`

### missing-permissions (severity: medium)

.github/workflows/lint.yaml has no top-level `permissions:` key and no job-level `permissions:` on any job. Without explicit permissions, the workflow runs with the default (potentially broad) token permissions.

Locations:

- `.github/workflows/lint.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all findings in both workflow files:

**build.yaml**:
- Added top-level `permissions: contents: read` block to address missing-permissions finding.
- Pinned all 6 unpinned action references to full 40-character commit SHAs:
  - actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803
  - docker/metadata-action@v6 → @dc802804100637a589fabce1cb79ff13a1411302
  - docker/setup-qemu-action@v4 → @96fe6ef7f33517b61c61be40b68a1882f3264fb8
  - docker/setup-buildx-action@v4 → @bb05f3f5519dd87d3ba754cc423b652a5edd6d2c
  - docker/login-action@v4 → @af1e73f918a031802d376d3c8bbc3fe56130a9b0
  - docker/build-push-action@v7 → @53b7df96c91f9c12dcc8a07bcb9ccacbed38856a

**lint.yaml**:
- Added top-level `permissions: contents: read` block to address missing-permissions finding.
- Pinned all 3 actions/checkout@v6 references to @d23441a48e516b6c34aea4fa41551a30e30af803
- The other actions in lint.yaml (brpaz/hadolint-action, avto-dev/markdown-lint, ibiqlik/action-yamllint) were already pinned to full commit SHAs.

All version tags preserved as inline comments for readability.

