# Skills — Phase-Flow Router

Last updated: 2026-06-26

## Purpose

This file tells you which sub-skill drives which phase, and what to load when. This is a **single pipeline with two branch points**: a PRD comes in, flows through up to five phases, and a build spec comes out. Read the phase you're in; load its skill before working it, not while.

The two named **gates** (gate 1 — phase 2; gate 2 — phase 4) hold the human-in-the-loop architecture work; the closing phase (phase 5) runs the coverage check and takes the final ratification. Phases 1 and 3 are routing/scope. Nothing advances or closes without the person's confirmation — see `rules.md`.

## The flow

```
  intake ──┬─ draft ─────────► gate 1 ──► scope ──► gate 2 ──► audit & close
           ├─ final ─────────────────►   scope ──► gate 2 ──► audit & close
           └─ no YAML ─► ask ─┬─"review"► gate 1 ──► scope ──► gate 2 ──► audit & close
                              └─"final"────────►    scope ──► gate 2 ──► audit & close
```

## Phase routing

| Phase | Entry / branch | Skill | Loads here | Gate |
|---|---|---|---|---|
| **1 · Intake** | Trigger fires (a PRD in `input/` + the person asking to architect it / typing **ARCHITECT**). Detect the PRD's status. | `intake.md` | the PRD from `input/`; any accompanying materials alongside it | — *(routing only)* |
| ↳ *branch* | `draft` → **gate 1** · `final` → skip to **scope** · no YAML / unrecognised → ask *"is this the final PRD, or should we review it together first?"* then branch | | | |
| **2 · Gate 1 — review & finalise** | PRD is `draft`, or the person chose to review | `gate1-review-finalise.md` | `examples/examples-gate-1.md` | **GATE** — surface gaps *with the person*, resolve, then set `draft → final` on their confirmation |
| **3 · Scope — standalone or wider** | PRD is `final` | `scope-standalone-or-wider.md` | the resolved reference architecture: `_config/sample-target-system/` (wider) **or** `_config/generic-icm-baseline.md` (standalone) | soft gate — confirm existing-system? then *gently* challenge fit; **load the reference architecture here, not at entry** |
| **4 · Gate 2 — architecture** | Scope resolved + reference architecture loaded | `gate2-architecture.md` | `reference/where-does-this-belong.md`, `reference/build-spec-template.md`, `reference/adr-proposal-template.md`, **`reference/challenger-calibration.md` (here only)**, `examples/examples-gate-2.md` | **GATE** — resolve breakdown, design structure, surface risk (teeth), call out governance; produce **draft** build spec + ADR proposals, then route to phase 5 |
| **5 · Coverage audit & close** | Gate 2 produced draft build spec + ADR proposals | `coverage-audit-and-close.md` | **only** the PRD + draft `build-spec-[slug].md` + draft `adr-proposals-[slug].md` — *deliberately lean; none of the gate-2 kit* | **CLOSE** — verify every PRD element has a home or recorded exclusion (fresh eyes: sub-agent → clear+re-enter → adversarial), resolve gaps, person ratifies, promote build spec `draft → ready` |

## Loading discipline

- **Always already read** (from `CLAUDE.md`'s read order, before any phase): `identity.md`, `CONTEXT.md`, `rules.md`. The skills don't re-load these.
- **Reference architecture loads at phase 3, not at entry.** Which one (target-system vs generic baseline) isn't known until the scope question is answered — so don't read `_config/` upfront.
- **`challenger-calibration.md` loads at gate 2 only.** The teeth belong in phase 4; keeping the calibration out of phases 1–3 keeps the gentle end gentle and the earlier context lean.
- **Templates load at the phase that produces their output** — `build-spec-template.md` and `adr-proposal-template.md` at gate 2; `where-does-this-belong.md` at gate 2 (placement).
- **Coverage audit loads lean — phase 5 only.** `coverage-audit-and-close.md` loads *only* the PRD + the two draft outputs — **not** the reference architecture, calibration, lens, templates, or examples. Loading the generative kit here would defeat the phase's purpose; the skill carries the full reasoning.

## When this router doesn't cover something

If a PRD or request doesn't fit the flow — it isn't an ICM-shaped problem, or it's a harm-risk domain — don't force it through. See *When to decline* in `rules.md`. If something genuinely falls outside both this router and the rules, stop and surface it to the person rather than proceeding.
