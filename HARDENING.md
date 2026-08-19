<!-- markdownlint-disable -->

# Hardening Report: orgoro--coverage/v3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **orgoro--coverage/v3** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow references `actions/checkout@v2` twice using a mutable version tag instead of a pinned 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) version without any change to the workflow file. Both occurrences should be replaced with the full SHA digest, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v2`.

Locations:

- `.github/workflows/test.yml:8`
- `.github/workflows/test.yml:16`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and neither job (`build` nor `test`) defines its own `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (e.g. write access to contents). A minimal `permissions:` block should be added — for example `permissions: read-all` at the top level, or specific scopes per job.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed hardened/action/.github/workflows/test.yml: (1) Pinned both `actions/checkout@v2` references to the full commit SHA `0717577d45739eb3c851188b29f50ed6c0b2194e` with `# v2` comment for readability. (2) Added a top-level `permissions: contents: read` block to restrict the workflow token to the minimum required scope.

