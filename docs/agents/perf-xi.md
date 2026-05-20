# Perf-Xi

> **Performance Testing Agent** — synthesises load-test plans and explains bottlenecks.

| | |
|---|---|
| **Port** | `8008` |
| **Stack** | Python · FastAPI |
| **Stage** | Specialised — independent |
| **Source** | `agents/perf-xi/` |

## What it does

From an OpenAPI spec or a recorded user journey:

- Generates **k6 / Locust** load scripts
- Recommends ramp profile (users, spawn rate, duration) for your SLOs
- Runs the test (locally or against a target)
- Explains result: "p95 spiked at 280 concurrent users because the `/orders` endpoint serializes through a single DB connection"

## In the UI

<!-- SCREENSHOT: perf-xi-01-plan.png — Generated load plan + script preview -->
<!-- SCREENSHOT: perf-xi-02-results.png — Run result charts -->
<!-- SCREENSHOT: perf-xi-03-bottleneck.png — AI explanation of bottleneck -->

[← Back to agents](index.md)
