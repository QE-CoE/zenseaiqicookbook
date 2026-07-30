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

Defect Intelligence solves the triage problem that follows every large test run. A five-hundred-test suite reporting thirty failures typically contains only four to six genuine underlying defects, but establishing that by hand costs an experienced tester hours of reading stack traces. The agent ingests an Auto-PlayPilot run report and performs that consolidation automatically. Its input is the execution report and normalised summary produced by the execution stage, so no separate setup is needed. It categorises each failure, clusters duplicates by fingerprinting the stack and assertion shape, and proposes a probable root cause for each cluster in plain language against the matching code or test line. It also suggests a fix path, distinguishing a selector problem, a wait condition, a test data issue, or a genuine product defect. Testers and automation engineers use it immediately after execution, while delivery managers use its output to answer whether a wall of red represents one problem or thirty. That distinction is what makes a go or no-go decision defensible rather than instinctive. Separating genuine regressions from environmental noise also protects the team's trust in the suite, which is usually the first thing to erode. Validating its output passes the clustered failures to Knowledge Graph, so defect history becomes part of the traceability model rather than being lost. The outcomes are triage effort reduced from hours to minutes, and release decisions based on the number of real defects rather than the number of failed tests. Defect Intelligence sits immediately after execution in the pipeline and feeds the traceability and impact stages beyond it.

Ingests an Auto-PlayPilot run report and produces:

- **Failure category** — `flaky` / `regression` / `env` / `data` / `selector-drift` / `assertion-mismatch`
- **Duplicate clusters** — fingerprinted by stack + assertion shape
- **Suggested root cause** — explained in plain language with the matching code/test line
- **Suggested fix path** — selector, wait condition, test data, or product defect

## Why it matters

A 500-test suite with 30 failures usually has 4-6 *actual* underlying bugs. Defect Intelligence shows you that clustering so triage takes minutes, not hours.

Typical use:

- **Failure triage** — turn a wall of red into a handful of real problems, ranked
- **Flaky-test identification** — separate genuine regressions from environmental noise, so trust in the suite holds
- **Root cause acceleration** — arrive at the failing line with an explanation rather than starting from a stack trace
- **Release decisions** — answer "are these 30 failures one problem or thirty?" before a go/no-go call

The business outcome is triage effort cut substantially, and release decisions made on the number of real defects rather than the number of red tests.

## In the UI

<!-- SCREENSHOT: defect-intel-01-input.png — Run report selector -->
<!-- SCREENSHOT: defect-intel-02-clusters.png — Failures clustered with category badges -->
<!-- SCREENSHOT: defect-intel-03-root-cause.png — Per-cluster root cause panel with suggested fix -->

## Tips

- **Feed it the Auto-PlayPilot run report directly** — the normalised summary carries the detail clustering depends on.
- **Validate the output** to pass clustered failures downstream to [Knowledge Graph](knowledge-graph.md) for traceability.

[← Back to agents](index.md)
