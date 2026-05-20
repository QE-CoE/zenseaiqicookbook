# Exploratory

Independent agent sweep across a deployed environment — no upstream dependency, run any time.

```mermaid
flowchart LR
  URL[Deployed URL] --> SX[Secure-Xi]
  URL --> PX[Perf-Xi]
  URL --> AC[Accessibility]
  URL --> VD[Visual Detector]
```

## When to use

- Pre-release environment validation
- Periodic non-functional health-checks
- Independent audit by the QE CoE

<!-- SCREENSHOT: workflow-exploratory-01-multi.png — Four agents running in parallel against one target -->
