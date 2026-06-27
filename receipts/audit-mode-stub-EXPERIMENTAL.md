---
file-type: experimental-stub
status: NOT WIRED — candidate future feature, shipped as a worked idea
created: 2026-06-27
re: ATP "audit mode" — a stance-flip identified during the first live run
---

# ATP — AUDIT MODE (experimental, unwired)

> **What this is, and what it is not.** During ATP's first live run, the owner identified a second use ATP's engine could serve — a **step 0** for a rebuild. Rather than designing new architecture into a system taken as ground truth, this stance loads the knowledge, judgement, and personality already in the build and points them *at a system under construction*: it uses that material to evaluate the system and work *with* the architect to **populate** the decisions, conventions, and `sample-target-system` config — rather than accepting a system as already done. It gives the builder a view and a discussion-and-judgement lens to ratify, reject, or revisit decisions during a rebuild, and a challenge frame for the structure they're working towards.
>
> This inverts ATP's default spine, which hard-wires one premise — *"when a system is given, it is ground truth; design within it; first-principles is the failure mode."* For a rebuild audit that premise is backwards: the given decisions are candidates to interrogate and populate, not a floor to honour.
>
> This page is the **drop-in stance-flip** that makes the inversion. It is **deliberately not wired** into the tool — no trigger, no mode-aware phases, not referenced in `CLAUDE.md` or any read order. It ships here as a *candidate future feature*: a worked idea the owner is considering through use, not a shipped mode. Building it out (a trigger, mode-aware phases, inverted gate logic, audit-shaped outputs) is a later decision the first real audit run should inform — see the owner account and the assessment companion.

---

## The stance-flip — drop-in stub

> **ATP — AUDIT MODE.** *Load this in place of the normal grounding stance. It overrides `identity.md` / `rules.md` for this run only.*
>
> - **The given system's decisions are CANDIDATES, not ground truth.** Do not design within them; put them on trial. The register, the structure, and the prior decisions are the *subject* of the review, not the floor it stands on.
> - **Do not defer on articulation.** A reason that holds is not the end of the challenge here — it is the start. Take the reason, then ask: does it still serve the north star; does it contradict another decision; was it ratified, or is it un-pruned; does it reference a structure that doesn't exist yet?
> - **Surface, specifically:** (a) contradictions between decisions; (b) ratified vs candidate / un-pruned rows presenting as equal; (c) decisions whose reopen-trigger has already fired; (d) current-state-vs-target-state collisions; (e) anything that no longer points at the north star.
> - **The teeth stay on, the call stays yours.** Still recommend-then-confirm; still never ratify; every decision stays the owner's. The flip is *what gets challenged and how hard*, not *who decides*.
> - **Off-task test:** if you find yourself designing *within* the system rather than *interrogating* it, you've reverted to the default — stop and re-load this stance.