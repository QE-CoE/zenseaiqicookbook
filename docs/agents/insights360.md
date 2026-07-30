# Insights360

> **Quality Observability** — quality insights, trends and agent usage across the whole engineering lifecycle, in one dashboard.

| | |
|---|---|
| **Stack** | Next.js (platform surface, no upstream service) |
| **Stage** | Platform |
| **Upstream** | All agents — reads persisted pipeline runs and agent outputs |
| **Source** | `frontend/src/app/(dashboard)/analytics/` |

## What it does

Insights360 exists to answer the question that ultimately decides whether an accelerator programme continues: is it actually being used, and is it delivering? It reads what the platform has already recorded — every pipeline run, every agent output — and presents that as management information. There is nothing to configure and no separate run to trigger, which is what keeps the reporting honest: it reflects work that genuinely happened rather than figures somebody assembled. Its inputs are the persisted pipeline runs and agent outputs already held by the platform, and its outputs are dashboards and trends rather than a generated artefact. Delivery managers, QE leads and CoE owners are the primary audience, and it is reachable both from the main navigation and from the agent catalogue. Views span an executive summary of quality posture, platform-level reporting on Knowledge Base health, agent adoption and pipeline efficiency, and dedicated per-agent breakdowns for the most heavily used agents. Typical uses are adoption reporting, evidencing change in cycle time and coverage since rollout, deciding which agents merit further enablement on an account, and tracking whether quality is improving release over release. Filtering by project or sector makes it straightforward to report to a specific business unit rather than presenting an undifferentiated total. Because it reflects only persisted runs, a run abandoned before completion will not appear in the trends, which is worth knowing when a figure looks lower than expected. For QE leads the benefit is answering an adoption question with evidence rather than anecdote; for engineering teams it identifies where enablement effort would actually pay back. The outcome is a defensible view of accelerator value produced without anyone maintaining a spreadsheet, since the reporting derives from the same records the pipeline already writes.

Insights360 reads what the platform has already recorded — every pipeline run, every agent output — and presents it as management information. There is nothing to configure and no separate run to trigger.

**Overview**

- **Executive summary** — quality posture at a glance, filterable by project and sector

**Platform**

- **Knowledge Base health** — coverage, ingestion status and retrieval quality
- **Agent usage** — which agents are actually being used, by whom, how often
- **Pipeline efficiency** — cycle time and throughput across pipeline runs

**Per-agent views**

Dedicated breakdowns for DeepSpeci, CaseGeni, Secure-Xi, Perf-Xi, Game-Xi, Defect Intelligence and Auto-PlayPilot.

## Why it matters

Adoption is the hard part of any accelerator programme. Insights360 answers the questions a delivery or CoE lead actually gets asked:

- **Adoption reporting** — are teams using the agents we rolled out, or reverting to old habits?
- **Value evidence** — what has changed in cycle time and coverage since adoption, with numbers behind it
- **Investment decisions** — which agents earn their keep on this account and which need enablement
- **Quality trending** — is quality improving release over release, or are we holding steady?

The business outcome is a defensible view of accelerator value without anyone assembling a spreadsheet — the reporting comes from the same records the pipeline already writes.

## In the UI

Reachable from **Insights360** in the main navigation, and from the agent catalogue.

<!-- SCREENSHOT: insights360-01-executive-summary.png — Executive summary with project and sector filters -->
*Executive summary — filterable by project and sector.*

<!-- SCREENSHOT: insights360-02-agent-usage.png — Agent usage analytics -->
*Agent usage — adoption across the catalogue.*

<!-- SCREENSHOT: insights360-03-kb-health.png — Knowledge Base health and coverage -->
*Knowledge Base health and coverage.*

<!-- SCREENSHOT: insights360-04-pipeline-efficiency.png — Pipeline cycle time and throughput -->
*Pipeline efficiency — cycle time and throughput trends.*

## Tips

- **Filter by sector** when reporting to a specific business unit — the dashboard respects the active sector selection.
- **Insights360 is read-only.** It reflects persisted pipeline runs, so a run abandoned before completion will not appear in the trends.

## What's new

- **June 2026** — Executive summary reworked; Knowledge Base health and agent usage views added.

[← Back to agents](index.md)
