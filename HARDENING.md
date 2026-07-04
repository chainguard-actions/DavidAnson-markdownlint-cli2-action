<!-- markdownlint-disable -->

# Hardening Report: DavidAnson--markdownlint-cli2-action--/v24.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **DavidAnson--markdownlint-cli2-action--/v24.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All workflow files use mutable tag-based references (e.g., @v7, @v47, @v24, @v6, @v1) instead of pinned 40-character SHA commit hashes. This exposes the workflow to supply-chain attacks if the referenced tag is moved or the action is compromised. Failing references include: actions/checkout@v7, tj-actions/changed-files@v47, DavidAnson/markdownlint-cli2-action@v24, actions/setup-node@v6, tbroadley/spellchecker-cli-action@v1.

Locations:

- `.github/workflows/changed.yml:6`
- `.github/workflows/changed.yml:8`
- `.github/workflows/changed.yml:11`
- `.github/workflows/checkers.yml:16`
- `.github/workflows/checkers.yml:22`
- `.github/workflows/checkers.yml:23`
- `.github/workflows/example.yml:6`
- `.github/workflows/example.yml:7`
- `.github/workflows/test.yml:15`
- `.github/workflows/test.yml:16`

### missing-permissions (severity: medium)

None of the workflow files define a top-level 'permissions:' key, and no individual job defines its own 'permissions:' block. Without explicit permissions, workflows run with the default token permissions which may be overly broad (e.g., write access to repository contents). Each workflow should declare minimal required permissions.

Locations:

- `.github/workflows/changed.yml:1`
- `.github/workflows/checkers.yml:1`
- `.github/workflows/example.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all four workflow files (.github/workflows/changed.yml, checkers.yml, example.yml, test.yml):

1. unpinned-uses: Replaced all mutable tag references with pinned 40-character commit SHAs:
   - actions/checkout@v7 → @9c091bb21b7c1c1d1991bb908d89e4e9dddfe3e0 # v7
   - tj-actions/changed-files@v47 → @24d32ffd492484c1d75e0c0b894501ddb9d30d62 # v47
   - DavidAnson/markdownlint-cli2-action@v24 → @8de2aa07cae85fd17c0b35642db70cf5495f1d25 # v24
   - actions/setup-node@v6 → @48b55a011bda9f5d6aeb4c2d9c7362e8dae4041e # v6
   - tbroadley/spellchecker-cli-action@v1 → @8369e98753c0d2c3a3c76fb4519d9056d1d4b129 # v1
   Local `./` references in test.yml were left unchanged as they reference the local action.

2. missing-permissions: Added `permissions: {}` top-level block to all four workflow files to enforce least-privilege (none of the workflows require any specific GitHub token permissions).

