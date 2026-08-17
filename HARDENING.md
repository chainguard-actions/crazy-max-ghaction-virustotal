<!-- markdownlint-disable -->

# Hardening Report: crazy-max--ghaction-virustotal/v3.3.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **crazy-max--ghaction-virustotal/v3.3.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All three workflow files use mutable tag-based `uses:` references instead of pinned 40-character commit SHAs. This exposes the workflow to supply-chain attacks if any referenced action's tag is moved or compromised.

.github/workflows/ci.yml:
  - uses: actions/checkout@v4
  - uses: actions/setup-go@v4
  - uses: crazy-max/ghaction-dump-context@v2

.github/workflows/labels.yml:
  - uses: actions/checkout@v4
  - uses: crazy-max/ghaction-github-labeler@v4

.github/workflows/test.yml:
  - uses: actions/checkout@v4
  - uses: docker/bake-action@v3 (x2)
  - uses: codecov/codecov-action@v3

Locations:

- `.github/workflows/ci.yml:16`
- `.github/workflows/ci.yml:19`
- `.github/workflows/ci.yml:36`
- `.github/workflows/labels.yml:20`
- `.github/workflows/labels.yml:23`
- `.github/workflows/test.yml:16`
- `.github/workflows/test.yml:19`
- `.github/workflows/test.yml:23`
- `.github/workflows/test.yml:30`

### missing-permissions (severity: medium)

None of the three workflow files define a top-level `permissions:` block, and no individual job within them defines job-level permissions either. Without explicit permissions, workflows inherit the repository's default token permissions (which may be broad write-all). Each workflow should declare minimal required permissions.

Locations:

- `.github/workflows/ci.yml:1`
- `.github/workflows/labels.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all three workflow files:

**unpinned-uses**: Replaced all 9 mutable tag references with pinned commit SHAs (tag preserved as comment):
- actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 (used in all 3 files)
- actions/setup-go@v4 → @7b8cf10d4e4a01d4992d18a89f4d7dc5a3e6d6f4 (ci.yml)
- crazy-max/ghaction-dump-context@v2 → @5355a8e5e6ac5a302e746a1c4b7747a0393863c8 (ci.yml)
- crazy-max/ghaction-github-labeler@v4 → @f4f6b96e7e747b5416cd470f3cfecf26abaa811e (labels.yml)
- docker/bake-action@v3 → @45c4bed4f4f232fb1466194a6cbdd7a18bcf0639 (test.yml, x2)
- codecov/codecov-action@v3 → @ab904c41d6ece82784817410c45d8b8c02684457 (test.yml)

**missing-permissions**: Added top-level `permissions:` blocks to all three files:
- ci.yml: `contents: read` (checkout + build only)
- labels.yml: `contents: read` + `issues: write` (labeler needs to create/update labels)
- test.yml: `contents: read` (checkout + Docker bake + coverage upload)

