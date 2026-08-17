<!-- markdownlint-disable -->

# Hardening Report: crazy-max--ghaction-virustotal/v5.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **crazy-max--ghaction-virustotal/v5.0.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references across the workflow files use mutable version tags (e.g., @v6, @v5) instead of immutable full 40-character SHA commit hashes. This exposes the workflow to supply-chain attacks where a tag could be silently moved to point to malicious code. Affected references: actions/checkout@v6, actions/setup-go@v6, crazy-max/ghaction-github-labeler@v6, docker/bake-action@v6, docker/bake-action/subaction/list-targets@v6, codecov/codecov-action@v5.

Locations:

- `.github/workflows/ci.yml:26`
- `.github/workflows/ci.yml:29`
- `.github/workflows/labels.yml:33`
- `.github/workflows/labels.yml:36`
- `.github/workflows/test.yml:21`
- `.github/workflows/test.yml:24`
- `.github/workflows/test.yml:31`
- `.github/workflows/validate.yml:26`
- `.github/workflows/validate.yml:30`
- `.github/workflows/validate.yml:42`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all 6 unique action references across 4 workflow files to their full 40-character commit SHAs (with original tags preserved as comments): actions/checkout@v6 → d23441a48e516b6c34aea4fa41551a30e30af803, actions/setup-go@v6 → 924ae3a1cded613372ab5595356fb5720e22ba16, crazy-max/ghaction-github-labeler@v6 → 548a7c3603594ec17c819e1239f281a3b801ab4d, docker/bake-action@v6 → 5be5f02ff8819ecd3092ea6b2e6261c31774f2b4, docker/bake-action/subaction/list-targets@v6 → 5be5f02ff8819ecd3092ea6b2e6261c31774f2b4, codecov/codecov-action@v5 → 0fb7174895f61a3b6b78fc075e0cd60383518dac. All 10 affected locations have been fixed.

