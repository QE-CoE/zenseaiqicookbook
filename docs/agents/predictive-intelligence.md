# Predictive Intelligence

> **Outcome Prediction Agent** — predicts whether a test will pass, fail or prove inconclusive *before* it is executed, and recommends what to do about it.

| | |
|---|---|
| **Stack** | Next.js (bundled in `agents/other-agents/`) · port `8003` |
| **Stage** | Quality Intelligence |
| **Upstream** | CaseGeni test cases · requirements · source code |
| **Source** | `agents/other-agents/src/agents/predictive-intelligence/` |

## What it does

Predictive Intelligence tackles a cost most teams absorb without noticing: executing tests that were never going to pass. A significant share of failures are not product defects at all, but tests that contradict the requirement, or tests assuming a code path the implementation does not provide — and each still consumes an execution slot and a triage conversation. Its inputs are the requirements, the test cases to assess, and the relevant source files. For each test case it reports traceability to the requirement, acceptance criterion and code components, then assesses whether business intent, test intent and code actually agree. It evaluates path feasibility, listing reachable paths, blocking conditions and boundary risks. It then predicts pass, fail and indeterminate likelihood with a confidence level, ranks the potential reasons for failure with supporting evidence, and recommends one of three actions: Execute, Defer or Refine. Testers and automation engineers use it before committing to a full regression cycle, refining the tests it flags instead of running them and triaging the fallout. Supplying the source code matters, because predictions without it fall back to comparing requirement against test alone and confidence drops accordingly. A Refine verdict usually indicates a real specification or test defect and is best treated as a work item rather than a warning to dismiss. For delivery managers the benefit is a shorter, more informative execution cycle; for QA it is evidence-backed reasons a test looks unsound rather than an opinion. The outcomes are less wasted execution time, fewer false failures reaching triage, and test defects caught before they are mistaken for product defects. It runs after test design and before or alongside execution in the pipeline.

Predictive Intelligence compares three things that are usually reviewed separately — the **requirement**, the **test case** written for it, and the **source code** meant to implement it — and reasons about whether that test can actually succeed.

**What you give it:** requirements, the test cases to assess, and the relevant source files.

**What you get back**, per test case:

| Output | Description |
|---|---|
| **Traceability** | The requirement, acceptance criterion and code components the test maps to |
| **Intent alignment** | Whether business intent, test intent and code agree — aligned, partial or misaligned |
| **Path feasibility** | Reachable paths, blocking conditions and boundary risks |
| **Outcome prediction** | Pass / fail / indeterminate likelihood, with a confidence level |
| **Potential failure reasons** | Ranked, each with supporting evidence |
| **Recommended action** | **Execute**, **Defer** or **Refine** — with the rationale |

## Why it matters

Test execution is expensive, and a large share of failures are not product defects at all — they are tests that were never going to pass, because the test contradicts the requirement or the code does not implement the path the test assumes. Those failures still consume an execution slot and a triage conversation.

Typical use:

- **Pre-execution triage** — refine the tests flagged *Refine* before burning a full regression cycle on them
- **Test quality assurance** — find misalignment between requirement, test and implementation while it is still cheap to fix
- **Execution prioritisation** — run the tests that will tell you something, defer the ones that won't
- **Review support** — give a reviewer evidence-backed reasons a test looks unsound, rather than an opinion

The business outcome is less wasted execution time, fewer false failures reaching triage, and test defects caught before they are mistaken for product defects.

## In the UI

<!-- SCREENSHOT: predictive-01-dashboard.png — Prediction summary across a test set with confidence levels -->
*Predicted outcomes across a test set, with confidence.*

<!-- SCREENSHOT: predictive-02-detail.png — Per-test detail: intent alignment, failure reasons, recommended action -->
*Per-test detail — alignment, ranked failure reasons and recommended action.*

## Tips

- **Supply the source code.** Predictions without code context fall back to requirement-versus-test comparison only, and confidence drops accordingly.
- **Treat *Refine* as a work item**, not a warning to dismiss — it usually indicates a genuine specification or test defect.
- **Run it after [Test Reviewer](test-reviewer.md).** Policy gaps are cheaper to fix first; prediction is most useful on a suite that already passes basic hygiene.

[← Back to agents](index.md)
