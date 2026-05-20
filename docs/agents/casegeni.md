# CaseGeni

> **Test Case Generation Agent** — produces structured test cases (positive, negative, edge) from refined user stories.

| | |
|---|---|
| **Port** | `8001` |
| **Stack** | Python · FastAPI |
| **Stage** | Test Design |
| **Upstream** | DeepSpeci (required, validated) |
| **Downstream** | Auto-PlayPilot, DataGeni, Test Reviewer |
| **Source** | `agents/casegeni/` |

## What it does

CaseGeni consumes validated DeepSpeci stories and emits a typed test case bundle:

| Field | Description |
|---|---|
| `id` | Stable case ID (`TC-001`, `TC-002`, …) |
| `title` | Short, action-oriented |
| `type` | `positive` / `negative` / `edge` / `boundary` |
| `priority` | `P1`-`P4` |
| `preconditions` | Setup steps |
| `steps[]` | Action + expected result per step |
| `tags[]` | Used by Test Optimization for selection |
| `requirementId` | Backlink to DeepSpeci story |

## Why it matters

Manually authoring 60+ test cases for a single story takes a tester 2-3 hours. CaseGeni gets you to a 90% draft in under 60 seconds and lets the tester focus on reviewing/augmenting.

## In the UI

<!-- SCREENSHOT: casegeni-01-input.png — CaseGeni workspace showing validated DeepSpeci stories as input -->
*Input panel auto-populated from upstream DeepSpeci.*

<!-- SCREENSHOT: casegeni-02-generation.png — Live generation stream, cases appearing one-by-one -->
*Cases stream in as the LLM produces them.*

<!-- SCREENSHOT: casegeni-03-table.png — Generated test case table with type/priority filters -->
*Filter by type and priority before validation.*

<!-- SCREENSHOT: casegeni-04-edit-case.png — Edit dialog for a single test case -->
*Inline edit — changes persist to the backend on save.*

## Tips

- Run **Test Reviewer** on the output before sending to Auto-PlayPilot. It catches duplicates and underspecified expected results.
- The `tags[]` field powers Test Optimization — adding `@smoke`, `@critical-path` etc. pays off later.

## What's new

- **April 2026** — Edge case heuristics improved (boundary detection on numeric ranges).
- **March 2026** — Bulk-edit priorities from the table header.

[← Back to agents](index.md)
