# Impact Analyzer

> **Change Impact Agent** — takes a change request and tells you which existing tests it affects, where coverage is missing, and what new tests are needed.

| | |
|---|---|
| **Port** | `8015` |
| **Stack** | Python · FastAPI |
| **Stage** | Quality Intelligence |
| **Upstream** | Knowledge Graph (relations), Knowledge Base (optional grounding) |
| **Source** | `agents/impact-analyzer/` |

## What it does

Impact Analyzer answers the question every change request raises: what does this break, and what have we not tested? Today that assessment is usually manual and experience-dependent — a senior tester reads the change and recalls which suites to re-run. That judgement is slow, difficult to hand over, and quietly incomplete, because the tests nobody remembered simply do not get run. Users describe the change in plain English and optionally scope it to particular Knowledge Base collections. The agent returns the existing test cases the change affects, each with a prioritised rank and the requirement it traces back to, plus an impact classification so high-consequence items surface first. It also identifies the coverage gaps the change introduces and drafts new test cases to close them, with summary statistics across the impacted set and export options for both lists. Impact reasoning runs against the Knowledge Graph, so the agent follows real relationships from change to business capability to user story to test case, rather than matching on keywords. Testers, business analysts and product owners use it for change-request triage, regression scoping and coverage assurance before committing to a sprint. Because the graph underpins the ranking, building it first is a genuine prerequisite rather than a recommendation. Exporting the impacted set gives the change record an audit trail explaining why a particular regression scope was chosen. For delivery managers the benefit is a defensible scope decision in minutes instead of an afternoon of expert guesswork. The outcomes are fewer regressions escaping because a dependency was overlooked, and an impact answer a new team member can reproduce as reliably as someone who has been on the account for years.

Describe a change in plain English — *"add two-factor authentication to the login flow"* — and Impact Analyzer works out what that change means for the test estate.

**What you give it:** a change request in free text, optionally scoped to one or more Knowledge Base collections.

**What you get back:**

| Output | Description |
|---|---|
| **Impacted test cases** | Existing tests the change affects, each with a **prioritised rank** and the requirement it traces back to |
| **Impact classification** | How each test is affected, so high-consequence items surface first |
| **Coverage gaps** | Areas the change introduces that no current test exercises |
| **Generated test cases** | New tests drafted to close the identified gaps |
| **Summary statistics** | Counts and distribution across the impacted set |

Impact reasoning runs against the [Knowledge Graph](knowledge-graph.md), so the agent follows real relationships — change → business capability → user story → test case → defect — rather than matching on keywords.

## Why it matters

Impact assessment is normally a manual, experience-dependent exercise: a senior tester reads a change request and works from memory which suites to re-run. That judgement is slow, hard to hand over, and quietly incomplete — the tests nobody remembered simply don't get run.

Impact Analyzer makes the assessment explicit and repeatable. Typical use:

- **Change-request triage** — size the testing effort before committing to a sprint
- **Regression scoping** — re-run the tests that matter instead of the whole suite, or everything someone can recall
- **Coverage assurance** — show an auditor or release board which tests cover a change, and where the gaps were closed
- **Handover** — a new team member gets the same impact answer as the person who has been on the account for three years

The business outcome is a defensible, evidence-backed scope decision in minutes, and fewer regressions that escape because a dependency was overlooked.

## In the UI

<!-- SCREENSHOT: impact-analyzer-01-input.png — Change request input with Knowledge Base scope selector -->
*Enter the change request and choose the Knowledge Base scope.*

<!-- SCREENSHOT: impact-analyzer-02-summary.png — Summary tab with impact statistics -->
*Summary — impact distribution across the existing suite.*

<!-- SCREENSHOT: impact-analyzer-03-impacted-tests.png — Impacted tests ranked by priority with linked requirements -->
*Impacted tests, ranked, each linked back to its requirement.*

<!-- SCREENSHOT: impact-analyzer-04-new-tests.png — Generated test cases closing coverage gaps -->
*Generated tests covering the gaps the change introduces.*

## Tips

- **Build the Knowledge Graph first.** Impact quality depends directly on graph completeness — run [Knowledge Graph](knowledge-graph.md) over your requirements and test estate before relying on the rankings.
- **One change per run.** A change request bundling four unrelated changes produces a diluted ranking; splitting them gives sharper priorities.
- **Export the impacted set** to attach to the change record — it is the audit trail for why a given regression scope was chosen.

## What's new

- **July 2026** — Prioritised ranking, reworked impact classification, Impacted Tests redesigned to match the New Tests layout, improved relevance scoring and persistence across navigation.
- **June 2026** — Agent introduced, with tree view, summary tab, generated-test view and export options.

[← Back to agents](index.md)
