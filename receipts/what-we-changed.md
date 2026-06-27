---
file-type: receipts-note
created: 2026-06-27
re: what changed in ATP as a result of running it on a real piece of work
---

# What we changed in ATP after the proof run

These artifacts come from running ATP cold on a real architecture job — turning Chalky's PRD (see the companion Chalky receipts) into a build plan for a tech/data policy-and-standards authoring suite. The headline proof held: the PRD flowed from Chalky into ATP and came out a sound build plan with no re-asking what the work was, every gate the owner's. Running it on real work also surfaced friction, logged and folded back in rather than papered over. This note records what changed.

The model-side assessment (`assessment-atp-first-run.md`), my owner's account, and the build outputs travel with these receipts.

---

### F5 — net-new needs the breakdown didn't list
**Found:** gate 2 resolved every element the PRD *listed* cleanly, but did not independently *generate* components the work clearly implied — a learning loop to feed the owner's edits back into the voice-print (without it, the voice-print goes stale), and an internal decisions-register for positions the PRD said were "decided mentally." The owner caught both; the tool should have surfaced them.
**Changed:** added a **net-new needs sweep** to gate 2 — after resolving the breakdown, the tool now explicitly checks for implied-but-unlisted components by name (a learning/feedback loop for anything the human shapes; a decisions/positions store for anything held "mentally"; a maintenance path for anything that mutates) and surfaces each as a recommend-confirm. Backed by a new decision point and quality check.

### F6 — a template that nudged the wrong structure
**Found:** ATP's own build-spec template showed a flat `skills/` example tree, which nudged the cold run to flatten a sequential pipeline into single files — losing the stage-folder anatomy and the `output/`-chaining that *is* the ICM glass-box audit trail. The owner, who knows ICM cold, caught it. A tool whose whole job is preventing structural drift shipped a template that induced one.
**Changed:** the build-spec template now carries a "pipeline builds — stages are folders, not files" callout with the canonical numbered stage-folder pattern (copied verbatim from the baseline so the two can't drift), plus the chaining note and an explicit "flattening loses the glass-box trail" warning.

---

### Audit stance — an earlier workflow stage we identified but haven't built
Through the run, the owner realised ATP's engine could serve an *earlier* stage than the one it's built for — a **step 0** for a rebuild. Rather than designing into a system taken as ground truth, that stage would load the knowledge, judgement, and personality already in the build to evaluate a system-under-construction and work *with* the architect to **populate** its decisions, conventions, and `sample-target-system` config — a challenge-and-judgement lens to ratify, reject, or revisit decisions, rather than accepting a system as done. The stance-flip is written down as a **drop-in experimental stub** (`audit-mode-stub-EXPERIMENTAL.md` in these receipts) but deliberately **not built**: it's an earlier workflow stage that doesn't exist yet, and building it out (trigger, mode-aware phases, inverted gate logic, audit-shaped outputs) is a later decision the first real audit run should inform — not a pre-build.

---

*Sanitisation: the company is referred to as "an FMCG company in New Zealand" throughout; stray literal company names in the build-spec were caught and generalised before these shipped.*

*Honest caveat (from the assessment): this run was **standalone**, so ATP's central mechanism — grounding into an existing system and holding teeth against its decisions register — was exercised on the fallback path, not the headline one. The seam and the discipline guardrails are proven; the "holds the line when the architect's attention is elsewhere" claim is the test still ahead.*