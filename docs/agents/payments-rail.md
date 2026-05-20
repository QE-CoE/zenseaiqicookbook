# Payments-Rail

> **Payments Specification Agent** — validates payment flows against industry specs (ISO20022, card schemes, UPI, SEPA).

| | |
|---|---|
| **Stack** | TypeScript |
| **Stage** | Specialised |
| **Upstream** | DeepSpeci (optional) |
| **Source** | `agents/payments-rail/` |

## What it does

- Parses payment message specs (ISO20022 `pacs.008`, `pain.001`, card-scheme messages)
- Generates test data and assertions for each mandatory + conditional field
- Flags spec violations in captured live traffic

## In the UI

<!-- SCREENSHOT: payments-rail-01-spec.png — Spec selector + version -->
<!-- SCREENSHOT: payments-rail-02-validation.png — Field-by-field validation result -->

[← Back to agents](index.md)
