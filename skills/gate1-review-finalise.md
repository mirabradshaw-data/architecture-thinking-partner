---
file-type: skill
workspace: architecture-thinking-partner
last-updated: 2026-06-26
status: active
referenced-by: [skills/CONTEXT.md]
---

# Skill — Gate 1: Review & Finalise

The first gate. Take a `draft` PRD, pressure-test it for what the architecture will need, surface the gaps *with the person*, resolve them, and set **`draft → final`** on their confirmation. This is the **gentle end** of the tool — collaborative, low-friction, surfacing *for* the person, not challenging them. The teeth (real architectural risk, inconsistency with past decisions) belong at gate 2; don't bring them here. `identity.md` is who you are; `rules.md` holds the gate; this skill is the procedure.

## When this runs

Reached from intake when the PRD is `draft`, or when the person chose to review a no-status PRD. A PRD already at `final` skips this entirely (intake routes it straight to scope) — don't re-open a final PRD unless the person asks.

## Inputs

### Reference (already read, from `CLAUDE.md`)
- `identity.md`, `CONTEXT.md`, `rules.md` — don't re-load.

### Reference (loaded here as needed)
- `examples/examples-gate-1.md` — the worked intake + gate-1 example (the input PRD and what a review-ready PRD looks like, good and mishandled). The gate-2 architecture run and the calibration vignettes live in `examples/examples-gate-2.md` and are **not** loaded here — the teeth stay out of this gentle phase.

### Working (per run)
- The PRD from `input/` (in hand from intake).
- Any accompanying materials (build-notes, transcript, deck) — read as context that may surface gaps the PRD alone wouldn't.
- The conversation itself.

## How to run it

You're not re-running the interview, and you're not architecting. You're reading the PRD as the architect who's about to build from it and asking one question throughout: **is everything the architecture will need actually here, and does it hang together?** Where it isn't or doesn't, surface it gently and resolve it with the person. Don't manufacture gaps to justify the gate — a sound draft gets a quick confirm and moves on.

- **Read it as the downstream architect.** Hold the PRD against what gate 2 will need to design well. The point isn't generic completeness; it's *build-readiness*.
- **Pressure-test for the three things that block architecture:**
    - **Gaps the architecture needs.** An output with no destination; an input with no source or format; a step with no actor or trigger; missing constraints or governance the build must respect; a missing or empty artifact breakdown; absent success criteria. And the two that decide the *next* phases: is the **scope** answerable (does the PRD say enough to know standalone vs an existing system?), and is the **mission / north star** present (so the architecture points at something)?
    - **Contradictions.** An output nothing produces; an input nothing uses; steps that conflict; a constraint a step violates; a build-target that contradicts what the person now says.
    - **Anything load-bearing that's only implied.** A dependency, a scale assumption, a data source the person knows but didn't write down — the unwritten knowledge the build would otherwise guess at.
- **Surface gently, one thread at a time.** Offer what you see and ask — *"The PRD names the weekly digest as an output but doesn't say where it lands — where does it go?"* Propose-and-confirm, not interrogate. The person is the authority on their work; you're the second pair of eyes catching what slipped.
- **Resolve, or mark open — never fabricate.** Where the person answers, fold it into the PRD. Where they can't, mark the gap **explicitly open** and carry it forward to gate 2 as known-open. A named hole is useful to the build; an invented fill is a landmine. Don't paper a gap with a plausible-sounding assumption.
- **Don't redesign the workflow.** You make the PRD complete and coherent enough to architect; you don't improve the process or re-spec the work. If the person wants to change something, capture *their* change — don't author one for them.
- **Set `draft → final` — only on the person's confirmation.** Once the gaps are resolved or marked open and the PRD hangs together, confirm with the person — *"I think this is ready to architect from — shall I set it to final?"* — and only then set `status: final`. **Never flip the status on your own judgment.** Write the finalised PRD to `output/prd-[slug].md`; the original in `input/` stays as the source.

## Decision points

- **Gap, or fine?** Surface a gap only where the architecture genuinely needs it. Polish for its own sake isn't this gate's job — a build-ready draft gets confirmed, not picked at.
- **Resolve, or mark open?** If the person can answer, fold it in. If they can't, mark it open and carry it forward. Don't stall the gate hunting for an answer that isn't available, and don't fabricate one.
- **Finalise, or hold?** Proceed to `final` when the PRD is build-ready *even with a few named-open gaps* — gate 2 can design around or surface them. Hold only when an open gap is genuinely architecture-blocking (e.g. no sense of what the thing produces, or no answerable scope). Say which it is; don't block on a non-blocking gap, and don't wave through a blocking one.
- **Their call, or yours?** Every gap-fill, contradiction-resolution, and the finalisation itself is the person's. You surface and propose; they decide. This holds even at the gentle end.

## Edge cases

- **The draft is already build-ready.** Confirm what you checked, note nothing's blocking, set `final`. Don't manufacture a review to justify the gate.
- **A gap the person can't close.** Mark it open, note it'll be carried into gate 2, and proceed if the rest is sound. Don't fabricate; don't stall.
- **A contradiction the person must settle.** Surface both sides; let them choose. Never silently pick one.
- **They want to rescope or change the work mid-review.** Fine — capture their changed intent into the PRD as theirs. You're not redesigning; you're recording the change they directed.
- **"Just architect it as-is."** Respect it — but first name any architecture-blocking gap so the choice is informed. If they still want to proceed, set `final` and carry the opens to gate 2.
- **A blocking gap and an impatient person.** Don't flip to `final` to be agreeable. Name the one thing that genuinely blocks the architecture and why; hold there. (This is the one place the gentle end holds firm — see `rules.md` on not advancing a gate without sound footing.)

## Quality checks (before you set `final`)

- The PRD was read as the architect would — for build-readiness, not generic polish.
- Every gap the architecture needs is either resolved with the person or explicitly marked open.
- No contradiction is left unflagged.
- The mission / north star is present, so the architecture has a target.
- The scope is answerable — the PRD says enough to know standalone vs an existing system.
- Nothing was fabricated; open gaps are named, not filled.
- The workflow wasn't redesigned — changes recorded are the person's.
- Nothing was architected — the breakdown wasn't resolved, no structure was designed (that's gate 2).
- The person confirmed the finalisation; the status wasn't flipped on your own judgment.
- The finalised PRD is written to `output/prd-[slug].md` at `status: final`; the `input/` original is untouched.

## Outputs

- `output/prd-[slug].md` — the PRD, finalised: gaps resolved or marked open, contradictions settled, `status: final`. The one written output of this phase. The `input/` original stays as the source it was finalised from.

Hand the finalised PRD back to the person to confirm before scope and architecture build on it. Then route to **`scope-standalone-or-wider.md`**.
