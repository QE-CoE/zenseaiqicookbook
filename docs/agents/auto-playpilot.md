# Auto-PlayPilot

> **Test Automation Agent** — scaffolds automation frameworks, generates test scripts, and executes them against a live application.

| | |
|---|---|
| **Port** | `8002` |
| **Stack** | Node · Express · TypeScript · Playwright · MCP |
| **Stage** | Automation |
| **Upstream** | CaseGeni (validated) |
| **Downstream** | Defect Intelligence |
| **Source** | `agents/auto-playpilot/autopilot-ui/` |

## What it does

Auto-PlayPilot closes the gap between having test cases and having something that actually runs. Building an automation framework from scratch is a multi-week engineering exercise, and writing scripts that match an existing project's conventions requires familiarity most teams cannot spare. Automation engineers are the primary users, though testers use the execution mode routinely as part of a normal delivery cycle. Inputs are validated test cases together with your framework or repository; outputs are runnable project files, an HTML report, an execution log and a normalised run summary. The four modes below cover scaffolding a framework, generating scripts into a new or existing project, executing the suite against a live application, and converting existing scripts between languages and frameworks. Script generation inspects the target project first, auto-detecting framework and language so the output follows your local patterns rather than imposing new ones. Execution discovers spec and feature files from a generated project and lets you select tests by file, suite or tag, with a headed or headless run. Typical scenarios are a team automating from a standing start, a team extending an existing suite without breaking its conventions, and routine execution feeding triage. For engineering the benefit is weeks of framework setup reduced to a guided generation step; for QA it is scripts that match the suite they were designed from. The outcome is design, scripting, execution and reporting collapsed into one stream instead of a swivel between a test tool, an IDE and a CI dashboard. Execution results flow directly into Defect Intelligence, making Auto-PlayPilot the bridge between test design and quality analysis.

Auto-PlayPilot has **four modes**:

### 1. Framework and Script Generation
Scaffolds a complete, production-ready automation framework from scratch, configured for your stack, language and CI/CD pipeline — page objects, fixtures, utilities and pipeline configuration for GitHub Actions, Azure DevOps or Jenkins. Playwright and Selenium are supported, with optional BDD/Cucumber structure. Output is a project you can clone into any repository.

### 2. Test Script Generation <span class="whatsnew">renamed May 2026</span>
Generates **just the test scripts** — either targeting a fresh framework or merging into an **existing project** that you upload as a zip or connect via a Git repository (GitHub, Azure DevOps, GitLab or Bitbucket). The agent auto-detects framework and language, then generates scripts that match your local conventions.

### 3. Test Execution
Runs the generated suite against a live application using the native Playwright CLI, with a headed/headless toggle. Discovers spec and feature files from a generated project, lets you select tests by file, suite or `@tag`, and produces an HTML report, execution log and normalised summary — which feed straight into [Defect Intelligence](defect-intelligence.md).

### 4. Test Code Conversion
Converts existing test scripts between languages (TypeScript, Java, Python, C#) and frameworks (Playwright, Selenium, Cypress), preserving page-object structure and assertions.

!!! note "Not yet enabled"
    Test Code Conversion appears in the mode picker but is not available in the current release — see [July 2026 known limitations](../releases/2026-07.md#known-limitations).

## Why it matters

Auto-PlayPilot collapses **"design → script → run → report"** into one stream. No swivel-chair between Test Studio, an IDE, and the CI dashboard.

Typical use:

- **Automation from a standing start** — a team with no framework gets a working, CI-wired one
- **Extending an existing suite** — generate scripts that match conventions your team already follows
- **Execution and triage** — run, report, and pass failures to Defect Intelligence without leaving the workspace

## In the UI

<!-- SCREENSHOT: auto-playpilot-01-mode-landing.png — Four-mode landing tiles -->
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
- **Execution** runs inside the agent's sandbox; secrets in your test config are not exfiltrated.
- The **run report** is browsable offline — download the zip from the workspace once execution finishes.
- **Select by `@tag`** to run a focused subset rather than the whole discovered suite.
- **DataGeni fixtures** can be previewed against the generated suite, so data and scripts are checked together before a run.

## What's new

- **July 2026** — Framework generation and pipeline configuration corrected; sample repository configuration loads properly; test-execution fixes.
- **June 2026** — Test Execution added to the End-to-End QA Pipeline template; single-select test type and uniform mobile configuration UI; browser dependencies pre-installed at generation time so runs no longer stall on downloads. **Fixed**: execution runs no longer overwrite generation output, and phantom pipeline runs are gone.
- **May 2026** — "Test Script Generation (Existing Framework)" label simplified to **"Test Script Generation"**; description clarifies it covers fresh frameworks and existing-project uploads.
- **May 2026** — **Fixed**: `save-config` no longer creates a phantom `AgentOutput` row → exactly one report per generation.
- **April 2026** — Existing-project Git URL connection via the Common Backend's encrypted integration store.

[← Back to agents](index.md)
