<!-- markdownlint-disable -->

# Hardening Report: DavidAnson--markdownlint-cli2-action/v23.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **DavidAnson--markdownlint-cli2-action/v23.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All four workflow files reference external actions using mutable tags instead of full 40-character SHA commit digests. This exposes the workflow to supply-chain attacks where a tag can be silently moved to point to malicious code. Failing references include: actions/checkout@v6, actions/setup-node@v6, tj-actions/changed-files@v47, DavidAnson/markdownlint-cli2-action@v23, JustinBeckwith/linkinator-action@v2, tbroadley/spellchecker-cli-action@v1. Each should be pinned to a full SHA, e.g. actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.

Locations:

- `.github/workflows/test.yml:14`
- `.github/workflows/test.yml:15`
- `.github/workflows/changed.yml:5`
- `.github/workflows/changed.yml:8`
- `.github/workflows/changed.yml:13`
- `.github/workflows/checkers.yml:15`
- `.github/workflows/checkers.yml:16`
- `.github/workflows/checkers.yml:22`
- `.github/workflows/checkers.yml:23`
- `.github/workflows/example.yml:5`
- `.github/workflows/example.yml:6`

### missing-permissions (severity: medium)

None of the four workflow files define a top-level 'permissions:' block, and no individual jobs define job-level permissions either. Without explicit permissions, GitHub Actions defaults to the repository's default token permissions (which may be read-write), granting more access than necessary. Each workflow should declare minimal required permissions (e.g. 'permissions: read-all' or specific scopes like 'contents: read').

Locations:

- `.github/workflows/test.yml:1`
- `.github/workflows/changed.yml:1`
- `.github/workflows/checkers.yml:1`
- `.github/workflows/example.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all four workflow files (.github/workflows/test.yml, changed.yml, checkers.yml, example.yml):

1. unpinned-uses: Pinned all external action references to full 40-character commit SHAs:
   - actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 # v6
   - actions/setup-node@v6 → @249970729cb0ef3589644e2896645e5dc5ba9c38 # v6
   - tj-actions/changed-files@v47 → @24d32ffd492484c1d75e0c0b894501ddb9d30d62 # v47
   - DavidAnson/markdownlint-cli2-action@v23 → @ded1f9488f68a970bc66ea5619e13e9b52e601cd # v23
   - JustinBeckwith/linkinator-action@v2 → @36a0bfbfecd5e237e8f8531537a693616c505faf # v2
   - tbroadley/spellchecker-cli-action@v1 → @8369e98753c0d2c3a3c76fb4519d9056d1d4b129 # v1

2. missing-permissions: Added top-level `permissions: contents: read` block to all four workflow files, granting only the minimum access needed for checkout operations.

