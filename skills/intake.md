---
file-type: skill
workspace: architecture-thinking-partner
last-updated: 2026-06-27
status: active
referenced-by: [skills/CONTEXT.md]
---

# Skill — Intake

The first phase. Find the PRD, read it, detect its status, and route to the right next phase — and nothing more. Intake orients; it does not review (that's gate 1) and it does not architect (that's gate 2). `identity.md` says who you are; `skills/CONTEXT.md` shows where this sits in the flow. This skill is the detect-and-branch procedure that opens it.

## Inputs

### Reference (already read, from `CLAUDE.md`)
- `identity.md`, `CONTEXT.md`, `rules.md` — don't re-load them here.

### Working (per run, from `input/`)
- The **PRD** — required, the floor. Read it.
- Any accompanying materials dropped alongside it — the build-notes and transcript an upstream PRD creator produces as a linked set, or a deck/exemplar/spec. Read as supporting context; never required.

## Pre-flight check (before anything else)

Confirm the floor before intake proper begins: a PRD must be in hand.

- **Locate the PRD in `input/`.** Identify the file that is the PRD — by `prd-[slug]` naming, by PRD shape (a problem statement, workflow steps, an artifact breakdown), or by a PRD's frontmatter. Treat the rest (build-notes, transcript, decks) as supporting context, not the spec.
- **If no PRD is present, stop and get one provided.** Ask for it — *"Drop the PRD into `input/` and I'll pick it up."* Don't proceed, don't accept a brief, deck, or transcript *as* the PRD, and don't reconstruct one from them. A PRD is the floor; the run does not start without it.
- Only once a PRD is in hand do you continue below.

## How to run it

Intake is mechanical on purpose — it's a small, careful gate, not a conversation. Keep it light and don't start critiquing the PRD; the moment you're surfacing gaps you've crossed into gate 1.

- **Establish the slug.** Take the `[slug]` from the PRD (its filename or frontmatter) so the run's outputs tie back to it — and, downstream, to the whole suite's linked set. If there's no clear slug, propose a lowercase-hyphenated one from the PRD's subject and confirm it in passing. Pin it before any file is written (see `CLAUDE.md` naming).
- **Detect the status — from the PRD's YAML frontmatter:**
    - **`status: final`** → the PRD is taken as final. **Skip gate 1**; **copy the PRD unchanged to `output/prd-[slug].md`** so the downstream phases (including the coverage audit) have the PRD in the linked set — gate 1 would otherwise write it, and a final PRD bypasses gate 1. Then route straight to **scope** (`scope-standalone-or-wider.md`). Don't re-open a final PRD unless the person asks — *or* unless it's architecture-blocking-thin (see edge cases).
    - **`status: draft`** → route to **gate 1** (`gate1-review-finalise.md`) to review and finalise.
    - **No YAML, no status, or an unrecognised value** (e.g. `in-progress`, `v2`) → **don't guess and don't be brittle.** Ask: *"Is this the final PRD, or should we review it together first?"* — *"review"* → gate 1; *"final"* → scope. On a **soft or ambiguous answer** (*"mostly,"* *"basically final"*), default to **gate 1**: review is the safe branch, because a wrong *"final"* skips a needed review (a one-way cost), while an unnecessary review is cheap.
- **Note the build-target seed — don't act on it.** If the PRD's frontmatter names a `build-target` / `target-workspace` (an upstream PRD creator may record this), carry it forward as a *seed* for the scope question — something to **confirm with the person**, never an assumption that the system exists or that the work belongs in it. The scope phase owns that call; intake only flags it.
- **State the route, then hand off.** Tell the person briefly what you found and where you're going — *"This PRD is a draft, so we'll review and finalise it first, then move to architecture"* — and pass to the routed skill. Don't begin the next phase's work inside intake.

## Decision points

- **Which file is the PRD?** The one with PRD shape / `prd-[slug]` naming / a PRD's frontmatter. Build-notes and transcripts are companions, not the spec. If two files both look like PRDs, ask which to architect.
- **Status ambiguous?** Never infer `final` vs `draft` from how polished the PRD looks. If the frontmatter doesn't say it plainly, ask. A wrong guess either skips a needed review or re-opens a settled PRD.
- **No PRD, or a non-PRD doc?** Ask for the PRD. Don't accept a brief, a deck, or a transcript *as* the PRD, and don't write one to fill the gap — that's the upstream PRD stage, not this one.

## Edge cases

- **No frontmatter at all.** Ask the final-or-review question; branch on the answer.
- **`input/` has a full upstream linked set** (prd + build-notes + transcript). Take the PRD as the spec; read build-notes and transcript as supporting context that may surface gaps for gate 1. The PRD's status still drives the branch.
- **Multiple PRDs in `input/`.** Ask which one to architect this run. Don't try to merge them.
- **A `final` PRD that's visibly thin.** Respect the status by default — but if it's missing something **architecture-blocking** (no mission / north star for the architecture to point at, or a scope that can't be answered), say so once and **offer to re-open gate 1 despite the `final` status**. If the person agrees, route to gate 1; if not, honour `final` and carry the gap forward (gate 2 will surface it, but can't invent what's missing). For a merely-thin-but-buildable final, note it once and route to scope.
- **The PRD names a build-target that contradicts what the person now says.** Don't resolve it here. Flag it and let the scope phase settle it with the person.

## Quality checks (before you hand off)

- The PRD is identified and read; companions noted as context, not spec.
- The `[slug]` is established and pinned.
- The status branch is determined — read from frontmatter, or asked and answered — never guessed.
- The build-target seed (if any) is carried as a flag for scope, not acted on.
- The route is stated to the person, and the next skill is the one the branch points to.
- Nothing was reviewed or architected — intake stayed in its lane.

## Outputs

Intake produces **no file** in the usual (draft) path — it establishes the run's state (which PRD, the slug, the status branch, any build-target seed) and routes to the next phase. **The one exception:** a `status: final` PRD is copied unchanged to `output/prd-[slug].md` here (see the status-detect step above). The other written outputs come later — the finalised PRD at gate 1, the build spec and ADR proposals at gate 2.
