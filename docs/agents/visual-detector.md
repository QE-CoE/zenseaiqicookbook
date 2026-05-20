# Visual Detector

> **Visual Regression Agent** — pixel and layout drift detection across builds.

| | |
|---|---|
| **Stack** | Node · Playwright · OpenCV / pixelmatch |
| **Stage** | Automation |
| **Source** | `agents/visual-detector/` |

## What it does

Captures a baseline screenshot set, then compares subsequent runs and surfaces:

- **Pixel diffs** (configurable threshold)
- **Layout shifts** (element bounding-box changes)
- **AI-explained changes** ("the CTA button moved 40px down because the hero increased in height")

## Why it matters

Catches CSS regressions that unit tests and DOM-based E2E tests miss entirely.

## In the UI

<!-- SCREENSHOT: visual-detector-01-baseline.png — Baseline capture run -->
<!-- SCREENSHOT: visual-detector-02-diff.png — Side-by-side diff with red highlight -->

[← Back to agents](index.md)
