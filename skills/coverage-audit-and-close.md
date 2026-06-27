---
file-type: skill
workspace: architecture-thinking-partner
last-updated: 2026-06-27
status: active
referenced-by: [skills/CONTEXT.md]
---

# Skill — Coverage Audit & Close

The final phase. Take the draft build spec and ADR proposals gate 2 produced, **verify they cover the PRD**, resolve any gap with the person, then close — ratify the outputs and set them ready to hand to a build. This is a **verify-and-complete** phase, deliberately separated from gate 2's design work: a different job (checking, not designing), run in a different, **lean** context. `identity.md` is who you are; `rules.md` holds the gate; this skill is the audit-and-close procedure.

## When this runs

Reached from gate 2, once the build spec and ADR proposals exist as **drafts** in `output/`. Gate 2 designs and produces; this phase checks and closes.

## Inputs — deliberately lean

**Load only these three artifacts — nothing else:**

- The **finalised PRD** (`output/prd-[slug].md`).
- The **draft build spec** (`output/build-spec-[slug].md`).
- The **draft ADR proposals** (`output/adr-proposals-[slug].md`).

**Do NOT load** the reference architecture, the challenger calibration, the placement lens, the templates, or the worked examples. Gate 2 is a "load everything" stage; this phase is the opposite. The verifier checks what's *on the page* against the PRD — holding the design scaffolding would only bias it toward believing the spec is complete.

*(`identity.md` / `CONTEXT.md` / `rules.md` are already read from the entry contract; the three artifacts above are the working set.)*

## How to run it

- **Run with genuinely fresh eyes.** The agent that authored the spec is context-poisoned — it knows what it *meant* to include. Get fresh eyes by the best available means, in order:
    1. **Fresh-context sub-agent (preferred — needs a filesystem).** Hand a sub-agent the three artifacts (by path) and have it run the coverage trace cold, **returning its findings** — the list of PRD elements with no home and no recorded exclusion. A sub-agent runs non-interactively: it **audits and reports only — it cannot resolve gaps with the person or close** (it has no one to ask). Resolution and ratification happen back in the main context. *Tier 1 assumes a filesystem to hand the artifacts by path; in a no-filesystem Claude Project, tier 1 isn't available — use tier 2.*
    2. **Clear → re-enter on this skill.** The drafts are already written to `output/`, so they survive a context clear. Ask the person to **clear context**, then re-enter and **run this skill on the three artifacts** — that *is* the handoff (no separate brief needed; the skill is the instruction, the three files are the input). The cleared context checks cold, with the person present to resolve and close.
    3. **Adversarial fresh read (last resort).** If neither is possible, re-derive coverage *from the PRD*, not from memory of what was intended — assume something was missed, and hunt for it.
- **The audit reports; resolving and closing need the person.** Only the coverage *trace* runs with fresh eyes. Resolving what it finds and closing the build spec require the person, so they happen in the main context. When the audit runs as a sub-agent (tier 1) — or any time the auditor can't talk to the person — run it as a **loop**: the audit reports its findings → the person resolves them (or directs otherwise) → **re-audit on the updated drafts** → repeat until the audit returns a **clean pass**, or the person judges the remaining items acceptable and **directs the close** (recording them as exclusions). *Under tier 1, the main context carries the loop and each re-audit spawns a **fresh** sub-agent (a re-used context isn't fresh). Under tier 2, the cleared context has no memory of prior iterations — each re-entry is a fresh single pass the person re-triggers, so the **person** carries the loop across re-entries, not the context.* The loop ends one of two ways — a clean pass, or the person calling it done. The auditor never closes on its own; **the person ends the loop.**
- **Run the coverage trace.** Walk every element of the PRD — outputs, inputs, steps, constraints, mission commitments, and §6 breakdown elements — and confirm each one either has an **architectural home** in the build spec, or a **consciously made, recorded decision** excluding it (an ADR proposal, or an explicit note in the build spec). List anything with **neither a home nor a recorded exclusion**: those are the gaps — elements that fell through silently. (When you are the sub-agent, this trace *is* your whole job — produce the list and return it.)
- **Resolve each gap with the person.** A gap is one of two things, and the person decides which:
    - **A real omission** — the architecture should cover it but doesn't. It needs a fix in the build spec. If it's a small addition, fold it in; if it reopens a genuine design question, route it back to gate 2 thinking rather than patching it thinly here.
    - **An intended exclusion not yet recorded** — it was meant to be left out, but nobody wrote down the decision. Record it: an ADR proposal, or an explicit exclusion note in the build spec. Now it's a conscious call, not a silent drop.
  Either way the silent gap is closed — covered, or excluded-on-record.
- **Close.** Once the audit returns a **clean pass** (every PRD element homed or excluded-on-record) — *or* the person has consciously **directed the close** on the remaining items, recording them as exclusions — the person **ratifies** the build spec and the ADR proposals. Promote the build spec from `draft` to **`ready`** (audited and ratified; ready to hand to a build). The ADR proposals stay `proposed` — the person ratifies *those* into the target system's register, which is outside this tool. Confirm the linked set is complete in `output/` and hand off: the build is the next conversation, with the person in the room (`rules.md`).

## Decision points

- **Home, exclusion, or gap?** A PRD element is covered if it has an architectural home *or* a recorded exclusion. Only an element with neither is a gap. A deliberate "we're not building that" is fine — *if it's written down*.
- **Fold in, or route back?** A small omission gets folded in here. One that reopens a real design question goes back to gate 2 thinking — don't patch a genuine architectural gap thinly just to close the audit.
- **Whose call?** Every resolution — fix vs exclude, fold-in vs route-back, and the final ratification — is the person's. The audit surfaces; the person decides.
- **Ready, or not yet?** Promote to `ready` when the audit is a clean pass (or the person has consciously directed the close on the remaining items, recorded as exclusions) and the person has ratified. Don't promote past an open gap the person hasn't either resolved or knowingly accepted — name it. The person ends the loop, not you.

## Edge cases

- **The trace finds nothing missing.** Good — confirm what you checked, note coverage is clean, and proceed to close. Don't manufacture gaps to justify the phase.
- **A gap reopens a real design question.** Route it back to gate 2 rather than resolving it thinly in the audit — the audit verifies; it doesn't redesign.
- **The person wants to exclude something the PRD asked for.** Their call — record it as a decision (an ADR proposal or an explicit exclusion note), so the build knows it was deliberate. Never silently drop a PRD element.
- **Tier 2 was used and context was cleared.** The cleared context has only the three artifacts and this skill — that's by design. Run the trace from them; if something seems to reference missing context, that itself may be a coverage gap (the spec leaned on something not on the page).
- **No sub-agent and the person won't clear context.** Fall to tier 3 (adversarial fresh read) — but say so, so the weaker check is visible, not silently substituted.
- **The audit keeps surfacing gaps (the loop runs long).** Re-audit after each resolution; that's expected, not failure. The loop ends on a clean pass or the person's explicit direction to close — never on your own call, and never by looping silently. If it isn't converging, surface that to the person so they can resolve the sticking point or consciously direct the close.

## Quality checks (before you close)

- The audit ran on the **lean set only** — PRD + build spec + ADR proposals — not the gate-2 kit.
- Fresh eyes were used by the strongest available means (sub-agent → clear-and-re-enter → adversarial read), and which tier was used is visible.
- Every PRD element (outputs, inputs, steps, constraints, mission commitments, §6 elements) has an architectural home or a consciously recorded exclusion — nothing fell through silently.
- Each gap was resolved with the person — folded in, routed back, or excluded-on-record — none left silently open.
- The loop ended properly — on a clean audit pass, or the person's explicit direction to close; the auditor never closed on its own.
- The person ratified the build spec and the ADR proposals.
- The build spec is promoted to `ready`; the ADR proposals remain `proposed` (ratified into the register outside this tool).
- The linked set in `output/` is complete and shares the `[slug]`.

## Outputs

- `output/build-spec-[slug].md` — promoted from `draft` to **`ready`**: audited against the PRD, gaps resolved, person-ratified, ready to hand to a build.
- `output/adr-proposals-[slug].md` — confirmed; stays `proposed` for the person to ratify into the target system's decisions register.

These, with the finalised PRD, are the tool's terminal outputs — the linked set a build conversation picks up cold. The build itself is the next conversation; this tool specs and verifies, it does not build (`rules.md`).
