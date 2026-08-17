<!-- markdownlint-disable -->

# Hardening Report: crazy-max--ghaction-virustotal/v4.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **crazy-max--ghaction-virustotal/v4.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All four workflow files reference GitHub Actions using mutable version tags (@v3, @v4) instead of pinned full 40-character SHA commit hashes. This exposes the workflows to supply-chain attacks if a tag is moved or a dependency is compromised. Failing references:
- ci.yml: actions/checkout@v4, actions/setup-go@v4
- test.yml: actions/checkout@v4, docker/bake-action@v3, codecov/codecov-action@v3
- validate.yml: actions/checkout@v3 (×2), docker/bake-action@v3
- labels.yml: actions/checkout@v4, crazy-max/ghaction-github-labeler@v4

Locations:

- `.github/workflows/ci.yml:20`
- `.github/workflows/ci.yml:23`
- `.github/workflows/test.yml:17`
- `.github/workflows/test.yml:20`
- `.github/workflows/test.yml:27`
- `.github/workflows/validate.yml:20`
- `.github/workflows/validate.yml:35`
- `.github/workflows/validate.yml:38`
- `.github/workflows/labels.yml:18`
- `.github/workflows/labels.yml:21`

### missing-permissions (severity: medium)

None of the four workflow files define a top-level `permissions:` key, and no individual job defines a `permissions:` block either. This means all jobs run with the default broad GITHUB_TOKEN permissions (read/write to repository contents, packages, etc.), violating the principle of least privilege.

Locations:

- `.github/workflows/ci.yml:1`
- `.github/workflows/test.yml:1`
- `.github/workflows/validate.yml:1`
- `.github/workflows/labels.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 4 workflow files:

**unpinned-uses** — Pinned all 10 action references to full 40-char SHAs with tag comments:
- actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 (ci.yml, test.yml, labels.yml)
- actions/checkout@v3 → @a37ce9120846195fa4ece8f58b268e6043cb2f26 (validate.yml ×2)
- actions/setup-go@v4 → @7b8cf10d4e4a01d4992d18a89f4d7dc5a3e6d6f4 (ci.yml)
- docker/bake-action@v3 → @45c4bed4f4f232fb1466194a6cbdd7a18bcf0639 (test.yml, validate.yml)
- codecov/codecov-action@v3 → @ab904c41d6ece82784817410c45d8b8c02684457 (test.yml)
- crazy-max/ghaction-github-labeler@v4 → @f4f6b96e7e747b5416cd470f3cfecf26abaa811e (labels.yml)

**missing-permissions** — Added top-level `permissions:` blocks to all 4 files:
- ci.yml: `contents: read`
- test.yml: `contents: read`
- validate.yml: `contents: read`
- labels.yml: `contents: read`, `issues: write` (needed by ghaction-github-labeler to manage labels)

