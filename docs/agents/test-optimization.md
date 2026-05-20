# Test Optimization

> **Test Selection Agent** — picks the minimum test subset that retains coverage for a given code change.

| | |
|---|---|
| **Stack** | Next.js (bundled in `agents/other-agents/`) |
| **Stage** | Quality Intelligence |
| **Source** | `agents/other-agents/src/agents/test-optimization/` |

## What it does

Given a diff or PR, returns:

- **Tests-to-run** — selected by tag, module mapping, and historical failure correlation
- **Tests-to-skip** — explicitly justified
- **Estimated runtime saved**
- **Coverage delta** — what's untested by the selection

## Why it matters

PRs that touch a settings page shouldn't trigger the full payments-flow suite. Test Optimization automates the judgement call.

## In the UI

<!-- SCREENSHOT: test-opt-01-input.png — Diff / PR URL input -->
<!-- SCREENSHOT: test-opt-02-selection.png — Selected vs skipped tests with reasoning -->

[← Back to agents](index.md)
