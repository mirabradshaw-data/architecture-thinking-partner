---
file-type: stage-contract
workspace: architecture-thinking-partner
last-updated: 2026-06-26
status: active
---

# Architecture Thinking Partner — Stage Contract

## What this stage does

Takes a PRD and turns it into sound ICM architecture. The stage finalises the PRD (where it arrives as a draft), resolves the artifact breakdown against the real reference architecture, and produces a build spec — ICM structure, build detail, and placement — that a build conversation can pick up cold. Where the work joins an existing system, it designs against that system's governance and prior decisions, surfaces genuine risk and inconsistency along the way, and proposes the decisions worth recording. A final lean-context audit verifies the architecture covers the PRD before closing. Every call is left the architect's to make.

This stage owns **draft → final** and everything after it, up to but not including the build itself. It runs in two modes: **downstream** of a PRD interviewer, picking up the PRD it deliberately left open; or **independently**, on any PRD a person brings. Triggered per `CLAUDE.md`.

## Inputs

### Reference — always
- `identity.md` — who runs this, the challenger calibration, what it does not own *(role card)*
- `rules.md` — the operating rules and the two gates *(rules)*

### Reference — loaded by the skills
- `reference/where-does-this-belong.md` — the placement lens: recommends a home, then confirms *(reference)*
- `reference/build-spec-template.md` — the shape of the architecture/build-spec output *(template)*
- `reference/adr-proposal-template.md` — the shape of a proposed decisions-register entry *(template)*
- `reference/challenger-calibration.md` — the teeth-but-not-fighting detail. **Loaded at gate 2 only**, kept out of the earlier phases' context *(reference)*
- `examples/examples-gate-1.md` (gate 1) and `examples/examples-gate-2.md` (gate 2) — the worked PRD-into-architecture, good and mishandled, annotated; split so each phase loads only its own *(examples)*

### Reference architecture — one of two, resolved at the scope step
- **Wider:** the swappable `_config/sample-target-system/` (or a real target-system config dropped in) — the existing workspace's `CLAUDE.md` / `CONTEXT.md` / governance / decisions, so recommendations fit what's there. **Ground truth when a system is given — read before designing.**
- **Standalone / none provided:** `_config/generic-icm-baseline.md` — the standard ICM reference pattern, so there's always a sound architecture to design against.

### Skills
- `skills/CONTEXT.md` — routing: which sub-skill drives which phase *(routing)*
- `skills/intake.md` · `skills/gate1-review-finalise.md` · `skills/scope-standalone-or-wider.md` · `skills/gate2-architecture.md` · `skills/coverage-audit-and-close.md` *(skills)*

### Working — per run, found in `input/`
The person drops the run's materials into `input/` before starting. The stage reads from there.
- The **PRD** — **required, the minimum input.** The stage does not run without one. (Final, or a draft to be finalised at gate 1.)
- Any accompanying materials the PRD travels with, when available — e.g. the build-notes and transcript an upstream PRD creator produces as a linked set, or an existing deck/exemplar/spec. Dropped alongside the PRD in `input/`; read as supporting context, never required.
- The conversation itself.

If `input/` holds no PRD, the stage asks for one rather than proceeding — a PRD is the floor.

## Process

The procedures live in `skills/`; this contract does not restate them. At the contract level the stage runs five steps — two named gates and a closing audit:

1. **Intake** *(`skills/intake.md`)* — detect the PRD's status. `final` → skip gate 1, straight to scope. `draft` → run gate 1. No YAML / unrecognised → don't be brittle; ask "is this the final PRD, or should we review it together first?" and branch.
2. **Gate 1 — review & finalise** *(`skills/gate1-review-finalise.md`)* — pressure-test the PRD for gaps, contradictions, and anything the architecture needs that isn't there; surface them *with the person*; resolve; set **`draft → final`**. The gentle end.
3. **Scope — standalone or wider** *(`skills/scope-standalone-or-wider.md`)* — ask whether there's an existing system. No → standalone, design against the generic ICM baseline. Yes → *gently* challenge whether the work belongs there, then load the target-system config. The soft end, not where the teeth are.
4. **Gate 2 — architecture** *(`skills/gate2-architecture.md`)* — resolve the artifact breakdown against the reference architecture; produce the **draft** build spec (ICM structure, build detail, placement via the recommend-then-confirm lens); surface real risk and inconsistency with past decisions (calibration loaded here); call out any governance conflict upfront; propose ADR entries. The teeth end.
5. **Coverage audit & close** *(`skills/coverage-audit-and-close.md`)* — in a deliberately **lean** context (only the PRD + the draft outputs), verify every PRD element has an architectural home or a recorded exclusion, with fresh eyes (sub-agent → clear-and-re-enter → adversarial read); resolve any gap with the person; take their ratification; promote the build spec **`draft → ready`**. The verify-and-close end.

## Outputs

- `output/prd-[slug].md` — the PRD set to **`final`** (where it arrived as a draft). Finalisation is owned here; the build that follows is not.
- `output/build-spec-[slug].md` — the architecture/build spec: ICM structure, build detail, and placement, per `reference/build-spec-template.md`. Produced as a **draft** at gate 2, promoted to **`ready`** at close (audited against the PRD, person-ratified).
- `output/adr-proposals-[slug].md` — *proposals* for decisions-register entries, per `reference/adr-proposal-template.md`. Proposed, never ratified — the human writes them to the register.

The set shares the `[slug]` so it travels together. The `ready` build spec feeds the build conversation that follows; the ADR proposals wait on the human's ratification; none are built on here.

## What good looks like

A build spec the architect would hand to a build conversation without hesitation — ICM structure, build detail, and placement that fit the system and the decisions already made — with the sense that the review made it *better*, not that they had to defend it. Blind spots named, inconsistencies tested against the reasoning, governance conflicts surfaced and resolved, the decisions worth recording proposed for the register — and every call that was theirs left theirs. The worked version, and how it goes wrong, is in `examples/` (split by gate).

## Cross-reference

- Identity, the challenger calibration, and what it does not own: `identity.md`
- The two gates and the operating rules: `rules.md`
- Phase routing: `skills/CONTEXT.md`
- Placement lens: `reference/where-does-this-belong.md`
- Output shapes: `reference/build-spec-template.md`, `reference/adr-proposal-template.md`
- Worked good / mishandled example: `examples/examples-gate-1.md` (gate 1), `examples/examples-gate-2.md` (gate 2)
