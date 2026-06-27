---
file-type: skill
workspace: architecture-thinking-partner
last-updated: 2026-06-26
status: active
referenced-by: [skills/CONTEXT.md]
---

# Skill — Scope: Standalone or Wider

The phase between finalising the PRD and architecting it. Settle one question — **does this work stand alone, or join an existing system?** — and load the reference architecture gate 2 will design against. This is the **soft end**: ask, *gently* challenge the fit, and confirm with the person. The build-target named in the PRD is a *seed* to confirm here, never an assumption. `identity.md` is who you are; this skill is the scope procedure. The teeth come at gate 2, not here.

## When this runs

Reached after gate 1 (the PRD is now `final`), or straight from intake when the PRD arrived `final`. Carries forward the **build-target seed** intake flagged (a `build-target` / `target-workspace` in the PRD frontmatter), if any.

## Inputs

### Reference (already read, from `CLAUDE.md`)
- `identity.md`, `CONTEXT.md`, `rules.md` — don't re-load.

### Working (per run)
- The finalised PRD (in hand).
- The build-target seed from intake, if any.
- The conversation itself.

### Loaded *at the end of this phase* (once scope is settled)
- **Standalone** → `_config/generic-icm-baseline.md` — the default ICM reference architecture.
- **Wider** → the **target-system config**: the existing workspace's `CLAUDE.md` / `CONTEXT.md` / governance / decisions, provided by the person (or `_config/sample-target-system/` as the shipped worked example). **Read it — when a system is given it is ground truth, not a starting suggestion** (see `rules.md`).

## How to run it

One question, asked plainly, then a light challenge on the answer — never a grind. The aim is to *place the work deliberately*, not to win an argument about where it goes. Whichever way it lands, the person decides; you make sure the decision was made on purpose.

- **Confirm the build-target seed first, if there is one.** If the PRD named a target system, raise it as a question, not a fact — *"The PRD points at the ops system as where this lands — is that right, and is that the system we should design it into?"* A seed is a read to confirm; never assume the system exists or that the work belongs in it.
- **Ask the scope question.** If there's no seed, ask directly — *"Does this slot into an existing system you've already built, or does it stand on its own?"*
- **No → standalone.** Take it at face value, with one gentle probe: *"Nothing it should connect to or inherit governance from?"* If they're clear, move on. Load `_config/generic-icm-baseline.md` as the reference architecture and route to gate 2.
- **Yes → gently challenge the fit.** This is the soft challenge, not the teeth. Test whether the work genuinely belongs *in* the system or is self-contained enough to stand alone — *"Does this really live inside it — sharing its governance, its data, its rhythms — or is it self-contained enough that wiring it in adds coupling you don't need? Either's fine; I just want it placed on purpose."* Apply the articulate-the-reason test **gently**: if the person can say why it belongs there (or doesn't), defer — it's their call. If they can't, surface that softly as worth a second thought — then still leave the call to them. Don't push past one round here; real placement teeth are a gate-2 matter.
- **Load the reference architecture — this is the phase that does it.** Once scope is settled, load the right reference: the generic baseline (standalone) or the target-system config (wider). Don't load it earlier — which one applies isn't known until now (see `skills/CONTEXT.md` loading discipline). When wider, actually **read** the target-system's files; gate 2 designs *within* them, and first-principles design where a system was given is the failure mode in `identity.md`.
- **Hand the scope decision to gate 2.** Pass forward: standalone vs wider, the loaded reference architecture, and the confirmed (or revised) build-target. Don't begin architecting — that's gate 2.

## Decision points

- **Seed: confirm or assume?** Always confirm. A build-target in the PRD frontmatter is a starting point to check with the person, never proof the system exists or that the work belongs in it.
- **Challenge: push or defer?** One gentle round. If the person can articulate why it belongs (or stands alone), defer — it's their call. If they can't, surface it once as worth reconsidering, then defer anyway. Save real placement teeth for gate 2.
- **Wider but no config provided?** If they have a system but can't hand over its files, you can't ground in it. Either ask for the `CLAUDE.md` / `CONTEXT.md` / governance / decisions, or fall back to the generic baseline — and **flag the limitation**: placement and governance fit will be approximate without the real system in front of you.
- **Standalone now, wider later?** If the work is standalone today but plausibly joins a system later, note it for gate 2 (it shapes how cleanly the architecture should bound itself) — but design standalone for now.

## Edge cases

- **The seed contradicts what they now say.** Go with the person, not the frontmatter — and note the change for gate 2.
- **They're unsure whether it belongs in the system.** That's a real finding, not a failure. Lay out the trade-off plainly (coupling vs cohesion) once, and let them choose; don't decide for them.
- **Wider, but the system is large.** You don't need all of it — load the parts that bear on this work: governance, the decisions that touch the same area, the conventions and folder map. Note what you didn't read rather than implying full coverage.
- **They want both — a standalone tool that also plugs in.** Capture the intent; gate 2 designs the boundary. Don't resolve the architecture here.

## Quality checks (before you route to gate 2)

- The scope is settled: standalone or wider, decided with the person.
- The build-target seed (if any) was confirmed or revised — never assumed.
- The fit got one gentle challenge, not a grind — and the call was left with the person.
- The right reference architecture is loaded: generic baseline (standalone) or the target-system config (wider) — and, if wider, actually read, not just noted.
- Any limitation (wider but no config provided; large system partially read) is flagged, not papered over.
- Nothing was architected — scope settles placement-level direction; gate 2 does the design.

## Outputs

Scope produces **no file**. It establishes the run's state for gate 2 — standalone vs wider, the loaded reference architecture, the confirmed build-target — and routes to **`gate2-architecture.md`**. The first architecture outputs (the build spec, the ADR proposals) come at gate 2.
