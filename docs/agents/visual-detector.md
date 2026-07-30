# Visual Xi

> **Design Compliance Agent** — compares a Figma design against the live site, scores how faithfully it was built, and explains what to change.

| | |
|---|---|
| **Port** | `8013` |
| **Stack** | Python · FastAPI · Node Playwright runner |
| **Stage** | Automation |
| **Integrations** | Figma (required) · TestMu AI (optional, for cloud devices) |
| **Source** | `agents/visual-detector/` |

## What it does

Visual Xi settles the argument design and engineering have most often: whether the built page actually matches the approved design. Design fidelity normally degrades quietly — a spacing value approximated here, a component drifting from the design system there — until a brand review finds the deviation in twenty places at once. The agent compares a Figma design reference against a live URL and scores how faithfully it was implemented. Designers, testers and business analysts submit one or more Figma and URL pairs, and page lists can be imported from Excel for site-wide sweeps. Outputs include a design compliance score, comparison views in side-by-side, onion-skin overlay and heatmap form, and analysis that explains each difference and suggests the CSS to correct it. The same run also produces an accessibility audit and a link health check, consolidated into a single shareable report. Ignore regions exclude areas expected to differ, such as carousels, personalised blocks and live data, which is what keeps the comparison meaningful rather than noisy. Cloud device execution verifies rendering on real devices and browsers instead of one developer's laptop. Typical scenarios are design sign-off, design-system governance, and a combined visual and accessibility check before release. For design and product teams the benefit is objective sign-off rather than subjective review; for engineering it is fewer late-stage cosmetic defects. The outcome is faster approval, less rework near a release date, and brand consistency that is measured rather than assumed. Visual Xi runs independently of the requirement pipeline, so it can be introduced at any point in a project.

Visual Xi answers the question design and QA argue about most: *does the built page actually match the design?*

**What you give it:** a Figma design reference and the live URL to compare it against. Several pairs can be submitted in one run, and page lists can be imported from Excel for bulk comparison.

**What you get back:**

| Output | Description |
|---|---|
| **Design compliance score** | How closely the implementation matches the design |
| **Visual Eyes comparison** | Side-by-side, **onion-skin** overlay and **heatmap** views of the differences |
| **AI analysis** | Each difference explained, with **CSS fix suggestions** |
| **Accessibility audit** | axe-core findings on the same pages, in the same run |
| **Link health** | Broken and misdirected links across the compared pages |
| **Consolidated report** | Everything above in one shareable report |

**Ignore regions** exclude areas that are expected to differ — carousels, personalised blocks, live data — so the comparison stays signal, not noise.

**Cloud device execution** runs the comparison on real devices and browsers via TestMu AI, for teams who need to verify rendering beyond their local browser.

## Why it matters

Design fidelity normally degrades quietly. A developer approximates a spacing value, a component drifts from the design system, and nobody notices until a brand review — by which point the deviation is in twenty places.

Checking against the design source of truth makes that objective and continuous. Typical use:

- **Design sign-off** — replace subjective review with a measured compliance score
- **Design-system governance** — catch drift from the system before it propagates
- **Pre-release visual check** — confirm a release did not disturb layout, and check accessibility and link health while you are there
- **Cross-device verification** — confirm the design holds on real devices, not just a developer's laptop

The business outcome is faster design sign-off, less rework late in delivery, and brand consistency that is actually verified rather than assumed.

## In the UI

<!-- SCREENSHOT: visual-detector-01-baseline.png — Figma reference and live URL input, with batch pairs -->
*Provide the Figma reference and live URL — several pairs per run.*

<!-- SCREENSHOT: visual-detector-02-diff.png — Visual Eyes side-by-side, onion-skin and heatmap comparison -->
*Visual Eyes — side-by-side, onion-skin and heatmap views.*

<!-- SCREENSHOT: visual-detector-03-ai-analysis.png — AI analysis with CSS fix suggestions -->
*Each difference explained, with a suggested CSS fix.*

<!-- SCREENSHOT: visual-detector-04-consolidated-report.png — Consolidated report with compliance score, accessibility and link health -->
*Consolidated report — compliance, accessibility and link health together.*

## Setup

Visual Xi requires a **Figma** integration to read design references. Add it on the Integrations page before the first run. Cloud device execution additionally requires **TestMu AI** credentials.

## Tips

- **Set ignore regions early.** One pass to identify the genuinely dynamic areas makes every later run far more readable.
- **Use Excel import for site-wide sweeps** rather than adding pages one at a time.
- **Onion-skin beats side-by-side for spacing issues** — small offsets are much easier to see in overlay.

## What's new

- **June 2026** — Full workflow shipped: Visual Eyes comparison modes, AI analysis with CSS suggestions, accessibility audit, link health, batch runs, Excel import, ignore regions and cloud device execution. Cloud-device runs now fail clearly instead of hanging when a session never starts.

[← Back to agents](index.md)
