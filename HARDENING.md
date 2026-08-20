<!-- markdownlint-disable -->

# Hardening Report: orgoro--coverage/v3.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **orgoro--coverage/v3.3** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses `actions/checkout@v3` (a mutable tag reference, not a pinned 40-character commit SHA) in two steps — one in the `build` job and one in the `test` job. A tag can be moved to point to a different, potentially malicious commit, enabling supply-chain attacks.

Locations:

- `.github/workflows/test.yml:9`
- `.github/workflows/test.yml:16`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key, and neither the `build` job nor the `test` job defines its own `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary (e.g., write access to contents and pull-requests).

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both findings in .github/workflows/test.yml: (1) Pinned both `actions/checkout@v3` references to the full commit SHA `a37ce9120846195fa4ece8f58b268e6043cb2f26` (with `# v3` comment for readability). (2) Added `permissions: {}` at the top level to explicitly deny all default token permissions, preventing over-broad access.

