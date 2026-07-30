# Accessibility Intelligence

> **a11y Audit + Remediation Agent** — axe-core scan across a whole site with AI-explained findings and code-level fix suggestions.

| | |
|---|---|
| **Port** | `8005` |
| **Stack** | Node · Express · axe-core |
| **Stage** | Specialised — independent |
| **Source** | `agents/Accessibility/` |

## What it does

Accessibility Intelligence speaks to both a legal exposure and a usability gap. Public-sector procurement and accessibility legislation increasingly require demonstrable WCAG conformance, yet the raw tooling produces hundreds of findings that no team can triage in that form. The agent runs an industry-standard accessibility engine across a whole site rather than a sample of pages, then does the work that makes the results usable. It groups findings by WCAG criterion and severity, explains each one for a non-expert audience by answering why it matters, and suggests concrete fixes including DOM patches, ARIA attribute changes and contrast adjustments. Inputs are a URL or page list and a crawl depth; outputs are the organised finding set, the explanations and fixes, a dashboard with a severity heatmap, and a downloadable report suitable for sharing with stakeholders. Business analysts and testers use it for compliance evidence, remediation planning and post-release regression checks, while delivery managers use the report in procurement and governance conversations. Deep crawls take time, since each page is audited in turn and a sixty-page crawl can run past ten minutes, so runs should be planned rather than triggered casually. Starting with a representative page set is usually more efficient than sweeping the whole estate, because the same template issues tend to repeat across pages. It is enabled by default for the BFSI sector, where accessibility obligations are typically contractual. Typical scenarios are pre-release conformance checks, building a remediation backlog, and demonstrating conformance on request. The outcomes are reduced legal and procurement risk, a product usable by more people, and accessibility work that can actually be scheduled because each finding is specific enough to assign to a developer. It runs independently of the requirement pipeline.

1. Crawls a target URL, a list of URLs, or discovers pages automatically (up to 50 pages per run)
2. Runs **axe-core** against each page
3. **Groups** findings by WCAG criterion and severity
4. **Explains** each finding for non-experts ("Why does it matter?")
5. **Suggests fixes** — DOM patches, ARIA attribute changes, contrast adjustments
6. **Generates a polished dashboard** plus a downloadable HTML/PDF report

**What you give it:** a URL or page list, and a crawl depth.

**What you get back:** a WCAG-organised finding set with a severity heatmap, plain-language explanations, concrete fix suggestions, and a stakeholder-ready report.

## Why it matters

axe-core surfaces hundreds of raw findings. Accessibility Intelligence groups, explains and prescribes — turning a wall of warnings into a triaged backlog.

Typical use:

- **Compliance evidence** — a shareable WCAG report for procurement, legal or public-sector obligations
- **Remediation planning** — findings ordered by severity, with fixes specific enough to assign
- **Regression checking** — re-run after a release to confirm accessibility did not regress
- **Whole-site assessment** — crawl the estate rather than spot-checking a handful of pages

The business outcome is reduced legal and procurement risk, a usable product for more people, and accessibility work that can actually be scheduled because the findings are specific.

## In the UI

<!-- SCREENSHOT: a11y-01-target.png — URL list / sitemap input with crawl depth -->
<!-- SCREENSHOT: a11y-02-dashboard.png — Polished dashboard with WCAG breakdown and severity heatmap -->
<!-- SCREENSHOT: a11y-03-finding-detail.png — Single finding with AI explanation + fix snippet -->
<!-- SCREENSHOT: a11y-04-report-download.png — Combined HTML/PDF report download -->

## Tips

- **Deep crawls take time.** A 60-page crawl audits each page in turn and can run past ten minutes — the platform allows for this, but plan the run accordingly.
- **Start with a representative page set** rather than the whole site; the same template issues usually repeat across pages.

## What's new

- **July 2026** — Enabled for the BFSI sector by default; raised proxy timeout for deep crawls; report downloads forwarded correctly.
- **April 2026** — Polished dashboard generator (`write-polished-dashboard.js`).
- **March 2026** — AI remediation engine (`ai-remediation.js`) using the per-tenant LLM config.

[← Back to agents](index.md)
