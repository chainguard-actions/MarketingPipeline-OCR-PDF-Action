<!-- markdownlint-disable -->

# Hardening Report: MarketingPipeline--OCR-PDF-Action/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **MarketingPipeline--OCR-PDF-Action/v2.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file references actions by mutable tag or branch instead of a full 40-character commit SHA. This exposes the workflow to supply-chain attacks if the referenced tag or branch is moved or overwritten. Failing references: `actions/checkout@v2` (tag) and `MarketingPipeline/OCR-PDF-Action@main` (branch). Both should be pinned to their full SHA, e.g. `actions/checkout@<40-char-sha> # v2`.

Locations:

- `.github/workflows/example_workflow.yaml:11`
- `.github/workflows/example_workflow.yaml:12`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the only job (`example_job`) also has no job-level `permissions:` key. Without explicit permissions, the GITHUB_TOKEN is granted its default (often broad) permissions. A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or on every job.

Locations:

- `.github/workflows/example_workflow.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/example_workflow.yaml: (1) Pinned `actions/checkout@v2` to full SHA `0717577d45739eb3c851188b29f50ed6c0b2194e # v2` and `MarketingPipeline/OCR-PDF-Action@main` to full SHA `35c5f0bbcd846030902eb86aba084e350f8a7528 # main`. (2) Added top-level `permissions: contents: read` block to restrict GITHUB_TOKEN to the minimum required permissions.

