# Vantage

> **Live Session Tool (developer-only)** — view and control a running browser or mobile session, and turn what you do into a Playwright test project. No AI involved.

!!! warning "Not a deployed agent"
    Vantage is a developer tool. It drives Chrome, Android (adb) and iOS (Appium) on whichever machine runs it, so it is started by `dev.sh` and `install.sh` and is deliberately **not** part of the deployed process set. It is not counted among the 19 agents.

| | |
|---|---|
| **Port** | `8017` |
| **Stack** | Node · Express · TypeScript |
| **Stage** | Automation support — independent |
| **Source** | `agents/vantage/` |

## What it does

- **Connect** to Chromium over the Chrome DevTools Protocol, to Android through an adb bridge, or to iOS through Appium
- **View and control** the live session — screenshots, click, type, fill, scroll and wheel
- **Record** a journey, actively or passively, and export it as a **Playwright project**
- **Capture API traffic** (opt-in): up to 500 XHR/fetch calls held in memory, credentials redacted at capture. Choose a scope of UI, API or UI + API when exporting

## Exports

| Export | Contents |
|---|---|
| **Playwright framework (ZIP)** | `tests/ui/recorded-flow.test.ts` with page objects, and `tests/api/captured-api.test.ts`, as separate Playwright projects — `npm run test:ui`, `npm run test:api`, or `npm test` for both |
| **Postman collection** | Postman v2.1 |
| **OpenAPI** | OpenAPI 3.0 inferred from captured traffic |

API tests offer **basic, standard or strict** assertion levels, chain a login token, and support GraphQL.

## Limitations

- The link between a UI step and an API call is a hint — the latest step when the request fired
- WebSocket traffic is not captured
- The OpenAPI specification is inferred from one sample per endpoint
- Multipart uploads are exported as `test.fixme` placeholders

[← Back to agents](index.md)
