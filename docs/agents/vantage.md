# Vantage

> **Record once, replay forever** — Vantage watches a workflow on a live system once and produces a ready-to-run automated test. It runs on a deterministic, rule-based engine with no AI in the loop, so every test is repeatable, auditable, private, and free of per-action cost.

!!! warning "Not a deployed agent"
    Vantage is a developer tool. It drives Chrome, Android and iOS targets on whichever machine runs it, so it is started by `dev.sh` and `install.sh` and is deliberately **not** part of the deployed process set. It cannot be added to a pipeline, and it is not counted among the 19 agents.

| | |
|---|---|
| **Port** | `8017` |
| **Stack** | Node · Express · TypeScript |
| **Stage** | Automation support — independent |
| **AI / LLM** | None — no model is called at any point |
| **Source** | `agents/vantage/` |

## What it does

Teams usually write automated tests by hand: someone walks through the workflow, then spends hours translating it into code and selectors. Vantage removes that translation step. A tester performs the workflow once on the live system while Vantage watches, and Vantage turns what it saw into a test project that runs without further editing.

Because the engine is rule-based rather than model-driven:

- **Repeatable** — the same recording always produces the same test
- **Auditable** — each generated step maps to something the tester actually did, and the logic can be read line by line
- **Private** — screens, data and credentials are never sent to a language model
- **No per-action cost** — nothing is billed by the click, so recording and re-recording are free

## What it can drive

| Target | How it connects | What you can do |
|---|---|---|
| **Web** — Chrome, Edge or any Chromium browser | Chrome DevTools Protocol (`--remote-debugging-port`) | Live screenshot, click, type, fill, scroll; record the flow |
| **Chromium-based desktop apps** | Same CDP connection, where the app exposes a debugging port | Same as web |
| **Android** — device or emulator | ADB port-forward to its Chrome or WebView; or an Appium session for the native app | Same as web for WebView content; tap, type, clear and navigation buttons for native screens |
| **iOS** — device or simulator | `ios-webkit-debug-proxy` for Safari and WebView; or an Appium session for the native app | Live inspection of web content; tap and type on native screens |

## How a test is produced

1. **Connect** to the target and watch the live screen
2. **Record** the workflow — *active* (you drive it from Vantage) or *passive* (you use the application normally and Vantage observes)
3. **Review and edit** — rename, reorder or delete steps, and include or exclude captured API calls
4. **Export** a ready-to-run project as a ZIP

## What you get

| Export | Contents |
|---|---|
| **Web / Chromium** | A Playwright project: `tests/ui/recorded-flow.test.ts` with page objects |
| **Mobile (Appium)** | A Playwright + Appium project with a bundled Appium client — no extra install |
| **API tests** (optional) | `tests/api/captured-api.test.ts` generated from the API calls the UI flow triggered, as a separate Playwright project. `npm run test:ui`, `npm run test:api`, or `npm test` for both |
| **Postman** | Collection v2.1 |
| **OpenAPI** | OpenAPI 3.0 inferred from captured traffic |

### API capture

Optional, and independent of recording. Choose a scope of **UI**, **API** or **UI + API**.

- Up to 500 XHR/fetch calls are held **in memory only** and never written to disk
- Credentials are redacted at capture: authorisation, cookie and API-key headers are dropped, and sensitive fields in bodies become `[REDACTED]`
- Assertion level is **basic**, **standard** or **strict**; IDs, timestamps and tokens are always checked by type only
- A login that returns a token is detected, and the export includes a helper that logs in once and reuses the token
- GraphQL calls are de-duplicated per operation

## Roadmap

Vantage is being extended beyond web and mobile to **desktop Java point-of-sale applications** and **store peripherals** such as receipt printers and barcode scanners, so a single recorded workflow can span the whole store. These targets are **planned and not yet available** — the current release connects to browsers, Chromium-based apps and Android/iOS targets only.

## Limitations

- The link between a UI step and an API call is a hint — the latest step when the request fired — not a guarantee
- WebSocket traffic is not captured
- The OpenAPI specification is inferred from one sample per endpoint, so review it
- Multipart uploads are exported as `test.fixme` placeholders
- Coordinate-based mobile steps are brittle across screen sizes and resolutions

[← Back to agents](index.md)
