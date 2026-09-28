# Marketing Angle Strategist

Turns an evidence pack into a scored, prioritised angle map — claims with hypotheses, evidence trails, counter-arguments and arithmetic somebody else can audit.

An angle is a CLAIM. "Problem-led" is an angle; "UGC talking head" is a format; "you have been doing this wrong" is a hook. It stays on claims, because mixing the three is how a test that was supposed to compare messages ends up comparing production styles.

Every angle is scored out of 100 with its arithmetic shown, so the number can be argued with rather than believed. Proven signal comes from how long competitors have run that claim; evidence strength from how many customer quotes support it and how close they sit to purchase; and anything unsupported by the landing page, blocked by compliance, or requiring proof the brand does not have is removed before scoring and recorded with its reason — because a rejection is information the hook stage needs.

It has no web access by design. It cannot fetch new evidence, only process what was observed and pasted in. That restriction is the point: it makes invention impossible rather than merely discouraged.

## What this is, precisely

A FindAgent **`mcp-tool`** agent. Each of its 6 tools is a
`prompt-template` action: the tool renders an instruction and hands it back to the
model that called it.

Two consequences worth being blunt about, because they decide whether this is useful to you:

- **It calls no model and reaches no network.** A tool call costs nothing and returns
  the same text for the same input, every time. There is no API key, no credential
  slot and no egress.
- **It observes nothing.** It has no access to your repository, your logs, your
  analytics or your devices. Every template is written so that supplying nothing
  produces an honest statement of what is missing rather than a confident-looking
  answer about data nobody provided. If you ask for a report and give it no findings,
  it will tell you the work has not been done — not invent it.

## Tools

| Tool | What it returns | Required input |
|---|---|---|
| `build_claim_inventory` | Index every distinct claim visible in the evidence with its sources, before any clustering or scoring, so nothing is merged away before it has been seen. | `evidence_pack` |
| `derive_angles` | Produce the angle set in two required tracks — derived from observed evidence, and original but anchored to a real page element or customer quote — each with its hypothesis and counter-argument. | `claim_inventory` |
| `block_unsupported_angles` | Remove angles the brand cannot actually run — unsupported by the page, blocked by compliance, requiring a forbidden competitor or absent proof — and record each rejection with its reason. | `angles`, `frozen_brief` |
| `score_angles` | Score each angle out of 100 with the arithmetic shown — proven signal from competitor longevity, evidence strength from quote volume and purchase proximity, and fit against the brief. | `angles` |
| `pick_first_wave` | Choose which angles ship first and which wait, balancing score against how different the angles are from each other, so the first test can actually be read. | `scored_angles` |
| `draft_angle_map` | Assemble the angle map for the hook stage — angles, hypotheses, evidence, rejections and the first wave — refusing to produce one when no evidence was supplied. | `campaign_context` |

Optional inputs render as empty when omitted. Every template names that case and says
what it could not determine, so an empty slot degrades into a stated gap rather than a
dangling clause.

## Part of a department

This agent is one member of the **marketing video ad** department, a
hub-orchestrator team of 7. The hub is `marketing-brief-scoper`, which locks the brief every later
stage reads; the other members are
reached through it or called directly as `<alias>__<tool>`.

| Agent | Stage in the pipeline |
|---|---|
| `marketing-brief-scoper` | 1 — interviews for the brief and freezes it (department hub) |
| `marketing-ad-researcher` | 2 — competitor harvest plan, longevity ranking, customer voice, coverage |
| `marketing-angle-strategist` | 3 — scored angle map with auditable arithmetic |
| `marketing-hook-writer` | 4 — the modular creative bank, built on verbatim customer language |
| `marketing-ad-scripter` | 5 — modules, continuity kits, prompts, assembly map, QA protocol |
| `marketing-production-planner` | 6 — blockers, tracks, cost estimate, shoot briefs, release gates |
| `marketing-ad-tester` | 7 — clip QA, test design, readout, and the feedback loop back to 3, 4 and 5 |

Each member is published independently and works on its own.

## Provenance

`source/angler.md` is the markdown skill this agent was converted from. The tool templates carry its
instructions, parameterised: anything the original hard-coded to one team's repositories,
file paths or people became an input you supply, and where a template would otherwise
depend on reading something it cannot reach, it asks for that material as an argument
instead.

## Licence and use

Published by Kata Team on FindAgent. Free to connect.
