# FAQ

### Is ZenseAI.QI a product or an accelerator?

It's an **AI-driven QE accelerator**. We use the term deliberately — it's a set of composable agents and a pipeline runner, not a packaged SaaS offering.

### Can I use my own LLM keys?

Yes. The Common Backend supports OpenAI, Anthropic, Google (Gemini), and Azure OpenAI. Keys are encrypted at rest and never exposed to the browser. See [Security](security.md).

### Can I use only one agent?

Yes. Every agent is an independent service. You can run, say, just Accessibility against your deployed site without touching the rest of the pipeline.

### Can I self-host?

Yes — `install.sh` provisions Python venvs, npm installs, Playwright browsers, and PostgreSQL via Podman. `make dev` (or `bash dev.sh`) starts everything.

### What stack is the frontend on?

Next.js 16.2.1 (App Router + React Compiler), React 19, Tailwind 4.x, Radix UI primitives. No external state library — React Context + a memory cache reconciled with the backend on mount.

### Where do agent results live?

PostgreSQL (`pipeline_runs`, `agent_outputs`). The frontend keeps a hot in-memory cache that reconciles via `hydrateProjectFromBackendAsync()` on every mount. The cache survives backend outages and holds optimistic writes (validate, edit-in-place).

### How do I add a new agent?

1. Add a service under `agents/<name>/` with a `/process/stream` SSE endpoint
2. Register it in `backend/src/modules/agent/agent.registry.ts`
3. Add a workspace component under `frontend/src/modules/agent/<name>/`
4. Wire dependencies in `frontend/src/modules/project/services/pipeline-data.service.ts` (`getPreviousAgentId`)

### How do I report a bug?

Open an issue on [github.com/QE-CoE/zenseaiqicookbook](https://github.com/QE-CoE/zenseaiqicookbook) (for docs) or the platform repo (for product).
