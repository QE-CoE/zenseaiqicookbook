# DataGeni

> **Test Data Synthesis Agent** — generates rule-compliant, realistic test data from a test case bundle.

| | |
|---|---|
| **Stack** | Python · FastAPI |
| **Stage** | Test Design |
| **Upstream** | CaseGeni (validated) |
| **Source** | `agents/datageni/` |

## What it does

Reads CaseGeni preconditions + step inputs and emits:

- **CSV / JSON datasets** matching the expected schema
- **Boundary fixtures** (min, max, off-by-one, empty)
- **Negative fixtures** (malformed, type-mismatched)
- **Persona fixtures** (locale-aware names, addresses, IDs)

Rules are inferred from the test case `preconditions` and `steps[].input` fields; you can also paste an explicit JSON schema or OpenAPI spec.

## Why it matters

Stops the "where do I get a test credit card for IN/SG/UK customers?" loop. Generates compliant fakes without leaving the workspace.

## In the UI

<!-- SCREENSHOT: datageni-01-input.png — Validated CaseGeni cases as input, schema hint editor -->
<!-- SCREENSHOT: datageni-02-output.png — Generated dataset table with download buttons (CSV/JSON) -->

## Tips

- For PII-heavy domains, enable the **"locale-faithful"** toggle — addresses match the country code in the persona.
- Datasets are linked back to the originating test case ID — Test Optimization uses this for selection.

[← Back to agents](index.md)
