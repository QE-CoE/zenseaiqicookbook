# DeepSpeci

> **Requirement Refinement Agent** — turns raw, ambiguous requirements into structured user stories with ambiguities surfaced for human review.

| | |
|---|---|
| **Port** | `8000` |
| **Stack** | Python · FastAPI · LangGraph |
| **Stage** | Requirements & Specs |
| **Downstream** | CaseGeni, Payments Rail QE |
| **Source** | `agents/deepspeci/` |

## What it does

DeepSpeci helps teams turn the documents delivery actually starts from — business requirements documents, technical specifications, Jira backlogs, meeting notes and rough epics — into structured, agreed user stories. It reads the source material, determines what kind of document it is, and routes it through the appropriate refinement path, because a technical specification needs decomposing while an epic simply needs stories written. As it works, it surfaces the ambiguities, missing information and contradictions that would otherwise be discovered much later by a developer or a tester. Business analysts and product owners typically use it during discovery, backlog refinement and change analysis, editing the output in place before approving it. Inputs can be pasted text, uploaded documents including Word files, diagrams and images embedded in those documents, or a connected Jira or qTest estate. Outputs are refined stories in a consistent *As a / I want / So that* form, explicit Given/When/Then acceptance criteria, flagged ambiguities, optional non-functional notes, and a Requirements Traceability Matrix. Where a Knowledge Base is connected, refinement uses your own domain terminology rather than generic phrasing, which noticeably reduces the editing a reviewer has to do. Teams migrating an existing backlog can pull it in, improve it, and push the result back to Jira or qTest. Because everything downstream depends on requirement quality, effort spent here is what prevents rework in test design, automation and impact analysis. For delivery managers the practical benefit is fewer clarification cycles mid-sprint and more predictable estimates. DeepSpeci is the usual entry point to the ZenseAI.QI pipeline, and its validated output is what unlocks CaseGeni and the agents beyond it.

DeepSpeci ingests one of:

- Free-text requirement (paste or upload `.txt`/`.md`/`.docx`)
- Jira ticket or an existing qTest estate (via integration)
- Confluence page (via integration)
- A document containing diagrams and images — these now contribute to refinement rather than being skipped

…and produces a **refined story set** with:

- Clear **As a / I want / So that** statements
- Explicit **acceptance criteria** (Given/When/Then)
- **Ambiguity callouts** — phrases that need clarification before tests can be designed
- Optional **non-functional notes** (perf, security, accessibility hints)
- A **Requirements Traceability Matrix** linking stories back to their source

### Document types

DeepSpeci classifies what you gave it and routes it accordingly, because a specification is not an epic:

| Document type | How it is handled |
|---|---|
| **Business Requirements Document** | Full refinement pipeline — extract, refine, generate stories |
| **Technical Specification** | Decomposed into implementation areas, then discrete requirements, then stories |
| **Epic / user story** | Direct story generation, skipping the extraction stage |

### Knowledge Base grounding

Any pipeline can be grounded in the [Knowledge Base](knowledge-base.md), so refinement uses your domain language rather than generic phrasing. Grounding reads **exact Knowledge Base content** rather than approximate matches, which materially improves terminology accuracy on domain-heavy requirements.

A **Knowledge Base lock** pins the selected sources for the duration of a run, so a long extraction cannot drift if someone updates a collection mid-flight. Long extractions are cancellable.

## Why it matters

Ambiguous requirements are the #1 cause of brittle test cases. Surfacing the ambiguity *before* CaseGeni runs prevents 30-40% of test rework downstream.

Typical use:

- **Backlog refinement** — turn a raw requirement into stories a team can estimate
- **Specification rescue** — make a Technical Specification usable as a story backlog instead of shelf-ware
- **Migration** — pull an existing Jira or qTest estate in, refine it, and push the result back
- **Traceability** — produce the matrix an audit will ask for, as a by-product rather than a project

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
- **LLM choice matters.** For long requirements (>4k tokens), prefer a long-context model such as Gemini 2.5 Pro or Claude Sonnet.
- **Ground it in the Knowledge Base** for domain-heavy work — the difference in terminology accuracy is significant.

## What's new

- **July 2026** — **v2**: document-type classification, Technical Specification decomposition, Jira/qTest migration, multimodal pipeline, unified integration experience and Requirements Traceability Matrix. Global Knowledge Base grounding with source locking and cancellable extraction. Security hardening with pipeline state retention.
- **May 2026** — Streaming stage names made human-readable; "tool_call" → "Extracting actors", etc.
- **April 2026** — DOCX upload supported.
- **March 2026** — Jira integration via Common Backend's per-tenant credentials.

[← Back to agents](index.md)
