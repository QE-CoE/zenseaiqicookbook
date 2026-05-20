# Test Reviewer

> **Quality review agent** — scores and reviews generated test cases for clarity, coverage, and duplication.

| | |
|---|---|
| **Stack** | Python · FastAPI |
| **Stage** | Requirements & Specs (quality gate) |
| **Upstream** | CaseGeni |
| **Source** | bundled in `agents/casegeni/` |

## What it does

For each generated test case:

- **Clarity score** — is the step + expected result unambiguous?
- **Coverage score** — does the set cover positive, negative, edge?
- **Duplicate flags** — pairs of near-identical cases
- **Suggested improvements** — concrete rewrite proposals

Use it as a soft gate before kicking off Auto-PlayPilot — saves regenerating scripts later.

## In the UI

<!-- SCREENSHOT: test-reviewer-01-scores.png — Score panel per test case -->
<!-- SCREENSHOT: test-reviewer-02-duplicates.png — Duplicate cluster view -->

[← Back to agents](index.md)
