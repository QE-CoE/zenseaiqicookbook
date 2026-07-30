# Perf-Xi

> **Performance Testing Agent** — designs the workload, generates the scripts, and analyses the results, across three modes.

| | |
|---|---|
| **Port** | `8008` |
| **Stack** | Python · FastAPI |
| **Stage** | Specialised — runs independently of upstream agents |
| **Source** | `agents/perf-xi/` |

## What it does

Perf-Xi addresses the two ways performance testing usually fails to deliver value. Either the workload model is invented rather than derived, so the test proves nothing about real behaviour, or the results arrive as charts that nobody can convert into an action. Performance engineers are the primary users, and the agent covers the full lifecycle from modelling the load, through generating the scripts, to analysing what a completed run actually means. Workload Modeling produces a defensible view of expected load, derived either from a business requirements document when there is no traffic history, or from real traffic where production data exists. Script Automation converts a journey definition into a tool-specific bundle for the major load-testing tools, with the script logic previewed for approval before anything is generated. The Anomaly Detection Engine works in the opposite direction, taking a completed run and explaining it: it ingests results together with application and infrastructure metrics, detects anomalies, correlates them, and performs root-cause analysis with confidence scoring. Inputs across the three modes span requirements documents, APM exports, log files, API specifications, UI flows, live captures, and completed test results. Outputs span workload models with concurrency and throughput figures, runnable script bundles, and prioritised remediation recommendations with a performance health score. Typical scenarios are pre-launch capacity validation, refreshing a model once production traffic exists, accelerating scripting work, and triaging a run that regressed. Correlation across application, infrastructure and database metrics is where root cause genuinely emerges, so supplying more than just the results materially improves the answer. For architecture and engineering teams the outcome is performance findings that survive scrutiny in a design review; for delivery managers it is remediation that starts with the highest-impact issue rather than the most visible one. Perf-Xi runs independently of the requirement pipeline.

Perf-Xi covers the performance lifecycle in **three modes**, chosen from the workspace landing screen.

### 1. Workload Modeling

Builds a defensible workload model — the part teams most often guess at.

- **Greenfield** — derive the model from a Business Requirements Document when there is no production traffic to learn from
- **Brownfield** — derive it from real traffic, using APM exports or log files

Either path extracts user journeys, non-functional requirements and transactions, then produces TPS bands, concurrency figures, peak and idle hours, a persona model, load shape and test scenarios.

### 2. Script Automation

Converts a journey definition into a tool-specific performance script bundle.

- Input from a **web app capture**, an API specification, or a UI flow
- **Recording Studio** captures a live user journey directly <span class="whatsnew">new July 2026</span>
- Output for **JMeter, k6, Gatling or Locust**
- Script logic is previewed for approval before generation
- Generated files download as a bundle

### 3. Anomaly Detection Engine <span class="whatsnew">new July 2026</span>

Analyses a completed test run instead of designing a new one. Upload performance results, APM exports and infrastructure or database metrics, and it returns:

- **Anomaly detection**, with validation of the ingested data
- **Correlation and root-cause analysis**, with confidence scoring
- **Prioritised recommendations**
- A **performance health score**

Accepts JTL, APM, infrastructure and log inputs, and reasons across layers rather than assessing each metric alone.

## Why it matters

Performance testing fails in two predictable ways: the workload model is invented rather than derived, so the test proves nothing; or the results arrive as charts nobody can convert into an action.

Perf-Xi addresses both ends. Typical use:

- **Pre-launch capacity validation** — model load for a system with no traffic history yet
- **Workload refresh** — rebuild the model from real traffic once production data exists
- **Scripting acceleration** — turn a journey into a tool-specific script bundle without hand-coding
- **Post-run analysis** — get root cause and prioritised recommendations instead of raw charts
- **Regression triage** — identify what changed between two runs and why

The business outcome is performance results that survive scrutiny, and remediation that starts with the highest-impact finding rather than the most visible one.

## In the UI

<!-- SCREENSHOT: perf-xi-01-plan.png — Mode picker: Workload Modeling, Script Automation, Anomaly Detection -->
*Three modes — model the workload, generate scripts, or analyse a run.*

<!-- SCREENSHOT: perf-xi-02-results.png — Workload model output: TPS bands, concurrency, load shape -->
*Workload model — TPS bands, concurrency and load shape.*

<!-- SCREENSHOT: perf-xi-03-bottleneck.png — Anomaly Detection root cause analysis with health score -->
*Anomaly Detection — correlated root cause with a health score.*

<!-- SCREENSHOT: perf-xi-04-recording-studio.png — Recording Studio capturing a live user journey -->
*Recording Studio — capture a journey directly from the running application.*

## Tips

- **Prefer Brownfield when you have traffic.** A model derived from real usage beats one derived from a document every time.
- **Approve the script logic** before generating — reviewing the plan is far cheaper than reviewing generated scripts.
- **Feed the Anomaly Detection Engine everything you have.** Correlation across application, infrastructure and database metrics is where root cause actually emerges; results alone give a much weaker answer.

## What's new

- **July 2026** — Anomaly Detection Engine added as a third mode; Recording Studio added to Script Automation with a redesigned input page; Guidewire integration and workload concurrent-user consistency corrected.
- **June 2026** — Greenfield BRD path mode, TPS calculation and the MAU label corrected; Guidewire edge loader added.

[← Back to agents](index.md)
