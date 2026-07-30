---
hide:
  - navigation
  - toc
---

<div class="hero" markdown>

<span class="eyebrow">Zensar QE CoE · Release Hub</span>

# ZenseAI.QI { .hero-title }

AI-powered Quality Engineering. **19 specialised agents** orchestrated into one governed pipeline — from a raw requirement to an executed, validated, defect-classified test run.
{ .hero-lede }

[:material-rocket-launch: July 2026 release](releases/2026-07.md){ .md-button .md-button--primary }
[:material-graph: See the pipeline](workflows/end-to-end.md){ .md-button }
[:material-puzzle: Browse agents](agents/index.md){ .md-button }
{ .hero-ctas }

<span class="badge">:material-circle-medium: Multi-LLM routing</span>
<span class="badge">:material-circle-medium: SSE streaming</span>
<span class="badge">:material-circle-medium: Tenant-isolated</span>
<span class="badge">:material-circle-medium: Self-hostable</span>
<span class="badge">:material-circle-medium: OWASP-aligned</span>
{ .badges }

</div>

<div class="stats" markdown>
<div class="stat"><span class="stat__num">19</span><span class="stat__label">Specialised agents</span></div>
<div class="stat"><span class="stat__num">36</span><span class="stat__label">Pipeline templates</span></div>
<div class="stat"><span class="stat__num">21</span><span class="stat__label">Tool integrations</span></div>
<div class="stat"><span class="stat__num">AES-256</span><span class="stat__label">GCM-encrypted secrets</span></div>
</div>

<div class="band band--soft" markdown>

## One requirement in. A validated test run out. { .section-title }

ZenseAI.QI is a unified, multi-tenant accelerator that walks a software requirement through **every quality stage** — clarification, test-case generation, test-data synthesis, script generation, execution, defect triage, performance and security validation — using purpose-built AI agents that talk to each other through a typed, validated pipeline.
{ .section-lede }

<div class="grid cards pillars" markdown>

- :material-flash:{ .lg .middle } **Faster cycle time**

    ---

    From requirement to executed regression in hours, not sprints. Agents pass typed outputs — no copy-paste between tools.

- :material-shield-check:{ .lg .middle } **Governed by design**

    ---

    AES-256-GCM secrets, JWT auth, row-level tenant isolation, OWASP-aligned hardening. Pipeline runs are auditable end-to-end.

- :material-puzzle-plus:{ .lg .middle } **Composable agents**

    ---

    Pick the agents your project needs. Each has its own UI, evidence trail, and a standard contract for upstream / downstream.

- :material-brain:{ .lg .middle } **Bring your own LLM**

    ---

    Per-tenant routing across Gemini, OpenAI, Claude and Azure AI Foundry. Keys stay encrypted; raw secrets never reach the browser.

</div>

</div>

<div class="band" markdown>

## The pipeline at a glance { .section-title }

<div class="pipeline-wrap" markdown>

```mermaid
flowchart LR
  R([Requirement]):::input --> DS[DeepSpeci]:::core
  DS --> CG[CaseGeni]:::core
  CG --> DG[DataGeni]:::core
  CG --> APP[Auto-PlayPilot]:::core
  APP --> DI[Defect Intelligence]:::quality
  DI --> KG[Knowledge Graph]:::quality
  KG --> IA[Impact Analyzer]:::quality
  APP --> PI[Predictive]:::quality
  APP --> TO[Test Optimization]:::quality

  R -.-> SX[Secure-Xi]:::spec
  R -.-> PX[Perf-Xi]:::spec
  R -.-> AC[Accessibility]:::spec
  R -.-> PR[Payments-Rail]:::spec
  R -.-> GX[Game-Xi]:::spec
  R -.-> VX[Visual Xi]:::spec
  R -.-> DP[DocuProof]:::spec

  classDef input  fill:#FFF3E8,stroke:#C45412,stroke-width:2px,color:#C45412;
  classDef core   fill:#F37021,stroke:#C45412,color:#fff;
  classDef quality fill:#FFE0CC,stroke:#F37021,color:#C45412;
  classDef spec   fill:#FFFFFF,stroke:#F89561,color:#C45412,stroke-dasharray:4 3;
```

</div>

<p class="pipeline-caption">Solid arrows = mandatory dependencies. Dashed = independent specialised agents.</p>

<div class="band__cta" markdown>
[Walk the end-to-end workflow](workflows/end-to-end.md){ .md-button .md-button--primary }
[Read the architecture](about/architecture.md){ .md-button }
</div>

</div>

<div class="band band--soft" markdown>

## What's new in July 2026 <span class="whatsnew">latest</span> { .section-title }

<div class="grid cards news" markdown>

- :material-file-tree:{ .lg .middle } **DeepSpeci v2**

    ---

    Document-type classification, Technical Specification decomposition, Jira/qTest migration and a multimodal pipeline — specifications become a story backlog.

- :material-radar:{ .lg .middle } **Anomaly Detection Engine**

    ---

    Perf-Xi gains a third mode: ingest results, APM and infra metrics for correlated root-cause analysis, prioritised recommendations and a health score.

- :material-record-circle:{ .lg .middle } **Perf-Xi Recording Studio**

    ---

    Capture a live user journey directly and convert it into a JMeter, k6, Gatling or Locust script bundle.

- :material-format-list-checks:{ .lg .middle } **CaseGeni test-design uplift**

    ---

    Step-specific expected results, configurable story and AC limits, ADA test cases, and Excel/CSV exports that survive contact with a spreadsheet.

</div>

<div class="band__cta" markdown>
[Read full July 2026 notes](releases/2026-07.md){ .md-button .md-button--primary }
</div>

</div>

<div class="band" markdown>

## The agent catalogue { .section-title }

<div class="cat-row" markdown>

<span class="cat-pill cat-pill--req">Requirements &amp; Specs</span>

<div class="grid cards agents" markdown>

- :material-clipboard-text-search:{ .lg .middle } **[DeepSpeci](agents/deepspeci.md)**

    ---

    Turns ambiguous requirements into refined user stories with clarifying questions surfaced.

- :material-format-list-checks:{ .lg .middle } **[CaseGeni](agents/casegeni.md)**

    ---

    Generates structured positive, negative and edge-case tests from refined stories.

- :material-account-supervisor:{ .lg .middle } **[Test Reviewer](agents/test-reviewer.md)**

    ---

    Applies sector policy packs — REST API, BFSI, HIPAA — and flags coverage gaps before automation.

- :material-account-tie-voice:{ .lg .middle } **[RIA](agents/ria.md)**

    ---

    ZenRia — in-app assistant for platform guidance and conversational requirement intake.

</div>

</div>

<div class="cat-row" markdown>

<span class="cat-pill cat-pill--auto">Test Data &amp; Automation</span>

<div class="grid cards agents" markdown>

- :material-database-cog:{ .lg .middle } **[DataGeni](agents/datageni.md)**

    ---

    Synthesises rule-compliant test data with foreign-key integrity across entities.

- :material-robot-happy:{ .lg .middle } **[Auto-PlayPilot](agents/auto-playpilot.md)**

    ---

    Scaffolds frameworks, generates scripts, and executes them against a live application.

- :material-eye-check:{ .lg .middle } **[Visual Xi](agents/visual-detector.md)**

    ---

    Compares Figma designs against the live site and scores design compliance.

</div>

</div>

<div class="cat-row" markdown>

<span class="cat-pill cat-pill--qi">Quality Intelligence</span>

<div class="grid cards agents" markdown>

- :material-bug-check:{ .lg .middle } **[Defect Intelligence](agents/defect-intelligence.md)**

    ---

    Classifies failed runs, clusters duplicates, suggests root cause.

- :material-chart-bell-curve:{ .lg .middle } **[Predictive Intelligence](agents/predictive-intelligence.md)**

    ---

    Predicts pass, fail or inconclusive before execution — and whether to run, defer or refine.

- :material-tune-variant:{ .lg .middle } **[Test Optimization](agents/test-optimization.md)**

    ---

    Finds redundancy in an existing suite and merges duplicates without losing coverage.

- :material-graph:{ .lg .middle } **[Knowledge Graph](agents/knowledge-graph.md)**

    ---

    Neo4j-backed traceability across capabilities, stories, tests and defects.

- :material-source-branch-sync:{ .lg .middle } **[Impact Analyzer](agents/impact-analyzer.md)**

    ---

    Turns a change request into ranked impacted tests, coverage gaps and new tests.

</div>

</div>

<div class="cat-row" markdown>

<span class="cat-pill cat-pill--spec">Specialised Validators</span>

<div class="grid cards agents" markdown>

- :material-shield-lock:{ .lg .middle } **[Secure-Xi](agents/secure-xi.md)**

    ---

    OWASP / ASVS scan with AI-driven exploit reasoning.

- :material-speedometer:{ .lg .middle } **[Perf-Xi](agents/perf-xi.md)**

    ---

    Load-test plan synthesis and bottleneck explanation.

- :material-gamepad-variant:{ .lg .middle } **[Game-Xi](agents/game-xi.md)**

    ---

    Game accessibility against Xbox (XAG), industry (GAG) and IARC rating standards.

- :material-human-wheelchair:{ .lg .middle } **[Accessibility Intelligence](agents/accessibility.md)**

    ---

    Site-wide axe-core audit with AI remediation guidance.

- :material-credit-card-check:{ .lg .middle } **[Payments Rail QE](agents/payments-rail.md)**

    ---

    Rail-aware scenarios for ACH, FedNow, SWIFT and ISO 20022, with compliance packs.

- :material-file-compare:{ .lg .middle } **[DocuProof](agents/pdf-validator.md)**

    ---

    PDF comparison with smart exclusions for dates, prices and IDs.

</div>

</div>

<div class="cat-row" markdown>

<span class="cat-pill cat-pill--plat">Platform</span>

<div class="grid cards agents" markdown>

- :material-book-open-page-variant:{ .lg .middle } **[Knowledge Base](agents/knowledge-base.md)**

    ---

    pgvector-backed RAG store every agent reads from, with Jira, Confluence and GitHub connectors.

- :material-chart-box:{ .lg .middle } **[Insights360](agents/insights360.md)**

    ---

    Quality trends, agent adoption and pipeline efficiency across the lifecycle.

</div>

</div>

</div>

<div class="cta-band" markdown>

## Ready to put it to work? { .section-title }

Explore the workflows your team will run most often, then drill into the agents that power each step.
{ .section-lede }

[Requirement → Test](workflows/requirement-to-test.md){ .md-button .md-button--primary }
[Regression](workflows/regression.md){ .md-button .md-button--primary }
[Exploratory](workflows/exploratory.md){ .md-button .md-button--primary }
[Architecture deep-dive](about/architecture.md){ .md-button }
{ .hero-ctas }

</div>
