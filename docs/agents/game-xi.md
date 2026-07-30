# Game-Xi

> **Game Accessibility Agent** — validates games against the accessibility guidelines platform holders certify against, plus age-rating metadata standards.

| | |
|---|---|
| **Port** | `8006` |
| **Stack** | Python · FastAPI |
| **Stage** | Specialised — runs independently of upstream agents |
| **Source** | `agents/game-xi/` |

## What it does

Game-Xi responds to a commercial risk specific to games publishing: accessibility and rating compliance are now gating requirements rather than optional improvements. Xbox certification tests against published accessibility guidelines, and a failed submission means a slipped launch date; an incorrect age-rating descriptor can force a store delisting. Its input is the game specification or build details to be assessed, and its output is a set of findings mapped to the specific guideline each one fails, grouped by category and severity, with remediation guidance a designer or producer can act on. Findings for the two accessibility standards are organised across the four impairment categories the guidelines themselves use, covering visual, audio, motor and cognitive needs. Testers and business analysts use it ahead of a certification submission, and product owners use it to convert published guidelines into a prioritised, assignable backlog. Running both accessibility standards together is advisable, because they overlap without being equivalent — the industry baseline catches issues the Xbox guidelines assume, while the Xbox guidelines carry the certification weight. Assessing at specification stage gives by far the best return, since a remappable-controls gap found in a design document costs a conversation while the same gap found in a submitted build costs a release slot. Rating metadata is checked separately, verifying that age and content descriptors are correct before a store submission is made. Typical scenarios are pre-certification checks, accessibility backlog creation, rating metadata assurance, and design review while changes are still cheap. For publishers the outcomes are fewer failed certification submissions and a broader addressable audience, since accessibility features benefit far more players than those who strictly require them. Game-Xi runs independently of the requirement pipeline and can be applied at specification or build stage.

Game-Xi checks a game build or specification against three published standards:

| Standard | What it covers |
|---|---|
| **XAG** — Xbox Accessibility Guidelines | Microsoft's certification-facing accessibility requirements |
| **GAG** — Game Accessibility Guidelines | The widely adopted industry baseline |
| **IARC / ESA metadata** | Age-rating and content-descriptor metadata correctness |

For XAG and GAG, findings are organised across the four impairment categories the guidelines themselves use:

- **Visual** — contrast, text scaling, colour-only information, subtitle legibility
- **Audio** — subtitles, captions, visual substitutes for audio cues
- **Motor** — remappable controls, input timing, held-input alternatives
- **Cognitive** — difficulty options, tutorial clarity, reading load

**What you give it:** the game specification or build details you want assessed.

**What you get back:** findings mapped to the guideline they fail, grouped by impairment category and severity, with remediation guidance a designer or producer can act on.

## Why it matters

Accessibility is no longer optional in games publishing — Xbox certification tests against XAG, and a failed submission is a slipped launch date. Age-rating metadata carries its own commercial risk: an incorrect IARC descriptor can force a store delisting.

Typical use:

- **Pre-certification check** — find XAG gaps before submitting a build, not after rejection
- **Accessibility backlog** — turn published guidelines into a prioritised, assignable work list
- **Rating metadata assurance** — verify IARC and ESA descriptors before store submission
- **Design review** — assess accessibility at specification stage, while changes are still cheap

The business outcome is fewer failed certification submissions, a broader addressable audience, and accessibility tracked as a requirement rather than handled as a late-stage scramble.

## In the UI

<!-- SCREENSHOT: game-xi-01-rules.png — Game specification input with standard selection (XAG / GAG / IARC) -->
*Choose which standards to assess against.*

<!-- SCREENSHOT: game-xi-02-coverage.png — Findings grouped by impairment category and severity -->
*Findings grouped by impairment category — visual, audio, motor, cognitive.*

<!-- SCREENSHOT: game-xi-03-remediation.png — Per-finding remediation guidance mapped to the guideline -->
*Each finding cites the guideline it fails, with remediation guidance.*

## Tips

- **Run XAG and GAG together.** They overlap but not completely — GAG catches baseline issues XAG assumes, while XAG carries the certification weight.
- **Assess at specification stage** for the best return. A remappable-controls gap found in a design document costs a conversation; found in a submitted build it costs a release slot.

[← Back to agents](index.md)
