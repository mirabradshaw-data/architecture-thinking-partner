---
file-type: reference
workspace: architecture-thinking-partner
last-updated: 2026-06-27
status: active
referenced-by: [gate2-architecture, scope-standalone-or-wider]
---

# Where Does This Belong?

> The placement lens. It answers two questions for each element of the architecture: **what artifact type is it**, and — when there's a target system — **where in that system does it go**. In this stage you use it to **recommend-and-confirm**: you recommend a home, confirm it with the person, and the person ratifies. *(Upstream, a PRD interviewer used the same lens only to propose-and-flag.)* You never decide placement silently, and you never write to the target system's real files (see `rules.md`).
>
> Unlike the upstream draft stage, **the remediation guidance below applies here** — this is the stage that actually places content against a real architecture. But it applies as a *recommendation to confirm*, not a move you make unilaterally.

## Why this file exists

Every system that mixes stable knowledge, behavioural patterns, and procedural steps eventually drifts — facts end up in skills, procedures end up in memory, current-state notes end up in config. Once that drift starts, files contradict each other, the same content gets edited in two places, and people stop trusting what's where. Resolving the PRD's artifact breakdown *well* — placing each element in the right type and the right home — is how the architecture avoids baking the drift in from day one. A wrong-home placement is one of the substance categories that earns a challenge (see `challenger-calibration.md`).

## Decision rules — which artifact type does this belong to?

| If the content is... | It belongs in... |
|---|---|
| A behavioural stance, learned pattern, or correction that shapes judgment across many future tasks | a **memory** file |
| Stable domain knowledge — facts about people, places, situations, the domain, terminology | a **reference** file (when scoped to one deployment, a **config** file) |
| A step-by-step process for a repeatable task | a **skill** file |
| A permission, approval, or escalation rule (who can do what, what needs review) | **governance / rules** |
| Identity, ownership, or judgment stance — who does the work and why | a **role card** (or a **specialist**, when the work warrants a distinct character with its own voice) |
| The mission / doctrine — *why* the work is worth defending: the north star, what it must always do, what it refuses | **splits** — the behavioural stance → a **memory**; the belief/identity it commits the owner to → the **role card**. Together they are the *chest* of the build. |
| A folder's or stage's current-state description (inputs, process, outputs) | the relevant **`CONTEXT.md`** (**context**) |
| Per-run content being produced or acted on | a **working artifact** |
| Configuration for connecting to an external tool (setup, MCP info, common operations) — a *connection spec* | a **connection** spec — any permissions in it are proposed defaults only, until ratified into governance / rules |

## Where in the target system does it go? (wider only)

Artifact *type* is half the answer; for a wider build, the other half is **location** — which folder, alongside which existing files, under whose governance. Here the target system is ground truth:

- **The target system's own conventions win.** Where the system already has a place and a pattern for this type of thing — a `skills/ops/` folder, a `config/` directory, a decisions register — recommend *that* home, in *its* idiom, not a generic one. Read the system's `CLAUDE.md` / `CONTEXT.md` / folder map before recommending placement; designing a fresh home where the system already has one is the first-principles failure mode (`identity.md`).
- **Reuse before you add.** If the system already has an artifact that does this job, recommend reusing or extending it — not a parallel new one. Duplication is a substance category for challenge.
- **Respect the governance boundary.** If placement would touch a file or area the system's governance gates, surface the governance conflict (see `rules.md`); don't recommend a placement that quietly crosses a rule.
- **Standalone case:** there's no target system, so location collapses to the generic ICM baseline's structure (`_config/generic-icm-baseline.md`). Recommend within that standard shape.

## The recommend → confirm → ratify flow

For each element of the breakdown:

1. **Recommend** a type (from the table) and, when wider, a home (from the system's conventions) — with the reasoning, in one line.
2. **Confirm** with the person — *"I'd put this in governance rather than config, because it's an approval rule and that's where the system keeps them — does that fit?"* A recommendation is an opening, not a verdict.
3. **The person ratifies.** The placement is decided when they agree. If they place it elsewhere and can articulate why, defer (run it through the calibration). If a genuine risk remains, raise it narrowly — then it's their call.

This replaces the upstream stage's propose-and-flag: there, every row was a flagged draft for later. Here, you carry each to a recommendation and a confirmed home — resolving the breakdown the PRD left open.

## When the rule isn't obvious

If the content has elements of more than one category — a learned pattern that involves a specific stable fact — split it, and recommend the split:

- Pattern (behavioural) → memory
- Fact (stable knowledge) → reference (config, when deployment-scoped)
- The memory entry references the fact rather than restating it

The same drift-correction recommendations apply (recommend the move; the person ratifies):

- A memory file carrying step-by-step procedure → recommend the procedure move to a skill, referenced.
- A skill carrying learned patterns or judgment shifts → recommend the patterns move to memory, referenced.
- A config file carrying approval rules → recommend they move to governance / rules.
- A role card carrying procedure, governance, or current project state → recommend each move to its own type.

## When you're still not sure

Recommend with the uncertainty named, and confirm — don't silently resolve, and don't leave it merely flagged-for-later (that was the upstream stage's job). *"This could be memory or config — I lean config because it's deployment-scoped, but it's a judgment call. Your read?"* gives the person a recommendation to react to *and* the honest uncertainty. A confirmed placement beats both a silent guess and an unresolved flag.

## When to update this file

When a new artifact type enters the picture, add a row to the decision table. When a target system uses a placement convention the generic table doesn't capture, that's the system's call to honour at runtime — not a change to this file.
