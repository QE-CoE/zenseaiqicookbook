# RIA — Requirements Intelligence Assistant

> **In-app conversational assistant** — branded **ZenRia** in the product; answers questions about the platform and your project, and helps stakeholders articulate requirements DeepSpeci can refine.

| | |
|---|---|
| **Port** | `8010` |
| **Stack** | Python · FastAPI |
| **Stage** | Requirements & Specs |
| **Downstream** | DeepSpeci |
| **Source** | `agents/ria/` |

## What it does

ZenRia addresses two everyday frictions: business stakeholders who find it hard to express a requirement in a form a delivery team can act on, and new users facing a platform of nineteen agents without knowing where to start. Users simply type a question, or describe what they want, in plain English. For requirement intake it asks clarifying questions, captures the decisions reached, and produces a clean requirement draft ready to hand to DeepSpeci. For platform guidance it explains what a given agent does and which one suits the task in hand. It can also answer questions about the current project's state, grounded in the knowledge connected to that project. Inputs are natural-language questions and descriptions; outputs are answers, clarifying prompts and structured requirement drafts. Product owners and business analysts use it at the very start of the lifecycle, often as the front door for stakeholders who would otherwise send requirements by email. Answer quality depends directly on the Knowledge Base scope available to it, including Azure AI Search connector content, so pointing it at the right collection matters. The practical outcomes are requirements that arrive usable rather than needing a workshop to decode, and a shorter path to productivity for people new to the platform. Within the ZenseAI.QI workflow ZenRia sits upstream of DeepSpeci, and alongside every other agent as a permanent source of help.

ZenRia is the assistant available throughout the workspace. It draws on the [Knowledge Base](knowledge-base.md) — including Azure AI Search connector content — so its answers reflect your project rather than generic guidance.

**What you give it:** a question or a requirement described in plain English.

**What you get back:**

- Answers about the platform, an agent, or your project's current state
- Clarifying questions that surface the decisions a requirement leaves open
- A clean **requirement draft**, ready to hand to [DeepSpeci](deepspeci.md)

## Why it matters

Two problems, one assistant. Non-technical stakeholders struggle to write requirements in a form a delivery team can act on — and new users of a nineteen-agent platform need somewhere to ask "which agent do I use for this?".

Typical use:

- **Requirement intake** — a business stakeholder describes what they want conversationally, and leaves with a structured draft
- **Platform guidance** — find the right agent without reading the full catalogue
- **Project questions** — ask about the current project's state, grounded in its own knowledge

The business outcome is requirements that arrive usable, and shorter time-to-productivity for new users.

## In the UI

<!-- SCREENSHOT: ria-01-chat.png — ZenRia chat interface with retrieval-grounded answers -->
*ZenRia — grounded in your Knowledge Base.*

<!-- SCREENSHOT: ria-02-draft.png — Generated requirement draft with edit button -->
*A conversation becomes a requirement draft, ready for DeepSpeci.*

## Tips

- **Point it at the right collection.** Answer quality tracks the Knowledge Base scope available to it.
- **Use it as the front door for business stakeholders** who would otherwise send requirements by email.

## What's new

- **July 2026** — Azure AI Search connector context enabled for ZenRia retrieval.

[← Back to agents](index.md)
