# Knowledge Base

> **Platform RAG store** — pgvector-backed knowledge store that grounds every other agent in your domain, not generic training data.

| | |
|---|---|
| **Port** | `8009` |
| **Stack** | Python · FastAPI · PostgreSQL · pgvector |
| **Stage** | Platform |
| **Source** | `agents/knowledge/` |

## What it does

The Knowledge Base is what separates a generic assistant from one that understands your business. An ungrounded model writes plausible test cases in generic vocabulary; a grounded one uses your product names, your business rules and your terminology — the difference between output a reviewer rewrites and output they accept. It is the platform's retrieval store, and every other agent reads from it. Content arrives either as direct uploads or through connectors to the systems where your knowledge already lives, so it does not have to be re-authored to be useful. Everything ingested is chunked and embedded, normalised to a consistent storage dimension so retrieval behaves predictably across sources. Payment documentation receives specialised treatment, chunked by flow rather than by page so retrieval returns a complete payment flow instead of a fragment stopping mid-sequence — this is what makes Payments Rail QE grounding useful in practice. Sources are organised into collections that agents select at run time, with a global collection grounding every pipeline and project collections scoping retrieval to a single piece of work. Every chunk is scoped to a tenant, so isolation holds between clients on a shared deployment. Business analysts and delivery teams curate it, while every agent consumes it, making it the one component whose quality affects all others. Ingesting content before running a pipeline is essential, since grounding only helps if the material is already indexed, and the coverage view shows what actually indexed rather than what was submitted. The outcomes are domain-accurate output across every agent, institutional memory in Confluence and Jira that stays useful rather than going stale, and consistent domain understanding across teams and handovers.

- **Ingests** PDFs, Word documents, code files and crawled URLs, plus connector-backed sources
- **Connects** to **Jira**, **Confluence**, **GitHub** and **Azure AI Search** (including Guidewire estates)
- **Chunks and embeds** using a configurable embedding model, normalised to the storage dimension
- **Serves** semantic search to every agent — DeepSpeci for domain terminology, CaseGeni for comparable test cases, Payments Rail QE for payment flows, Defect Intelligence for prior failure patterns
- **Tenant-isolated** — every chunk is scoped to a tenant ID

### Payments-aware chunking

Payment documentation is chunked by **flow** rather than by page, so retrieval returns a whole payment flow instead of a fragment that stops mid-sequence. This is what makes [Payments Rail QE](payments-rail.md) grounding useful in practice.

### Knowledge collections

Sources are organised into collections that agents select at run time. A **global** collection grounds every pipeline; project collections scope retrieval to one piece of work.

## Why it matters

An ungrounded model writes plausible, generic test cases using generic vocabulary. A grounded one uses your product names, your business rules and your terminology — the difference between output a reviewer edits heavily and output they accept.

Typical use:

- **Domain grounding** — every agent speaks your language rather than the industry's
- **Institutional memory** — Confluence and Jira history stay useful instead of going stale
- **Consistency** — the same domain understanding applied across every agent and every team

## In the UI

<!-- SCREENSHOT: kb-01-upload.png — Document upload and connector setup with embedding model picker -->
<!-- SCREENSHOT: kb-02-search.png — Manual search + similarity scores -->
<!-- SCREENSHOT: kb-03-usage.png — Coverage and ingestion status across collections -->

## Setup

The Knowledge Base requires PostgreSQL with pgvector, provisioned by `install.sh` as a Podman container (`zenseai-knowledge-db`, port 5433).

```bash
# Knowledge Base requires PostgreSQL + pgvector.
# install.sh provisions both via Podman.
cd agents/knowledge && .venv/bin/uvicorn main:app --host 0.0.0.0 --port 8009 --reload
```

## Tips

- **Ingest before running the pipeline.** Grounding only helps if the content is already indexed.
- **Use a global collection for standards and terminology**, and project collections for requirement-specific material.
- **Check coverage** after ingestion — the upload classification and coverage view shows what actually indexed rather than what was submitted.

## What's new

- **July 2026** — Word document uploads unblocked with clearer error reporting; Azure AI Search connector context available to ZenRia.
- **June 2026** — Payments-aware chunking; LLM-assisted document ingestion; embeddings normalised to the storage dimension (3072); Jira, Confluence and Guidewire Azure AI Search connectors; upload classification and coverage reporting corrected.

[← Back to agents](index.md)
