<!-- markdownlint-disable -->

# Hardening Report: crazy-max--ghaction-virustotal/v4.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **crazy-max--ghaction-virustotal/v4.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All workflow files use mutable version tags instead of full 40-character SHA commit hashes for their `uses:` references. This exposes the action to supply-chain attacks if any referenced action is compromised or its tag is moved. Failing references: actions/checkout@v4, actions/setup-go@v5, docker/bake-action@v5, codecov/codecov-action@v4, crazy-max/ghaction-github-labeler@v5.

Locations:

- `.github/workflows/ci.yml:20`
- `.github/workflows/ci.yml:23`
- `.github/workflows/test.yml:17`
- `.github/workflows/test.yml:20`
- `.github/workflows/test.yml:27`
- `.github/workflows/validate.yml:21`
- `.github/workflows/validate.yml:38`
- `.github/workflows/labels.yml:20`
- `.github/workflows/labels.yml:23`

### missing-permissions (severity: medium)

None of the workflow files define a top-level `permissions:` block, and no job within any workflow defines job-level permissions. Without explicit permissions, workflows run with default GitHub token permissions which may be broader than necessary (e.g., write access to contents, packages, etc.).

Locations:

- `.github/workflows/ci.yml:1`
- `.github/workflows/test.yml:1`
- `.github/workflows/validate.yml:1`
- `.github/workflows/labels.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 9 unpinned action references across 4 workflow files by replacing mutable version tags with full 40-character SHA commit hashes (preserving tags as comments). Added minimal top-level permissions blocks to all 4 workflow files: ci.yml, test.yml, and validate.yml get 'contents: read'; labels.yml gets 'contents: read' plus 'issues: write' (required for the GitHub Labeler action to manage labels).

