# Game-Xi

> **Game Testing Agent** — game-flow and rule-coverage validator for game-like applications.

| | |
|---|---|
| **Port** | `8006` |
| **Stack** | Python · FastAPI |
| **Stage** | Specialised |
| **Source** | `agents/game-xi/` |

## What it does

Validates that game rules and state transitions are exercised correctly:

- **State coverage** — every reachable state visited at least once
- **Rule violations** — detects illegal transitions
- **Win/lose-condition coverage** — every terminal path exercised

## In the UI

<!-- SCREENSHOT: game-xi-01-rules.png — Rule schema input -->
<!-- SCREENSHOT: game-xi-02-coverage.png — State coverage report -->

[← Back to agents](index.md)
