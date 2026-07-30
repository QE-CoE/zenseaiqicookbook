# DocuProof

> **Document Validation Agent** — compares two versions of a PDF and reports what genuinely changed, ignoring the parts that are meant to change.

| | |
|---|---|
| **Port** | `8014` |
| **Stack** | Python · FastAPI · pdfplumber |
| **Stage** | Specialised — runs independently of upstream agents |
| **Source** | `agents/pdf-validator/backend/` |

## What it does

DocuProof automates one of the last genuinely manual checks in regulated delivery. Validating a generated document today means printing two versions, laying them side by side and reading — slow, impossible to scale across a release, and unreliable after the third page. The agent compares a baseline and a candidate document and reports what materially changed, extracting both text and table structure from each. The critical capability is masking the differences that are *expected*, because documents are supposed to differ: a statement generated today carries today's date, so without exclusions a comparison is unreadable noise. Built-in presets cover dates, prices and currency amounts, reference identifiers, email addresses, phone numbers, percentages and page numbers, and anything domain-specific can be added as a custom rule. Outputs are line-level content differences, table structure analysis reporting column and row-count drift page by page, narration explaining each material difference in business language, and a side-by-side report suitable for attaching to a sign-off. Testers, business analysts and automation engineers use it to validate statements and invoices after a billing change, to evidence that a regulatory or policy template change did not disturb mandated wording, to verify clinical and laboratory reports after an upstream data change, and to diff generated reports between builds. On data-driven documents, table drift is often the most useful signal, since a stable text comparison combined with a changed row count usually indicates a data problem rather than a template one. Sample document pairs ship with the agent, covering invoice, financial, clinical and test-report scenarios, so a first run needs no preparation. For compliance and operations teams the outcome is document sign-off in minutes rather than hours, with an attachable audit trail. The wider benefit is materially fewer wording and layout defects reaching a customer, in exactly the documents where an error is most visible and least forgivable. DocuProof runs independently of the requirement pipeline.

Upload a **baseline** PDF and a **candidate** PDF. DocuProof extracts text and table structure from both, masks the differences you expect to see, and reports the ones you don't.

**What you give it:** two PDFs, plus the exclusion rules that describe acceptable variation.

**What you get back:**

| Output | Description |
|---|---|
| **Content differences** | Line-level additions and removals between the two documents |
| **Table structure analysis** | Column and row-count drift, page by page |
| **AI narration** | Each material difference explained in business language |
| **Side-by-side report** | Reviewable diff, suitable for attaching to a sign-off |

### Smart exclusion rules

Documents are *supposed* to differ — a statement generated today carries today's date. Without exclusions, a diff is unusable noise. DocuProof ships built-in presets for the fields that legitimately vary:

- Dates · prices and currency amounts · reference IDs
- Email addresses · phone numbers · percentages · page numbers

Anything domain-specific can be added as a **custom rule**.

## Why it matters

Document validation is one of the last genuinely manual checks in regulated delivery. Someone prints two statements, lays them side by side, and reads. It is slow, it does not scale to a release, and attention fades after the third page.

DocuProof turns that into a repeatable check. Typical use:

- **Statement and invoice validation** — confirm a billing engine change altered only what was intended
- **Regulatory and policy documents** — evidence that a template change did not disturb mandated wording
- **Clinical and laboratory reports** — verify report generation after an upstream data change
- **Test report comparison** — diff generated reports between builds

The business outcome is document sign-off in minutes instead of hours, with an attachable audit trail — and materially fewer wording or layout defects reaching a customer.

## In the UI

<!-- SCREENSHOT: docuproof-01-upload.png — Baseline and candidate PDF upload with exclusion preset toggles -->
*Upload both documents and choose which variations to ignore.*

<!-- SCREENSHOT: docuproof-02-exclusions.png — Exclusion presets plus custom rule entry -->
*Built-in presets, plus custom rules for domain-specific noise.*

<!-- SCREENSHOT: docuproof-03-diff.png — Side-by-side diff with material changes highlighted -->
*Side-by-side comparison — only material differences remain.*

<!-- SCREENSHOT: docuproof-04-narration.png — AI narration explaining each difference -->
*Each difference explained in plain language.*

## Tips

- **Start with presets on.** Run once with the standard exclusions enabled; add custom rules only for the noise that survives.
- **Sample PDFs ship with the agent** — `agents/pdf-validator/sample_pdfs/` contains invoice, financial, clinical and test-report pairs for a first run.
- **Table drift is the useful signal** on data-driven documents — a stable text diff with a changed row count usually means a data problem, not a template one.

## What's new

- **June 2026** — Agent introduced with exclusion presets, custom regex rules, table structure analysis and AI narration.

[← Back to agents](index.md)
