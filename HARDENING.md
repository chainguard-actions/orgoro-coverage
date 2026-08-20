<!-- markdownlint-disable -->

# Hardening Report: orgoro--coverage/v3.3.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **orgoro--coverage/v3.3.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses `actions/checkout@v3` (a mutable tag) in two steps instead of a pinned full 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) version without any change to the workflow file. Both the `build` and `test` jobs are affected.

Locations:

- `.github/workflows/test.yml:9`
- `.github/workflows/test.yml:15`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/test.yml` has no top-level `permissions:` block and neither the `build` job nor the `test` job defines job-level `permissions:`. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (e.g., write access to contents). Explicit minimal permissions should be declared.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned both `actions/checkout@v3` references to full SHA `a37ce9120846195fa4ece8f58b268e6043cb2f26` (with `# v3` comment) in both the `build` and `test` jobs. 2. Added a top-level `permissions: {}` block to deny all permissions by default, and added job-level `permissions: { contents: read }` to both jobs since they need to check out the repository.

