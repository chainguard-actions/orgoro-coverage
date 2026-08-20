<!-- markdownlint-disable -->

# Hardening Report: orgoro--coverage/v3.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **orgoro--coverage/v3.2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `actions/checkout@v3` (a mutable tag, not a pinned 40-character SHA commit hash) in two steps. If the tag is moved or the referenced commit is compromised, the action will silently execute different code. Both occurrences should be replaced with a full SHA pin, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3`.

Locations:

- `.github/workflows/test.yml:8`
- `.github/workflows/test.yml:16`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/test.yml` has no top-level `permissions:` key, and neither the `build` job nor the `test` job defines its own `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions (which may be `write-all`), granting broader access than necessary. A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or per job.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Pinned both `actions/checkout@v3` references to the full commit SHA `a37ce9120846195fa4ece8f58b268e6043cb2f26` with `# v3` comment for readability. (2) Added a top-level `permissions: contents: read` block to restrict the workflow token to the minimum necessary permissions.

