# DataGeni

> **Test Data Synthesis Agent** — generates realistic, rule-compliant test data that respects the relationships between your tables.

| | |
|---|---|
| **Port** | `8007` |
| **Stack** | Python · FastAPI |
| **Stage** | Test Design |
| **Upstream** | CaseGeni (validated), or a CSV/Excel upload |
| **Source** | `agents/datageni/` |

## What it does

DataGeni removes the most common reason a ready test cannot actually run: the absence of usable test data. The realistic alternatives are extracting from production, which carries privacy and compliance exposure, or hand-crafting rows, which takes hours and usually covers only the happy path. Testers and automation engineers point DataGeni at a source and receive coherent datasets in minutes. It accepts validated CaseGeni test cases from the pipeline, a CaseGeni CSV or Excel export uploaded directly, an explicit JSON schema or OpenAPI specification, or a live database connection managed through the Connection Manager. From these it produces CSV and JSON datasets, boundary fixtures covering minimum, maximum, off-by-one and empty values, negative fixtures with malformed and type-mismatched values, and locale-aware persona fixtures. Critically, it enforces foreign-key integrity across generated entities, so a customer referenced by an order actually exists — the difference between data that loads and data that fails on insert. Rules are inferred from test case preconditions and step inputs, or read from a schema you supply. It runs inside a pipeline or standalone, selecting its own source when launched on its own. Typical uses include seeding a fresh test environment, generating market-appropriate data for multi-region testing, and producing the awkward boundary values nobody enjoys writing by hand. For compliance and security teams the outcome is one less reason to copy production data into a lower environment; for testers it is being unblocked in minutes rather than days. DataGeni consumes CaseGeni output and supports the automation and execution stages that follow.

**What you give it** — any of:

- Validated CaseGeni test cases from the pipeline
- A **CaseGeni CSV or Excel export**, uploaded directly
- An explicit JSON schema or OpenAPI specification
- A **database connection**, managed through the Connection Manager

**What you get back:**

- **CSV / JSON datasets** matching the expected schema
- **Boundary fixtures** — minimum, maximum, off-by-one, empty
- **Negative fixtures** — malformed and type-mismatched values
- **Persona fixtures** — locale-aware names, addresses and identifiers

Rules are inferred from test case preconditions and step inputs, or read from the schema you supply. **Foreign-key integrity is enforced across generated entities**, so a customer referenced by an order actually exists — the difference between data that loads and data that fails on insert.

DataGeni can run inside a pipeline or **standalone**, selecting its own source when launched on its own.

## Why it matters

Test data is the most common reason a ready test cannot run. The realistic options are usually a production extract — which carries privacy and compliance risk — or hand-crafted rows, which take hours and cover only the happy path.

Typical use:

- **Environment seeding** — populate a fresh test environment with coherent, related data
- **Privacy-safe testing** — remove the need for production extracts, and the exposure that comes with them
- **Boundary and negative coverage** — get the awkward values nobody enjoys writing by hand
- **Locale coverage** — generate market-appropriate data for multi-region testing
- **Referential integrity** — multi-table data that loads cleanly first time

The business outcome is testers unblocked in minutes rather than days, and one less reason to copy production data into a lower environment.

## In the UI

<!-- SCREENSHOT: datageni-01-input.png — Source selector: pipeline, upload, schema or database connection -->
*Choose a source — pipeline output, upload, schema or database connection.*

<!-- SCREENSHOT: datageni-02-output.png — Generated dataset table with CSV/JSON download -->
*Generated datasets, downloadable as CSV or JSON.*

<!-- SCREENSHOT: datageni-03-connection-manager.png — Connection Manager for reusable database connections -->
*Connection Manager — reusable, credential-backed database connections.*

## Tips

- For PII-heavy domains, enable the **"locale-faithful"** toggle — addresses match the country code in the persona.
- Datasets link back to the originating test case ID, which downstream agents use for correlation.
- **Upload a CaseGeni export** when you want data for a suite that was designed outside the current pipeline run.

## What's new

- **July 2026** — CaseGeni CSV/Excel uploads accepted with improved schema inference; foreign-key integrity enforced across generated entities; generation stream kept alive through slow model responses; explicit `null` constraints treated as missing.
- **June 2026** — Source selector for standalone launches, Connection Manager for reusable database connections, per-card URLs and clearer navigation.

[← Back to agents](index.md)
