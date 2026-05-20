# Knowledge Graph

> **Traceability Agent** — builds a graph linking requirements ↔ test cases ↔ defects ↔ code modules.

| | |
|---|---|
| **Stack** | Next.js (bundled in `agents/other-agents/`) |
| **Stage** | Quality Intelligence |
| **Upstream** | Defect Intelligence |
| **Source** | `agents/other-agents/src/agents/knowledge-graph/` |

## What it does

Pulls IDs from every agent in the pipeline and answers questions like:

- "Which tests cover requirement REQ-127?"
- "What requirements does the failing test `checkout-flow.spec.ts` validate?"
- "Which modules touch the most failed-test fingerprints in the last sprint?"

Surfaces traceability gaps visually.

## In the UI

<!-- SCREENSHOT: knowledge-graph-01-overview.png — Interactive force-directed graph -->
<!-- SCREENSHOT: knowledge-graph-02-query.png — Query panel with results -->

[← Back to agents](index.md)
