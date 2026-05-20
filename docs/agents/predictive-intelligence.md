# Predictive Intelligence

> **Risk Forecasting Agent** — flags risky modules from code churn + historical failure data *before* tests run.

| | |
|---|---|
| **Stack** | Next.js (bundled in `agents/other-agents/`) |
| **Stage** | Quality Intelligence |
| **Source** | `agents/other-agents/src/agents/predictive/` |

## What it does

Crawls the connected repository's commit history and prior test runs, scores each module on:

- **Churn** — lines changed in last N days
- **Failure density** — historical test failures touching that module
- **Coupling** — how many other modules depend on it
- **Owner load** — author count + bus factor

Output: a **ranked risk list** that informs which tests to prioritise.

## Why it matters

Run the 50 highest-risk tests in 5 minutes during PR validation instead of the full 2-hour suite. Catch 80% of regressions in 5% of the time.

## In the UI

<!-- SCREENSHOT: predictive-01-dashboard.png — Risk heatmap by module -->
<!-- SCREENSHOT: predictive-02-detail.png — Module detail: churn, failure history, suggested tests -->

[← Back to agents](index.md)
