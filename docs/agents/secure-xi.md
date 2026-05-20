# Secure-Xi

> **Security Testing Agent** — OWASP/ASVS-aligned vulnerability scan with AI-driven exploit reasoning.

| | |
|---|---|
| **Port** | `8004` |
| **Stack** | Python · FastAPI |
| **Stage** | Specialised — runs independently of upstream agents |
| **Source** | `agents/secure-xi/` |

## What it does

Point Secure-Xi at a deployed URL (or upload an OpenAPI spec) and it:

1. **Discovers** endpoints via spec + crawling
2. **Probes** for OWASP Top 10 (injection, broken auth, XSS, SSRF, IDOR, etc.)
3. **Reasons** about exploit chains — "this IDOR + this verbose error == account-takeover path"
4. **Reports** with severity, evidence, remediation snippet

## Why it matters

Most DAST tools surface findings. Secure-Xi surfaces *exploitable* findings — and explains the chain.

## In the UI

<!-- SCREENSHOT: secure-xi-01-target.png — Target URL / spec upload input -->
<!-- SCREENSHOT: secure-xi-02-scan-progress.png — Live scan progress, endpoint by endpoint -->
<!-- SCREENSHOT: secure-xi-03-findings.png — Findings table with severity + ASVS chapter -->
<!-- SCREENSHOT: secure-xi-04-exploit-chain.png — Visual exploit chain explanation -->

[← Back to agents](index.md)
