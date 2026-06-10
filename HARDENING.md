<!-- markdownlint-disable -->

# Hardening Report: dokku--github-action/v1.7.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **dokku--github-action/v1.7.0** was hardened automatically. 0 finding(s) were identified and resolved across 2 iteration(s).

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Dockerfile base image from the mutable tag `dokku/ci-docker-image:0.14.0` to the immutable digest `dokku/ci-docker-image@sha256:eeb61dcf61cae19f6de79833a33198ee76717594c1feec3aa701c27b5be9ca28 # 0.14.0`. The action.yaml already references `image: "Dockerfile"` and required no changes.

### Iteration 2

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all unpinned action references across 7 example workflow files to full 40-character commit SHAs with original tag names preserved as comments:
- actions/checkout@v4 → @34e114876b0b11c390a56381ad16ebd13914f8d5
- docker/setup-qemu-action@v3 → @c7c53464625b32c7a7e944ae62b3e17d2b600130
- docker/setup-buildx-action@v3 → @8d2750c68a42422c14e847fe6c8ac0403b4cbd6f
- docker/login-action@v3 → @c94ce9fb468520275223c153574b00df6fe4bcc9
- docker/build-push-action@v6 → @10e90e3645eae34f1e60eeb005ba3a3d33f178e8
- dokku/github-action@master → @b705ed643fea68530501b1faf37abe233caa06be
- styfle/cancel-workflow-action@0.12.1 → @85880fa0301c86cca9da44039ee3bb12d3bedbfa
All 24 locations identified in the findings were addressed.

