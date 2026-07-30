# Payments Rail QE

> **Payments Testing Agent** — generates rail-aware test scenarios for payment flows, with the compliance checks each rail and regulator expects built in.

| | |
|---|---|
| **Port** | `8012` |
| **Stack** | Python · FastAPI |
| **Stage** | Specialised |
| **Upstream** | DeepSpeci (optional) · Knowledge Base |
| **Source** | `agents/payments-rail/` |

## What it does

Payments Rail QE addresses a scarcity problem. Payments defects are unusually expensive — a mishandled return or a missed sanctions screen is not a bug report but a regulatory finding, a remediation programme and sometimes a fine — yet the rail expertise needed to test properly sits with a few people per organisation and is hard to recruit. The agent encodes that expertise so a tester without a decade of payments background can produce credible coverage. Inputs are the payment flow or requirement under test, optionally grounded in Knowledge Base payment documentation. Outputs are rail-appropriate scenarios spanning happy path, rejection and return handling, timing edge cases, and the compliance assertions the enabled packs require. A conversational mode lets a tester explore unfamiliar rail behaviour before committing to a full scenario set, which is often how a team new to a rail gets oriented. Business analysts and testers use it when onboarding a new rail, evidencing compliance to an internal audit function, or validating message handling during a payments modernisation programme. Ingesting payment documentation first materially improves relevance, because the Knowledge Base chunks payment content by flow rather than by page and therefore returns whole flows instead of fragments. Enabling only the packs that genuinely apply matters, since every pack adds obligations a given programme may not owe. Typical scenarios include a bank adding instant payments, a modernisation programme moving to ISO 20022, and routine regression whenever the payment engine changes. For risk and compliance functions the outcome is demonstrable coverage of screening and consumer-protection obligations; for delivery teams it is credible payments testing without waiting on a scarce specialist. Payments Rail QE can run standalone or take refined requirements from DeepSpeci as its starting point.

Payments Rail QE understands that a payment is not a generic transaction — each rail has its own message format, timing rules, return codes and regulatory obligations. It generates test scenarios that reflect those differences.

**Supported rails**

| Rail | Coverage |
|---|---|
| **ACH** | Batch processing, return codes, settlement windows |
| **FedNow** | Instant payment flows, real-time confirmation and rejection |
| **SWIFT** | Cross-border messaging |
| **EFT / RTC** | Electronic funds transfer and real-time clearing |
| **ISO 20022** | `pacs.008`, `pain.001` and related message validation |

**Built-in compliance packs**

- **SARB** and **FinSurv** — South African Reserve Bank reporting and exchange-control obligations
- **OFAC** — sanctions screening scenarios
- **Reg E** — consumer electronic funds transfer protections and error-resolution flows

**What you give it:** the payment flow or requirement you are testing, optionally grounded in Knowledge Base payment documentation.

**What you get back:** rail-appropriate test scenarios covering happy path, rejection and return handling, timing edge cases, and the compliance assertions the applicable packs require. A conversational mode is available for exploring a rail's behaviour interactively.

## Why it matters

Payments defects are unusually expensive. A mishandled ACH return or a missed sanctions screen is not a bug report — it is a regulatory finding, a remediation programme, and sometimes a fine. Yet rail expertise is scarce, concentrated in a few people per organisation, and hard to hire.

Payments Rail QE encodes that expertise so a tester without a decade of payments background can produce credible coverage. Typical use:

- **New rail onboarding** — a team adding FedNow gets scenario coverage that reflects instant-payment realities, not adapted ACH tests
- **Compliance evidence** — demonstrate that OFAC screening and Reg E error resolution were tested
- **Migration testing** — validate ISO 20022 message handling during a modernisation programme
- **Regression assurance** — re-run rail-specific edge cases whenever the payment engine changes

The business outcome is credible payments coverage without waiting on a scarce specialist, and materially lower regulatory exposure.

## In the UI

<!-- SCREENSHOT: payments-rail-01-spec.png — Rail selection with compliance pack toggles -->
*Select the rail and the compliance packs that apply.*

<!-- SCREENSHOT: payments-rail-02-validation.png — Generated rail-aware scenarios with compliance assertions -->
*Generated scenarios, with the compliance assertions each pack requires.*

## Tips

- **Ingest your payment documentation first.** The Knowledge Base uses payments-aware chunking, so whole flows are retrieved rather than fragments — this noticeably improves scenario relevance.
- **Enable only the packs that apply.** Every pack adds obligations; enabling all of them produces coverage your programme may not owe.
- **Use the conversational mode** to explore unfamiliar rail behaviour before generating a full scenario set.

## What's new

- **June 2026** — Knowledge Base context now reaches the agent correctly; extraction quality substantially upgraded; payments-aware Knowledge Base chunking introduced.

[← Back to agents](index.md)
