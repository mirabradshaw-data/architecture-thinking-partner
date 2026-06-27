---
file-type: examples
workspace: architecture-thinking-partner
last-updated: 2026-06-26
status: active
referenced-by: [gate1-review-finalise]
---

# Worked Example — Intake & Gate 1

The front half of one full worked run: the `skill-share-prep` PRD arriving from the upstream PRD interviewer (its own worked example), through **intake** and **gate 1** (review & finalise). The run continues — scope, architecture, and the close — in `examples/examples-gate-2.md`.

This file is loaded at **gate 1**, the gentle end. The gate-2 architecture run and the calibration vignettes live in the gate-2 file and are deliberately kept out of here — the teeth belong at gate 2, not in finalisation.

---

## The input — the PRD this picks up

The PRD arrives at `input/prd-skill-share-prep.md`, `status: draft`, `build-target: existing`, `target-workspace: team-ops` (the host's existing system). Its mission is the host's quoted north star — *"someone junior standing up, teaching the room something, and realising they're not the dumbest person in the building."* Its §6 breakdown is a draft with three flagged-open questions the architecture has to resolve later:

- one "session-build" skill, or separate deck and run-sheet skills?
- are the format rules (45-min slot, segment shape) **governance**, or just **config** the skills read?
- the recap connection — does it need **write-back** to the shared team doc, or read-only?

That's the seam: the interviewer drafted and flagged; this tool resolves. (Gate 1 doesn't resolve those — it confirms the PRD is build-ready and finalises it; gate 2 resolves them.)

---

## Good — intake & gate 1

### Intake
The PRD has `status: draft` → route to **gate 1** (a `final` PRD would skip it, and intake would copy it to `output/` instead). The `[slug]` carries over — `skill-share-prep` — so this run's outputs tie back to the PRD. The `build-target: existing` / `target-workspace: team-ops` frontmatter is noted as a **seed for scope**, not acted on: intake flags it and moves on.

### Gate 1 — review & finalise
Read as the architect about to build from it: is everything the architecture needs here, and does it hang together? It is. The mission is present (the architecture has a north star to point at), the scope is answerable (the PRD says it's `existing`), outputs have destinations, constraints are captured. The three flagged questions are *fine to carry* — gate 2 resolves them, that's its job. One gentle confirm with the host, then set **`draft → final`**; the finalised PRD lands at `output/prd-skill-share-prep.md`. The gentle end — no teeth here.

---

## Mishandled — the same PRD, at gate 1

How gate 1 goes wrong, named against the failure modes in `identity.md` and `rules.md`:

- **Manufactured gaps.** Picks at a build-ready PRD to look useful — querying settled detail, inventing concerns. *Should: a sound draft gets a quick confirm; don't manufacture review to justify the gate.*
- **Fabricated fill.** A genuinely-missing input gets papered over with a plausible-sounding assumption instead of surfaced. *Should: mark the gap open and carry it; never fabricate.*
- **Teeth in the gentle phase.** Brings a gate-2 architecture challenge ("this whole breakdown is wrong, here's how I'd structure it") into finalisation, grinding a review that should be collaborative. *Should: gate 1 surfaces gaps gently; the teeth are gate 2's.*
- **Silent finalisation.** Flips `draft → final` on its own judgment without the host's confirmation. *Should: the person confirms the finalisation; never flip the status unprompted.*

---

*The run continues in `examples/examples-gate-2.md` — scope, the architecture (with teeth), the coverage audit, and the worked vignettes.*
