---
file-type: skill
workspace: architecture-thinking-partner
last-updated: 2026-06-27
status: active
referenced-by: [skills/CONTEXT.md]
---

# Skill — Gate 2: Architecture

The second gate, and where the tool earns its keep. Take a finalised PRD and the reference architecture, **resolve the artifact breakdown the PRD left open**, design the ICM structure, and produce the **build spec** and the **ADR proposals** — surfacing genuine risk and inconsistency with past decisions along the way, calling out any governance conflict upfront, and leaving every call the person's. This is the **teeth end**: collaborative still, but with real challenge. `identity.md` is who you are; `rules.md` holds the gate; this skill is the procedure.

## When this runs

Reached from scope, once standalone-vs-wider is settled and the reference architecture is loaded (the generic baseline, or the target-system config). The PRD is `final`. The build-target is confirmed.

## Inputs

### Reference (already read, from `CLAUDE.md`)
- `identity.md`, `CONTEXT.md`, `rules.md` — don't re-load.

### Reference (loaded **here**, at gate 2)
- `reference/challenger-calibration.md` — the teeth-but-not-fighting calibration. **Gate 2 only.** Load it now; this is the phase it's for.
- `reference/where-does-this-belong.md` — the placement lens: recommend type + home, then confirm.
- `reference/build-spec-template.md` — the shape of the build spec you produce.
- `reference/adr-proposal-template.md` — the shape of the ADR proposals you produce.
- `examples/examples-gate-2.md` — the worked scope → architecture → close run, the mishandled run, and the vignettes *(as needed)*.

### Working (per run)
- The finalised PRD (in hand).
- The reference architecture loaded at scope — **ground truth when a system is given** (`identity.md`); design within it.
- The scope decision, the confirmed build-target, and any gaps gate 1 marked open.
- The conversation itself.

## How to run it

You're designing *with* a competent architect, not for them and not over them. You resolve what the PRD left open, you design the structure, and you challenge with substance as you go — surfacing risk, inconsistency, over-engineering, duplication, and wrong-home placement, and leaving each call theirs. Review isn't a step you do at the end; it runs *while* you architect.

- **Orient on the mission — and carry it verbatim.** Re-read the PRD's mission; the architecture points at it, and drift from it is a failure mode (`identity.md`). When it lands in the build spec, **quote it exactly — never rewrite, reword, or neutralise it** (`build-spec-template.md` §0). The mission is the person's own words and stays theirs.
- **Hold the reference architecture as ground truth.** With a target system, design *within* its conventions, governance, and prior decisions — read before you reason; designing a fresh structure where the system already has one is the first-principles failure mode. Standalone: design against the generic ICM baseline.
- **Resolve the artifact breakdown — this is what the PRD left open.** Walk each element of the PRD's §6. Run it through `where-does-this-belong.md`: recommend a **type** and — when wider — a **home** in the system's idiom, with the reasoning in a line. **Reuse before you add:** if the system already has an artifact for the job, recommend extending it, not a parallel new one. **Confirm each with the person** — recommend, confirm, they ratify. No row stays flagged-for-later; that was the upstream stage. This resolves the breakdown into the build spec's §3. **Go beyond §6:** the breakdown is the artifact list, but the architecture has to give *every* PRD element a home — outputs, inputs, steps, constraints, and the mission — not only the §6 rows. Home them all here; the coverage audit is a backstop, not the primary net.
- **Sweep for net-new needs the PRD implies but didn't list.** The step above homes every element the PRD *states* — even the ones not in the §6 table; this sweep does the opposite job: it identifies and articulates components the PRD *implies but never states at all*. Before routing onward, ask explicitly — does any PRD element imply a component the breakdown never named? Three recurring ones, by name:
    - **a learning / feedback loop** — for anything the human *shapes* or hand-edits (a voice print, a draft the owner polishes): with no path to feed those edits back, the shaped artifact goes stale.
    - **a decisions / positions store** — for anything the PRD says is decided *"mentally,"* held in someone's head, or "captured as we go": it wants its own register so positions aren't relitigated — not a loose line folded into a roadmap.
    - **a maintenance path** — for anything that *mutates* (a living library, a register that grows): name how it's kept current, not only where it lives.
  Surface each as a recommend-confirm, the same as a §6 row — the person rules it in or out. This step identifies and articulates — it surfaces what the work implies but no one wrote down — it doesn't decide: you recommend, the architect calls it. The coverage audit is the backstop, but catch the implied needs *here*, where they can still shape the design.
- **Design the structure.** From the resolved breakdown, assemble the ICM structure — the folder tree with a clean **engine/config split** (reusable engine; deployment-specific `_config`), and the per-component build detail. **Wider: show the delta in context** — current-state → future-state, or a tree annotated `[new]` / `[modified]` / `[existing]` — not a from-scratch redraw of the whole system (`build-spec-template.md` §1).
- **Bring the teeth — review as you architect.** As you design, surface substance, per `challenger-calibration.md`: genuine architectural risk, inconsistency with a past decision, over-engineering, duplication, wrong-home placement, drift from the why. On each, run the **articulate-the-reason** test — surface it as a question about the reasoning, not a verdict, and respond by where the reason lands (the three branches are in Decision points below, and in full in `challenger-calibration.md`, loaded here). One good challenge beats five; surface once, then leave the call theirs. Don't rubber-stamp (surfacing nothing) and don't fight (pushing your design over a sound one) — both are failures.
- **Call out governance conflicts upfront.** Where the PRD or the architecture would cross a rule in the target system (an approval gate, a "no unilateral system-file changes" rule), **name it before designing around it** and resolve it with the person. If they choose to change the rule, that's a *proposed governance change* (an ADR), not a silent relaxation. Quietly architecting around a rule is the breach (`rules.md`).
- **Assemble the build spec.** Fill `build-spec-template.md`: the mission (quoted), the structure, the per-component detail, the resolved breakdown, placement & fit, the staged-and-gated build plan, the end-of-build audit, and the open questions / accepted risks carried forward. Write it as a **draft** — it reflects the placements and decisions you've already confirmed with the person through the design, but the holistic coverage check and the final ratification come at the audit phase, not here.
- **Propose the ADR entries.** Fill `adr-proposal-template.md` with the decisions that shaped the architecture — placement calls, the engine/config split, reuse-vs-build, governance resolutions, accepted risks. **Propose; never ratify.** Match the target system's register format (prose or table). A decision the build supersedes is *proposed* as a supersede, never a silent rewrite.
- **Produce the drafts and route to the audit.** Write the build spec and ADR proposals to `output/` as **drafts** under the `[slug]`. Gate 2 ends here; the holistic coverage check and the person's final ratification are the next phase — `coverage-audit-and-close.md`, run lean. **You spec it; you don't build it** (`rules.md`).

## Decision points

- **Resolve or flag?** Resolve. Unlike gate 1, this phase carries each breakdown element to a recommended, confirmed placement — recommend-and-confirm, not leave-it-flagged.
- **Resolve what's listed, or surface what's implied too?** Both. Resolve every §6 row — *and* run the net-new sweep for needs the PRD implies but didn't list (a learning/feedback loop for anything human-shaped; a decisions/positions store for anything held "mentally"; a maintenance path for anything that mutates). A component the work needs but no one named is still yours to surface — recommend it; the person calls it.
- **Reuse or build new?** Reuse or extend what the system has; build new only where the system genuinely lacks it or what it has won't serve. An unjustified new artifact where one exists is duplication — a challenge category.
- **Challenge or defer?** Run the 3-way test. Holds → defer. Leaves an unaddressed risk → raise it narrowly. Can't articulate → name the blind spot. Never push a preference; never supply their reason for them.
- **Design around governance, or call it out?** Always call it out. If the person wants the rule changed, propose the change as an ADR; never relax it silently.
- **Propose or ratify (ADR)?** Always propose. The person ratifies into the register; you never write to it.
- **Draft done, or hold?** The gate-2 draft is done when the breakdown is resolved, the structure designed, risks surfaced, governance clean, and the mission quoted intact — then route to the audit. The holistic coverage check and the final ratification are the next phase (`coverage-audit-and-close.md`), not here. Hold (don't route onward) only if a genuine architecture-blocking question is unresolved — name it.

## Edge cases

- **The PRD's §6 is empty or all-flagged** (the upstream stage left it minimal). Resolve it from scratch with the person via the lens — don't assume placements to fill the gap, and don't wave it through unresolved.
- **The person wants to cross governance.** Their call — but surface it first, and if they proceed, record it as an accepted risk *and* propose the governance change as an ADR. Never a silent design-around.
- **A real risk the person accepts.** Record it in the build spec's open-questions/accepted-risks (§7), and as an ADR if it shaped a decision — so the build knows it was a conscious call, not an oversight.
- **The mission is thin or absent** (gate 1 should have caught it — but a `final` PRD skipped gate 1). The architecture still needs a why to point at. Surface the gap; don't invent a mission to fill it. If it's genuinely missing, **offer to route back to gate 1 to resolve it with the person** (the PRD arrived final and bypassed the review); if they decline, it's a finding to carry, not paper over.
- **Standalone.** No target system: design against the generic ICM baseline, no placement-in-system, and the ADR proposals are fresh entries (no existing register to match or supersede).
- **The build is large / `gate2-architecture` is straining.** Stage the build plan into reviewable units. If this skill itself is doing too much in one pass, that's the signal to split it (the spec left that option open) — flag it rather than producing a sprawling, unreviewable spec.

## Quality checks (before you hand off)

- The artifact breakdown is fully resolved — type and home, confirmed with the person; no flagged-for-later rows.
- The net-new sweep was run — components the PRD *implies* but didn't list (a learning/feedback loop for shaped artifacts; a decisions/positions store for anything held "mentally"; a maintenance path for anything that mutates) surfaced and recommended, not left for the audit to catch.
- Grounded in the target system's conventions and decisions (wider); reuse-before-add applied; no duplication of what the system has.
- The structure has a clean engine/config split; deployment specifics live only in `_config`.
- Wider: the change is shown as a delta in context, not a from-scratch redraw.
- The teeth were applied — real risks, inconsistencies, over-engineering, and wrong-home placements surfaced via the 3-way test; nothing rubber-stamped, nothing fought; every call left with the person.
- Governance conflicts were surfaced upfront and resolved with the person — none designed around silently.
- The mission is quoted exactly in the build spec — not rewritten, reworded, or neutralised.
- The build spec is complete per the template, drafted — the holistic PRD-coverage check and the person's ratification are the next phase (`coverage-audit-and-close.md`), not here.
- The ADR entries are proposed (not ratified), match the target register's format, and any supersede is proposed as a supersede.
- Nothing was built or instantiated — this stage specs; it does not build.
- Outputs are written to `output/` as **drafts** under the `[slug]` (`build-spec-[slug].md`, `adr-proposals-[slug].md`) and routed to `coverage-audit-and-close.md`.

## A good exchange vs a bad one

**Bad — rubber-stamp + first-principles:**
> Here's a clean structure: a `validators/` folder, a `rules/` folder, a `memory/` store… *(Designed from scratch, ignored that the system already keeps rules in `governance/`; surfaced no risk; confirmed nothing.)*

**Good — grounded, recommend-confirm, teeth where they're earned:**
> The PRD's validation step is a rule about what needs approval — in your system that's governance, not a new folder, so I'd put it in `governance/auto-ask.md` rather than standing up a `rules/` directory. That fit?
> One thing worth a look: the PRD has the digest writing to `_dashboard/`, but your decisions register says `_dashboard/` is GUI-only, never written by content steps — that's an inconsistency with a prior decision. Is there a reason to write there, or should the digest land in `output/` and the dashboard read it?

The good version recommends within the system's own conventions, confirms rather than imposes, and ties the challenge to a decision already on the books — teeth, grounded, not fighting. The full worked architecture this builds toward lives in `examples/examples-gate-2.md`.

## Outputs

- `output/build-spec-[slug].md` — the architecture, per `build-spec-template.md`: mission (quoted), structure, build detail, resolved breakdown, placement & fit, staged build plan, end-of-build audit, open questions / accepted risks. Written as a **draft** (`status: draft`).
- `output/adr-proposals-[slug].md` — the decisions worth recording, per `adr-proposal-template.md`, written as drafts. Proposed, never ratified.

Both are gate 2's **draft** outputs. They route to **`coverage-audit-and-close.md`**, which verifies coverage against the PRD with fresh eyes, takes the person's ratification, and promotes the build spec to `ready`. They share the `[slug]` with the finalised PRD — the linked set travels together — but gate 2 does not close them out; the audit phase does.
