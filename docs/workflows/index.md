# Workflows

The pipeline builder lets you compose agents into named workflows. These are the most common patterns we ship as starting points.

| Workflow | Use when |
|---|---|
| [End-to-end Pipeline](end-to-end.md) | New feature from requirement → executed regression |
| [Requirement → Test](requirement-to-test.md) | Just need designed cases + data; manual execution |
| [Exploratory](exploratory.md) | A11y/security/perf sweep against a deployed environment |
| [Regression](regression.md) | PR-time selective regression on a code change |

Every workflow is just a saved selection of agents + their order. You can fork any of these in the UI.
