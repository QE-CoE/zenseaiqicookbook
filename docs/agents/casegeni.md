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

CaseGeni targets the part of testing that consumes the most analyst time: writing test cases. Given refined requirements it produces a complete, structured test suite in under a minute, where a tester working by hand would spend two to three hours on a single story. Testers and business analysts use it immediately after DeepSpeci, reviewing and augmenting the generated set rather than authoring from a blank page. It takes validated user stories as input and can be grounded in the Knowledge Base, so cases use your product names and business vocabulary instead of generic phrasing. Each generated case carries a stable identifier, an action-oriented title, a type covering positive, negative, edge and boundary conditions, a priority, preconditions, and numbered steps with an expected result for every individual step. Scenario-type classification and requirement backlinks keep the whole suite traceable to its source. Story and acceptance-criteria limits are configurable, so a very large requirement can be bounded deliberately rather than truncated arbitrarily. Where a story involves user-interface work, accessibility test cases are generated alongside the functional ones. The suite exports to Excel and CSV with steps, expected results and preconditions in separate columns, and can be pushed directly into qTest for teams whose test management lives there. Typical scenarios include designing a new feature, building a regression pack, and modernising an inherited manual suite. For QA the benefit is coverage breadth achieved quickly; for product and business stakeholders it is a readable artefact showing how a requirement will actually be verified. CaseGeni output feeds test data generation, automation scripting and policy review, placing it at the centre of the pipeline.

CaseGeni consumes validated DeepSpeci stories and emits a typed test case bundle:

| Field | Description |
|---|---|
| `id` | Stable case ID (`TC-001`, `TC-002`, …) |
| `title` | Short, action-oriented |
| `type` | `positive` / `negative` / `edge` / `boundary` |
| `priority` | `P1`-`P4` |
| `preconditions` | Setup steps |
| `steps[]` | Action plus a **step-specific expected result** for every step |
| `scenarioType` | Scenario classification used for grouping and traceability |
| `tags[]` | Used by Test Optimization for selection |
| `requirementId` | Backlink to DeepSpeci story |

Generation can be grounded in the [Knowledge Base](knowledge-base.md), so cases use your domain terminology. **Story and acceptance-criteria limits are configurable**, which keeps very large requirements bounded deliberately rather than by truncation. Where a story warrants it, **accessibility (ADA) test cases** are generated alongside the functional set.

Test cases export to **Excel and CSV**, with steps, expected results and preconditions in separate columns, and can be pushed to qTest.

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

- Run **[Test Reviewer](test-reviewer.md)** on the output before sending to Auto-PlayPilot. It applies your sector's policy pack and catches coverage gaps that are far cheaper to fix now than after script generation.
- The `tags[]` field powers Test Optimization — adding `@smoke`, `@critical-path` etc. pays off later.
- **Set story and AC limits** on large requirements so the run is bounded by intent rather than by whatever the model produces.

## What's new

- **July 2026** — Expected results for every test step; test-case display reorganised into distinct sections; configurable story and acceptance-criteria limits; accessibility (ADA) test cases; scenario-type classification and corrected traceability; Excel and CSV export fixes (separate step/expected-result columns, text wrapping, column widths, junk characters removed).
- **June 2026** — Knowledge Base retrieval for domain-grounded generation; Guidewire test generation; export/import round-trip and special-character handling corrected.
- **April 2026** — Edge case heuristics improved (boundary detection on numeric ranges).
- **March 2026** — Bulk-edit priorities from the table header.

[← Back to agents](index.md)
