# DeepSpeci

> **Requirement Refinement Agent** — turns raw, ambiguous requirements into structured user stories with ambiguities surfaced for human review.

| | |
|---|---|
| **Port** | `8000` |
| **Stack** | Python · FastAPI · LangGraph |
| **Stage** | Requirements & Specs |
| **Downstream** | CaseGeni, Payments-Rail |
| **Source** | `agents/deepspeci/` |

## What it does

DeepSpeci ingests one of:

- Free-text requirement (paste or upload `.txt`/`.md`/`.docx`)
- Jira/Azure DevOps ticket link (via integration)
- Confluence page (via integration)

…and produces a **refined story set** with:

- Clear **As a / I want / So that** statements
- Explicit **acceptance criteria** (Given/When/Then)
- **Ambiguity callouts** — phrases that need clarification before tests can be designed
- Optional **non-functional notes** (perf, security, accessibility hints)

## Why it matters

Ambiguous requirements are the #1 cause of brittle test cases. Surfacing the ambiguity *before* CaseGeni runs prevents 30-40% of test rework downstream.

## In the UI

<!-- SCREENSHOT: deepspeci-01-input.png — DeepSpeci workspace, input panel with free-text requirement -->
*Workspace input panel.*

<!-- SCREENSHOT: deepspeci-02-streaming.png — Streaming progress: "Parsing requirement…", "Extracting actors…", "Generating stories…" -->
*Live streaming progress while the LangGraph plan executes.*

<!-- SCREENSHOT: deepspeci-03-refined-stories.png — Refined stories with acceptance criteria and ambiguity callouts highlighted in amber -->
*Refined stories — ambiguities highlighted for resolution before Validate.*

<!-- SCREENSHOT: deepspeci-04-validate.png — Validate button + status flipping to "Validated" -->
*Validate output to unlock CaseGeni downstream.*

## Tips

- **Edit before validating.** DeepSpeci output is editable in-place; updates persist via `PATCH /agent-outputs/:id/data`.
- **One requirement at a time.** Splitting a 20-story epic into 4 runs gives noticeably cleaner CaseGeni results downstream.
- **LLM choice matters.** For long requirements (>4k tokens), prefer Gemini Pro or Claude Sonnet over GPT-4o-mini.

## What's new

- **May 2026** — Streaming stage names made human-readable; "tool_call" → "Extracting actors", etc.
- **April 2026** — DOCX upload supported.
- **March 2026** — Jira integration via Common Backend's per-tenant credentials.

[← Back to agents](index.md)
