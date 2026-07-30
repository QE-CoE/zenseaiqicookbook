# Knowledge Graph

> **Traceability Agent** — turns requirements, design documents and delivery artefacts into a connected map of the business, so change and coverage can be traced end to end.

| | |
|---|---|
| **Stack** | Next.js · Neo4j (graph persistence via Common Backend) |
| **Stage** | Quality Intelligence |
| **Upstream** | Knowledge Base sources, DeepSpeci, CaseGeni, Defect Intelligence |
| **Downstream** | Impact Analyzer |
| **Source** | `agents/other-agents/src/agents/knowledge-graph/` · `backend/src/modules/project-graph/` |

## What it does

Knowledge Graph solves the traceability problem every regulated programme eventually faces. Traceability is usually a spreadsheet somebody maintains until they stop — demanded at audit, assembled under pressure, and out of date the week after it is signed. Its inputs are Knowledge Base sources such as uploaded documents, Confluence spaces and Jira projects, together with the outputs the pipeline has already produced. The resulting graph, persisted in Neo4j, spans the business layer of capabilities, processes, rules and roles; the requirements layer of user stories, acceptance criteria and entities; the delivery layer of test cases, scenarios, defects, modules, APIs and system operations; and the findings produced by the security, performance and accessibility agents. Alongside the graph it produces concept maps, flow diagrams and knowledge gap analysis showing where documentation is thin or contradictory. Because the relationships are explicit, it answers questions the source documents cannot — which tests cover a business capability, which stories a business rule constrains, or what the impact path is from a proposed change to the tests and defects it touches. Product owners and business analysts use it to understand how the domain fits together, while QA uses it to find requirements that no test exercises. Graph quality tracks Knowledge Base quality, so connecting Confluence and Jira first is what makes capabilities and rules resolve against real content rather than guesses. The graph is a fingerprinted snapshot, so it should be rebuilt after significant requirement change to keep impact answers current. For audit and governance the outcome is traceability produced as a by-product of doing the work rather than as a separate project. Critically, this graph is the relationship model that [Impact Analyzer](impact-analyzer.md) depends on, so building it is what makes change impact assessment possible at all.

The Knowledge Graph reads your requirements, Confluence pages, design documents and delivery artefacts and builds an **enterprise knowledge model** — the business expressed as connected entities rather than as a pile of documents.

**What you give it:** Knowledge Base sources — uploaded documents, Confluence spaces, Jira projects — plus the outputs already produced by the pipeline.

**What you get back:** a navigable graph, persisted in Neo4j, covering:

| Layer | Node types |
|---|---|
| **Business** | Business capabilities, business processes, business rules, roles |
| **Requirements** | User stories, acceptance criteria, entities |
| **Delivery** | Test cases, test scenarios, defects, modules, APIs, system operations |
| **Findings** | Security findings, performance metrics, accessibility issues |

Alongside the graph it produces **concept maps**, **flow diagrams** and **knowledge gap analysis** — the areas where documentation is thin or contradictory.

Because relationships are explicit, the graph answers questions the underlying documents can't:

- Which test cases cover this business capability?
- Which user stories does this business rule constrain?
- What is the **impact path** from a proposed change to the tests and defects it touches?
- Where do we have requirements with no test coverage at all?

## Why it matters

Traceability is usually a spreadsheet somebody maintains until they stop. It is demanded at audit, assembled under pressure, and out of date the week after it is signed.

Building it from the artefacts themselves makes traceability a by-product of doing the work. Typical use:

- **Audit and regulatory evidence** — demonstrate requirement-to-test coverage on request
- **Change impact** — the graph is what powers [Impact Analyzer](impact-analyzer.md); without it, impact assessment falls back on individual memory
- **Coverage assurance** — find requirements no test exercises, before a release board does
- **Onboarding and knowledge retention** — a new joiner can see how the domain fits together, and the map survives handover

The business outcome is traceability that stays current, faster audit response, and change decisions grounded in relationships rather than recollection.

## In the UI

Available as an agent workspace, and through the **Knowledge Base** explorer for graph browsing.

<!-- SCREENSHOT: knowledge-graph-01-overview.png — Interactive graph of business capabilities, stories and test cases -->
*The enterprise knowledge model — capabilities through to test cases.*

<!-- SCREENSHOT: knowledge-graph-02-query.png — Search and filter across node types -->
*Search and filter by node type and relationship.*

<!-- SCREENSHOT: knowledge-graph-03-impact-path.png — Impact path traced from a change through to affected tests -->
*Impact path — a change traced to the artefacts it touches.*

<!-- SCREENSHOT: knowledge-graph-04-gaps.png — Knowledge gap analysis highlighting thin coverage -->
*Knowledge gap analysis — where documentation and coverage are thin.*

## Setup

Graph persistence requires **Neo4j**, provisioned as a Podman container by `install.sh`:

```bash
# Neo4j runs as the `zenseai-neo4j` container on bolt://localhost:7687
bash scripts/neo4j-podman-setup.sh start
```

## Tips

- **Ingest before you build.** Graph quality tracks Knowledge Base quality — connect Confluence and Jira first so capabilities and rules resolve against real content.
- **Rebuild after significant requirement change.** The graph is a snapshot, fingerprinted against its sources; a stale graph gives stale impact answers.
- **Large estates need headroom.** Neo4j memory limits were raised in July 2026 for bigger graphs — if a build stalls on a very large project, check the container's allocation.

## What's new

- **July 2026** — Business-capability relations, acceptance criteria, business rules and impact paths corrected; duplicate graph generation and redundant writes removed; Neo4j memory raised for larger graphs.
- **June 2026** — Rebuilt on Neo4j with the enterprise knowledge model; defect and test-case relations, module identification and isolated-node handling added.

[← Back to agents](index.md)
