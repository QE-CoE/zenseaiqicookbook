# Defect Intelligence

> **Failure Triage Agent** — classifies failed test runs, clusters duplicates, suggests probable root cause.

| | |
|---|---|
| **Port** | `8011` |
| **Stack** | Python · FastAPI |
| **Stage** | Quality Intelligence |
| **Upstream** | Auto-PlayPilot execution (validated) |
| **Downstream** | Knowledge Graph |
| **Source** | `agents/defect-intelligence/` |

## What it does

Ingests an Auto-PlayPilot run report and produces:

- **Failure category** — `flaky` / `regression` / `env` / `data` / `selector-drift` / `assertion-mismatch`
- **Duplicate clusters** — fingerprinted by stack + assertion shape
- **Suggested root cause** — explained in plain language with the matching code/test line
- **Suggested fix path** — selector, wait condition, test data, or product defect

## Why it matters

A 500-test suite with 30 failures usually has 4-6 *actual* underlying bugs. Defect Intelligence shows you that clustering so triage takes minutes, not hours.

## In the UI

<!-- SCREENSHOT: defect-intel-01-input.png — Run report selector -->
<!-- SCREENSHOT: defect-intel-02-clusters.png — Failures clustered with category badges -->
<!-- SCREENSHOT: defect-intel-03-root-cause.png — Per-cluster root cause panel with suggested fix -->

[← Back to agents](index.md)
