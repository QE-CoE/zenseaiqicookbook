# FAQ

### Is ZenseAI.QI a product or an accelerator?

It's an **AI-driven QE accelerator**. We use the term deliberately — it's a set of composable agents and a pipeline runner, not a packaged SaaS offering.

### Can I use my own LLM keys?

Yes. Seven providers are listed in the provider catalogue — Google Gemini, OpenAI, Anthropic Claude, Azure AI Foundry, Meta Llama, Mistral and Cohere.

Server-side completion is currently implemented for **Google Gemini, OpenAI, Anthropic Claude and Azure AI Foundry**. The remaining three can be configured but will not serve completions yet. Keys are encrypted at rest and never exposed to the browser — see [Security](security.md).

### Which integrations are supported?

Twenty-one integrations can store credentials, across project planners (Jira, Azure DevOps, Monday.com, Asana, Trello, ClickUp), test management (TestRail, Zephyr Scale, qTest, Testmo, Xray), CI/CD (Jenkins, GitHub Actions, GitLab CI, CircleCI, Azure Pipelines), version control (GitHub, GitLab, Bitbucket), design (Figma) and cloud devices (TestMu AI).

Working **data adapters** currently exist for **Jira** and **qTest**. Other providers connect and validate credentials while their adapters are built. Figma is required for [Visual Xi](../agents/visual-detector.md), and TestMu AI for its cloud-device runs.

### Can I use only one agent?

Yes. Every agent is an independent service. You can run, say, just Accessibility Intelligence against your deployed site without touching the rest of the pipeline.

### Can I self-host?

Yes — `install.sh` provisions Python venvs, npm installs, Playwright browsers, and three Podman containers (PostgreSQL, PostgreSQL with pgvector, and Neo4j). `make dev` (or `bash dev.sh`) starts everything. It also runs under Git Bash on Windows.

### What are the prerequisites?

Python 3.10+ (the platform is aligned on 3.14), Node.js 22+, npm 9+, and Podman 4.0+ for the database containers. Tesseract OCR is optional, for document parsing in DeepSpeci.

### What stack is the frontend on?

Next.js 16 (App Router + React Compiler), React 19, Tailwind 4.x, Radix UI primitives. No external state library — React Context + a memory cache reconciled with the backend on mount.

### Where do agent results live?

PostgreSQL (`pipeline_runs`, `agent_outputs`). The frontend keeps a hot in-memory cache that reconciles via `hydrateProjectFromBackendAsync()` on every mount. The cache survives backend outages and holds optimistic writes (validate, edit-in-place). Knowledge Graph data is persisted separately in Neo4j.

### What is a sector, and why does it matter?

Each project is scoped to an industry sector — BFSI, MCS, HLS or TMT. The sector tailors the agent catalogue and determines which policy packs [Test Reviewer](../agents/test-reviewer.md) applies, so a healthcare project is checked against HIPAA rules and a banking project against BFSI rules without anyone selecting them manually.

### How do I add a new agent?

1. Add a service under `agents/<name>/` with a `/process/stream` SSE endpoint
2. Register it in the agent master seed (`backend/src/database/seeds/seed-agents-master.ts`) and add its routing in `backend/src/integrations/ai/agent-routing.ts`
3. Add a workspace component under `frontend/src/modules/agent/<name>/`
4. Wire dependencies in `frontend/src/modules/project/services/pipeline-data.service.ts` (`getPreviousAgentId`)

### How do I report a bug?

Open an issue on [github.com/QE-CoE/zenseaiqicookbook](https://github.com/QE-CoE/zenseaiqicookbook) (for docs) or the platform repo (for product).
