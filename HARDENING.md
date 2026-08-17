<!-- markdownlint-disable -->

# Hardening Report: crazy-max--ghaction-virustotal/v4.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **crazy-max--ghaction-virustotal/v4.2.0** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in ci.yml use mutable version tags instead of pinned 40-character SHA commit hashes, making the workflow vulnerable to supply-chain attacks if the referenced action is compromised or the tag is moved. Failing references: `actions/checkout@v4` (line 26), `actions/setup-go@v5` (line 29).

Locations:

- `.github/workflows/ci.yml:26`
- `.github/workflows/ci.yml:29`

### unpinned-uses (severity: high)

All `uses:` references in labels.yml use mutable version tags instead of pinned 40-character SHA commit hashes. Failing references: `actions/checkout@v4` (line 33), `crazy-max/ghaction-github-labeler@v5` (line 36).

Locations:

- `.github/workflows/labels.yml:33`
- `.github/workflows/labels.yml:36`

### unpinned-uses (severity: high)

All `uses:` references in test.yml use mutable version tags instead of pinned 40-character SHA commit hashes. Failing references: `actions/checkout@v4` (line 21), `docker/bake-action@v6` (line 24), `codecov/codecov-action@v5` (line 34).

Locations:

- `.github/workflows/test.yml:21`
- `.github/workflows/test.yml:24`
- `.github/workflows/test.yml:34`

### unpinned-uses (severity: high)

All `uses:` references in validate.yml use mutable version tags instead of pinned 40-character SHA commit hashes. Failing references: `actions/checkout@v4` (line 26), `docker/bake-action/subaction/list-targets@v6` (line 30), `docker/bake-action@v6` (line 49).

Locations:

- `.github/workflows/validate.yml:26`
- `.github/workflows/validate.yml:30`
- `.github/workflows/validate.yml:49`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all mutable `uses:` references to full 40-character SHA commit hashes across four workflow files:
- ci.yml: actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262, actions/setup-go@v5 → @40f1582b2485089dde7abd97c1529aa768e1baff
- labels.yml: actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262, crazy-max/ghaction-github-labeler@v5 → @24d110aa46a59976b8a7f35518cb7f14f434c916
- test.yml: actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262, docker/bake-action@v6 → @5be5f02ff8819ecd3092ea6b2e6261c31774f2b4, codecov/codecov-action@v5 → @0fb7174895f61a3b6b78fc075e0cd60383518dac
- validate.yml: actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262, docker/bake-action/subaction/list-targets@v6 → @5be5f02ff8819ecd3092ea6b2e6261c31774f2b4, docker/bake-action@v6 → @5be5f02ff8819ecd3092ea6b2e6261c31774f2b4
Original version tags preserved as inline comments for readability.

