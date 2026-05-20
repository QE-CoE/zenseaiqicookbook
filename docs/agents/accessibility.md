# Accessibility

> **a11y Audit + Remediation Agent** — axe-core scan with AI-explained findings and code-level fix suggestions.

| | |
|---|---|
| **Port** | `8005` |
| **Stack** | Node · Express · axe-core |
| **Stage** | Specialised — independent |
| **Source** | `agents/Accessibility/` |

## What it does

1. Crawls a target URL (or list of URLs)
2. Runs **axe-core** against each page
3. **Groups** findings by WCAG criterion and severity
4. **Explains** each finding for non-experts ("Why does it matter?")
5. **Suggests fixes** — DOM patches, ARIA attribute changes, contrast adjustments
6. **Generates a polished dashboard** + downloadable HTML/PDF report

## Why it matters

axe-core surfaces 100s of raw findings. Accessibility groups, explains, and prescribes — turning a wall of warnings into a triaged backlog.

## In the UI

<!-- SCREENSHOT: a11y-01-target.png — URL list / sitemap input -->
<!-- SCREENSHOT: a11y-02-dashboard.png — Polished dashboard with WCAG breakdown -->
<!-- SCREENSHOT: a11y-03-finding-detail.png — Single finding with AI explanation + fix snippet -->
<!-- SCREENSHOT: a11y-04-report-download.png — Combined HTML/PDF report download -->

## What's new

- **April 2026** — Polished dashboard generator (`write-polished-dashboard.js`).
- **March 2026** — AI remediation engine (`ai-remediation.js`) using the per-tenant LLM config.

[← Back to agents](index.md)
