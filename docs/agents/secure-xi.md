# Secure-Xi

> **Security Testing Agent** — OWASP/ASVS-aligned vulnerability scan with AI-driven exploit reasoning.

| | |
|---|---|
| **Port** | `8004` |
| **Stack** | Python · FastAPI |
| **Stage** | Specialised — runs independently of upstream agents |
| **Source** | `agents/secure-xi/` |

## What it does

Secure-Xi moves security testing to the point in delivery where problems are cheapest to fix and most often missed. Findings usually arrive from an annual penetration test or a formal assessment, long after the code shipped, when remediation competes directly with new feature work. The agent brings that assessment forward into the delivery cycle, where a fix is a code change rather than a programme. Users point it at a deployed URL or upload an OpenAPI specification, and it discovers endpoints both from the specification and by crawling. It then probes for the OWASP Top 10, including injection, broken authentication, cross-site scripting, server-side request forgery and insecure direct object references. What distinguishes it from a conventional scanner is that it reasons about exploit chains, recognising for example that a particular object-reference weakness combined with a verbose error message constitutes an account-takeover path. Findings carry a severity, the relevant ASVS chapter, supporting evidence and a remediation snippet, alongside a visual explanation of the chain. Security engineers are the primary users, but the output is written to be actionable by developers rather than requiring a specialist to interpret it. Supplying an OpenAPI specification materially improves coverage, since specification-driven discovery reaches endpoints that crawling alone will miss, and a Guidewire loader supports insurance estates specifically. Typical scenarios are a pre-release security gate, prioritising a remediation backlog, and continuous assurance after each release rather than once a year. The outcomes are remediation effort concentrated where exploitability is genuine rather than spread across a long list of informational findings, and fewer issues escalating into a formal assessment. Secure-Xi runs independently of the requirement pipeline and can be used at any stage of a project.

Point Secure-Xi at a deployed URL (or upload an OpenAPI spec) and it:

1. **Discovers** endpoints via spec + crawling
2. **Probes** for OWASP Top 10 (injection, broken auth, XSS, SSRF, IDOR, etc.)
3. **Reasons** about exploit chains — "this IDOR + this verbose error == account-takeover path"
4. **Reports** with severity, evidence, remediation snippet

## Why it matters

Most DAST tools surface findings. Secure-Xi surfaces *exploitable* findings — and explains the chain.

Typical use:

- **Pre-release security gate** — find exploitable paths before a penetration test does, when fixes are still cheap
- **Remediation prioritisation** — a chained account-takeover path outranks a dozen informational findings
- **Developer enablement** — findings arrive with evidence and a remediation snippet, not just a CWE reference
- **Continuous assurance** — re-scan after each release rather than waiting for an annual assessment

The business outcome is fewer findings escalating to a formal assessment, and remediation effort spent where exploitability is real.

## In the UI

<!-- SCREENSHOT: secure-xi-01-target.png — Target URL / spec upload input -->
<!-- SCREENSHOT: secure-xi-02-scan-progress.png — Live scan progress, endpoint by endpoint -->
<!-- SCREENSHOT: secure-xi-03-findings.png — Findings table with severity + ASVS chapter -->
<!-- SCREENSHOT: secure-xi-04-exploit-chain.png — Visual exploit chain explanation -->

## Tips

- **Upload the OpenAPI spec when you have one.** Spec-driven discovery reaches endpoints crawling alone will miss.
- **Scan a representative environment.** Findings are only as valid as the deployment they came from.

## What's new

- **June 2026** — Guidewire OpenAPI loader added for insurance estates.

[← Back to agents](index.md)
