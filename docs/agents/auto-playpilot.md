# Auto-PlayPilot

> **Test Automation Agent** — generates Playwright test scripts and executes them headlessly via the Model Context Protocol (MCP).

| | |
|---|---|
| **Port** | `8002` |
| **Stack** | Node · Express · TypeScript · Playwright · MCP |
| **Stage** | Automation |
| **Upstream** | CaseGeni (validated) |
| **Downstream** | Defect Intelligence |
| **Source** | `agents/auto-playpilot/autopilot-ui/` |

## What it does

Auto-PlayPilot has **three execution modes**:

### 1. Framework Scripts
Scaffolds a brand-new Playwright project — `package.json`, `playwright.config.ts`, page objects, fixtures, CI config — from the validated CaseGeni bundle. Output is a zip you can clone into any repo.

### 2. Test Script Generation <span class="whatsnew">renamed May 2026</span>
Generates **just the test scripts** — either targeting a fresh framework or merging into an **existing project** that you upload as a zip or connect via Git URL. The agent inspects the project's existing page objects / utilities and generates scripts that match the local conventions.

### 3. Execution
Runs the generated suite headlessly using Playwright MCP, streaming step-by-step progress and producing a full run report (HTML + JSON + trace files).

## Why it matters

Auto-PlayPilot collapses **"design → script → run → report"** into one stream. No swivel-chair between Test Studio, an IDE, and the CI dashboard.

## In the UI

<!-- SCREENSHOT: auto-playpilot-01-mode-landing.png — Three-mode landing tiles -->
*Pick a mode from the landing screen.*

<!-- SCREENSHOT: auto-playpilot-02-test-script-config.png — Test Script Generation config: upload project / Git URL -->
*Test Script Generation — upload your project or paste a Git URL.*

<!-- SCREENSHOT: auto-playpilot-03-generation-stream.png — Live generation: file-by-file emission -->
*Watch each spec file emerge as the agent writes it.*

<!-- SCREENSHOT: auto-playpilot-04-run-report.png — Single run report (after duplicate-row fix) -->
*One run, one report — the May 2026 fix removed the phantom save-config row.*

<!-- SCREENSHOT: auto-playpilot-05-execution-trace.png — Playwright trace viewer linked from the run report -->
*Per-step trace, screenshot, and DOM snapshot via Playwright trace viewer.*

## Tips

- **Existing project mode** works best when your `playwright.config.ts` and at least one page object already exist — the agent learns conventions from those.
- **MCP execution** runs inside the agent's sandbox; secrets in your test config are not exfiltrated.
- The **run report** is browsable offline — download the zip from the workspace once execution finishes.

## What's new

- **May 2026** — "Test Script Generation (Existing Framework)" label simplified to **"Test Script Generation"**; description clarifies it covers fresh frameworks and existing-project uploads.
- **May 2026** — **Fixed**: `save-config` no longer creates a phantom `AgentOutput` row → exactly one report per generation.
- **April 2026** — Existing-project Git URL connection via the Common Backend's encrypted integration store.

[← Back to agents](index.md)
