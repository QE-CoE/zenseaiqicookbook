# Test Reviewer

> **Policy-aware quality gate** — checks a generated test suite against policy packs and surfaces coverage gaps before automation begins.

| | |
|---|---|
| **Stack** | TypeScript (runs in the frontend — no upstream service) |
| **Stage** | Requirements & Specs (quality gate) |
| **Upstream** | CaseGeni |
| **Downstream** | Auto-PlayPilot |
| **Source** | `frontend/src/modules/agent/test-reviewer/` |

## What it does

Test Reviewer solves a problem that usually surfaces far too late: discovering at audit, or after automation has already been built, that a test suite never covered something it was obliged to. It applies policy packs — reusable sets of quality and compliance rules — to a generated suite and reports exactly where that suite falls short. Testers and automation engineers run it as a gate between test design and automation, at the point where fixing a gap still costs a test-case edit rather than a full regeneration cycle. Its input is a CaseGeni test suite plus the packs relevant to the work; its output is a per-rule finding set describing each gap and what needs to change. The REST API pack checks negative coverage, boundary cases, happy and sad path balance, expected results, steps, automation hints, priority spread, and authentication and data-validation coverage. The BFSI pack adds masking of personally identifiable information and positive *and* negative role-based access checks drawn from PCI-DSS and RBI digital lending guidance. The HLS pack verifies protected health information audit logging and encryption in line with the HIPAA Security Rule, while a cross-cutting UI pack checks accessibility coverage on interface-heavy stories. Packs are sector-aware, so a healthcare project is measured against healthcare rules without anyone remembering to select them. Rules combine deterministic checks with model-assisted assessment for the judgements that require actually reading the test. For regulated programmes the outcome is documented evidence that a control was checked rather than assumed; for engineering teams it is markedly less automation rework. Test Reviewer sits between CaseGeni and Auto-PlayPilot in the pipeline and is the cheapest quality gate the platform offers.

Test Reviewer applies **policy packs** — reusable sets of quality and compliance rules — to a generated test suite, and reports where the suite falls short.

**What you give it:** a CaseGeni test suite, and the policy packs relevant to your sector.

**What you get back:** per-rule findings across the suite, the gaps each one represents, and what needs to change before the suite is fit for automation.

### Policy packs

| Pack | What it enforces |
|---|---|
| **REST API Best Practices** | Negative coverage, boundary cases, happy/sad path balance, expected results present, steps present, automation hints, priority spread, authentication and data-validation coverage |
| **BFSI / Regulated Finance** | PII masking, role-based access control positive *and* negative coverage, payment-flow gates derived from PCI-DSS and RBI digital lending guidance |
| **HLS / HIPAA** | Protected health information audit-logging and encryption verification, aligned to the HIPAA Security Rule |
| **UI Quality Cross-Cutting** | Accessibility coverage across UI-heavy stories |

Packs are **sector-aware** — the BFSI and HLS packs surface automatically for tenants in those sectors, while the REST API and UI packs apply everywhere. Rules combine deterministic checks with model-assisted assessment for the judgements that need reading comprehension.

## Why it matters

The expensive way to discover that a test suite has no negative authorisation coverage is at an audit. The second most expensive way is after it has already been automated, when every gap means regenerating scripts.

Test Reviewer moves that check to the cheapest possible point — immediately after generation, before automation. Typical use:

- **Pre-automation gate** — confirm the suite is worth automating before spending the cycles
- **Regulatory readiness** — evidence that PII masking or PHI audit rules were checked, not assumed
- **Sector compliance** — apply the right rulebook automatically, rather than relying on each tester knowing it
- **Consistency across teams** — the same standard applied whoever wrote the tests

The business outcome is fewer compliance findings late in delivery, less rework in automation, and a documented quality gate for release governance.

## In the UI

<!-- SCREENSHOT: test-reviewer-01-scores.png — Policy pack selection with per-rule findings -->
*Select the applicable packs — sector packs appear automatically.*

<!-- SCREENSHOT: test-reviewer-02-duplicates.png — Findings detail with the gaps each rule identified -->
*Findings per rule, with the gap each one represents.*

## Tips

- **Run it before [Auto-PlayPilot](auto-playpilot.md).** Fixing a coverage gap in a test case takes a minute; fixing it after script generation means regenerating.
- **Stack the packs.** REST API plus your sector pack is the usual combination — they check different things.
- **Treat findings as backlog, not blockers.** Most are quick test-case edits; the value is in seeing them all at once.

[← Back to agents](index.md)
