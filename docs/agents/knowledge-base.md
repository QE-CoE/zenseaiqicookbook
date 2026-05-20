# Knowledge Base

> **Platform RAG store** — pgvector-backed document store that every other agent reads from.

| | |
|---|---|
| **Port** | `8009` |
| **Stack** | Python · FastAPI · PostgreSQL · pgvector |
| **Stage** | Platform |
| **Source** | `agents/knowledge/` |

## What it does

- **Ingests** PDFs, DOCX, Confluence pages, Jira tickets, code files
- **Chunks + embeds** using a configurable embedding model
- **Serves** semantic search to other agents (DeepSpeci uses it to find prior similar requirements, CaseGeni for similar test cases, Defect Intelligence for prior failure patterns)
- **Tenant-isolated** — every chunk is scoped to a tenant ID

## In the UI

<!-- SCREENSHOT: kb-01-upload.png — Document upload with embedding model picker -->
<!-- SCREENSHOT: kb-02-search.png — Manual search + similarity scores -->
<!-- SCREENSHOT: kb-03-usage.png — Which agents have queried which documents recently -->

## Setup

```bash
# Knowledge Base requires PostgreSQL + pgvector.
# install.sh provisions both via Podman.
cd agents/knowledge && .venv/bin/uvicorn main:app --host 0.0.0.0 --port 8009 --reload
```

[← Back to agents](index.md)
