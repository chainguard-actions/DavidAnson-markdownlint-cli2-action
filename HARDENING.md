<!-- markdownlint-disable -->

# Hardening Report: DavidAnson--markdownlint-cli2-action/v24.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **DavidAnson--markdownlint-cli2-action/v24.2.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference external actions using mutable tags instead of pinned full-length SHA digests. This exposes the workflow to supply-chain attacks if the referenced tag is moved or the upstream repository is compromised.

.github/workflows/test.yml: `actions/checkout@v7`, `actions/setup-node@v7` (used in multiple jobs)
.github/workflows/changed.yml: `actions/checkout@v7`, `tj-actions/changed-files@v47`, `DavidAnson/markdownlint-cli2-action@v24`
.github/workflows/checkers.yml: `actions/checkout@v7`, `tbroadley/spellchecker-cli-action@v1`
.github/workflows/example.yml: `actions/checkout@v7`, `DavidAnson/markdownlint-cli2-action@v24`

Locations:

- `.github/workflows/test.yml:14`
- `.github/workflows/test.yml:15`
- `.github/workflows/changed.yml:6`
- `.github/workflows/changed.yml:7`
- `.github/workflows/changed.yml:11`
- `.github/workflows/checkers.yml:16`
- `.github/workflows/checkers.yml:20`
- `.github/workflows/example.yml:5`
- `.github/workflows/example.yml:6`

### missing-permissions (severity: medium)

None of the workflow files define a top-level `permissions:` block, and none of the individual jobs within them define job-level `permissions:` blocks. Without explicit permissions, workflows run with the default (potentially broad) token permissions, violating the principle of least privilege. All four workflow files are affected: test.yml, changed.yml, checkers.yml, and example.yml.

Locations:

- `.github/workflows/test.yml:1`
- `.github/workflows/changed.yml:1`
- `.github/workflows/checkers.yml:1`
- `.github/workflows/example.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all four workflow files: (1) Replaced all mutable tag references with pinned full-length SHA digests while preserving the tag in a comment for readability — actions/checkout@v7→3d3c42e5..., actions/setup-node@v7→820762786..., tj-actions/changed-files@v47→24d32ffd..., DavidAnson/markdownlint-cli2-action@v24→21c1be1b..., tbroadley/spellchecker-cli-action@v1→8369e987.... (2) Added top-level `permissions: {}` block to all four workflow files (test.yml, changed.yml, checkers.yml, example.yml) to enforce least-privilege token access.

