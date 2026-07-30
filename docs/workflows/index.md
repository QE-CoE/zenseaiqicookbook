# Workflows

The pipeline builder lets you compose agents into named workflows. These are the most common patterns we ship as starting points.

| Workflow | Use when |
|---|---|
| [End-to-end Pipeline](end-to-end.md) | New feature from requirement → executed regression |
| [Requirement → Test](requirement-to-test.md) | Just need designed cases + data; manual execution |
| [Exploratory](exploratory.md) | A11y/security/perf/document sweep against a deployed environment |
| [Regression](regression.md) | Change-scoped regression on an existing test estate |

Every workflow is just a saved selection of agents + their order. You can fork any of these in the UI.

## Template catalogue

The pipeline builder ships **36 ready-made templates**, filtered by your project's sector. Pick one as a starting point rather than composing from scratch.

| Group | Templates |
|---|---|
| **Cross-sector** | Test Case Generation from Requirements · Test Automation Script Pack · Framework Bootstrap · Data-Driven Test Automation · Requirement Quality Gate · Smoke + Sanity Suite · Regression Suite Refresh · Failure Triage Pack · Test Suite Health Check · Knowledge Graph from Docs · Security Pen-Test Lite · Accessibility Audit Sprint · Performance Baseline (Greenfield) · Performance Brownfield Audit · Convert Manual Tests to Automation · End-to-End QA Pipeline · Spec → Ship Bundle · Compliance-Safe Test Data Bundle |
| **BFSI** | Loan Origination QA · Payment Gateway Smoke Suite · Loan Journey Security Assessment · Payments Rail QE Coverage Pack · Payments Rail QE Full Pipeline |
| **BFSI — Guidewire** | User Story Refinement · Test Case Generation · Stories to Test Cases · Stories to Automation · Security Assessment · Performance Benchmark · ContactManager QA · Reinsurance Management QA |
| **HLS** | EHR HIPAA Compliance Pack |
| **MCS** | E-commerce Checkout Coverage · E-commerce Performance Benchmark |
| **TMT** | Telco Billing Cycle Tests |

Templates carry their agent selection, order and default configuration. Instantiate one, then adjust it like any other pipeline.

## Demo Builder Studio

For demonstrations and proof-of-concept work, **Demo Builder Studio** stands up a complete demo project — Knowledge-Base-powered Jira seeding and automatic story cleanup — so a working environment is ready in minutes.
