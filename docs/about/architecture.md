# Architecture

## Service map

```mermaid
flowchart TD
  Browser[Browser<br/>Next.js 16 · React 19]
  BE[Common Backend<br/>Express 5 · :3001]
  DB[(PostgreSQL<br/>pipeline_runs<br/>agent_outputs<br/>integrations)]
  Browser -->|Bearer JWT| BE
  BE --> DB
  BE -->|per-tenant LLM injected| A1[DeepSpeci :8000]
  BE --> A2[CaseGeni :8001]
  BE --> A3[Auto-PlayPilot :8002]
  BE --> A4[Other Agents :8003]
  BE --> A5[Secure-Xi :8004]
  BE --> A6[Accessibility :8005]
  BE --> A7[Game-Xi :8006]
  BE --> A8[Perf-Xi :8008]
  BE --> A9[Knowledge Base :8009]
  BE --> A10[RIA :8010]
  BE --> A11[Defect Intelligence :8011]
```

## Request flow

1. Browser calls `/api/...` on Common Backend with a Bearer JWT
2. Backend resolves the tenant's encrypted LLM config (AES-256-GCM `v1:iv:tag:ct`)
3. Backend decrypts in-process and merges into the upstream agent request
4. Agent streams progress via SSE → backend proxies back to browser
5. Final result is persisted to `agent_outputs` and the pipeline run record is updated

Raw API keys never reach the browser.

## Frontend cache model

| Layer | Lives in | Purpose |
|---|---|---|
| `pipelineDataCache` (memory) | Page session | Hot reads for components |
| Backend (`pipeline_runs`, `agent_outputs`) | PostgreSQL | Source of truth — survives reloads |
| `sessionStorage.pipelineContext` | Tab | Current `pipelineRunId` |

`hydrateProjectFromBackendAsync()` reconciles on every project/pipeline mount, with per-runId guards to preserve optimistic local writes (e.g. just-validated outputs).

## Pipeline dependencies (frontend-enforced)

```
deepspeci → casegeni → auto-playpilot → defect-intelligence
                    ↘ datageni
                    ↘ test-reviewer
```

Independent agents (Secure-Xi, Perf-Xi, Accessibility, Visual Detector, Game-Xi, Payments-Rail) have no upstream requirement.
