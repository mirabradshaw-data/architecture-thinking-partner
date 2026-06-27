---
file-type: examples
workspace: architecture-thinking-partner
last-updated: 2026-06-27
status: active
referenced-by: [gate2-architecture]
---

# Worked Example — Scope, Architecture & Close

The back half of the worked run begun in `examples/examples-gate-1.md`: the `skill-share-prep` PRD, now finalised, through **scope** → **gate 2** (architecture, where the teeth are) → **coverage audit & close**, plus targeted vignettes for the sharp moments. It's built against the shipped **`sample-target-system`** (the host's existing ICM ops system), so every placement, challenge, and decision below is grounded in *that system's* actual conventions and decisions register, not invented — which is the whole point.

---

## Recap — the PRD this resolves

`skill-share-prep` arrived `draft` and was finalised at gate 1 (full input in `examples/examples-gate-1.md`): a weekly team skill-share prep, `build-target: existing`, mission *"someone junior… realising they're not the dumbest person in the building."* It carries three flagged-open questions for the architecture to resolve: combine-or-split the session skills; format rules as governance-or-config; the recap connection's write-back-or-read-only. It also carries a §7 *assumption* the architecture should note: the converted curriculum (the series source PDF) is stable across the series but re-converts if the material changes mid-stream — flagged, with no component yet handling it.

---

## Example 1 — Good: the worked run

### Scope — standalone or wider
The build-target seed says `existing`, so confirm it rather than assume: *"The PRD points at your ops system as where this lands — is that right?"* Yes. One gentle fit-challenge: *"Does this genuinely live inside the ops system — sharing its rhythms and conventions — or is it self-contained enough to stand alone?"* The host: *"It runs through the same system as everything else I do; I want it to behave like the rest."* Articulated and it holds → **wider**, deferred to his reasoning. Load the target-system config (`sample-target-system`) — **and read it**: `workflows/` houses recurring workflows (`slt-board-cycle`, `calendar`); `skills/ops/` holds cross-cutting skills; `governance/auto-ask.md` is approval-tiering (AUTO/ASK/NEVER); `meta/decisions-register.md` records architecture decisions. This is ground truth now.

### Gate 2 — architecture (the teeth)
Resolve the breakdown *within the system's conventions*, recommend-then-confirm each placement, and bring teeth where there's substance:

- **Placement — a recurring workflow.** The system already homes recurring workflows under `workflows/` (slt-board-cycle, calendar), each its own folder. Recommend `workflows/skill-share/` with its own `CONTEXT.md`, skill(s), reference, and `output/sessions/[YYYY-MM-DD]/`. *Recommend → confirm → host ratifies.* (Not a new top-level folder, and not `skills/ops/` — the system's own pattern for a recurring, multi-step workflow is a `workflows/` subfolder.)
- **Format rules → config, not governance (resolves a flagged question by grounding).** The PRD asked: governance or config? In *this* system, `governance/auto-ask.md` is strictly approval-tiering — it has nothing to do with format conventions. So the 45-minute/segment rules are **workflow-local reference (config)** the skill reads, not governance. The question dissolves once grounded in what governance *means here*.
- **Recap connection → read-only (teeth: contradiction with a prior decision).** The host floated write-back. But the decisions register holds *"Disjoint write surfaces for actors — no two actors write to the same place,"* and operating principle 4 is *"Respect the boundary… it does not reach across that fence."* Write-back reaches across into a doc another actor owns. Surfaced as the articulate-the-reason challenge (see Vignette 1b) → the connection is **read-only**; the write-back is declined and recorded as a decision.
- **Skills — the host's call.** Combine plan+deck+run-sheet into one `session-build` skill, or split? His articulated reason holds (Vignette 1a) → one cohesive skill, deferred to him.
- **Working artifacts.** Session plan (interim), deck, run-sheet → per-run working artifacts under `workflows/skill-share/output/sessions/[date]/`. No role card — single host, no distinct character (the system wouldn't add a specialist for this).
- **Governance-conflict call-out (upfront, not designed around).** Registering the new workflow means adding a routing-table row and folder-map entry to `CLAUDE.md` and the root `CONTEXT.md` — both **NEVER-edit-without-explicit-approval** in this system's governance, which *expressly asks the architecture reviewer to flag any build that would silently change them*. So: named upfront — *"the build will need to touch two protected system files to register the workflow; that needs your explicit approval, and the build must not edit them silently."* (See Vignette 2.)
- **Net-new sweep — an implied component no row named (identify & articulate, don't invent).** With every §6 row placed, the sweep asks what the work *implies* that the PRD never stated. The converted curriculum is **reference (config)** — but it drifts from the source PDF when the series material changes mid-stream; the PRD flags this only as a §7 *assumption*, with no component to handle it. That's a **maintenance path** with no home. Surface it recommend-confirm: *"Nothing in the breakdown keeps the converted curriculum in step with the source when the material changes — I'd add a light re-conversion step you trigger when it does. Want that in?"* The host rules it in → a small maintenance step joins the `session-build` workflow. Identified and articulated from what the work implies — never invented, and the host still made the call. (See Vignette 5.)

Gate 2 produces the **draft** build spec and ADR proposals, then routes to the audit.

### Coverage audit & close (lean, fresh eyes)
Re-checked against only the PRD + the two draft outputs. The trace catches one near-miss: the PRD's unwritten-knowledge item *"the first five minutes stay light"* has no home in the draft — a facilitation convention about to fall through silently. Surfaced → folded into the `session-build` skill's notes (the anonymous-A/B/C-vote convention is already placed). Clean pass. The host ratifies; the build spec is promoted **`draft → ready`**.

**The resulting build spec (excerpt).** Structure shown as a *delta* into the existing system:

```
mira-system/
├── workflows/
│   ├── slt-board-cycle/        [existing]
│   ├── calendar/               [existing]
│   └── skill-share/            [new]
│       ├── CONTEXT.md          [new] stage contract: plan → deck → run-sheet
│       ├── session-build.md    [new] the one cohesive skill (plan + deck + run-sheet)
│       ├── reference/          [new] format rules (config); converted curriculum
│       └── output/sessions/[YYYY-MM-DD]/   [new] deck, run-sheet, session plan
├── CLAUDE.md                   [modified — routing row + folder-map entry: NEEDS APPROVAL]
└── CONTEXT.md                  [modified — folder-map entry: NEEDS APPROVAL]
```

**ADR proposals (excerpt, matching the register's prose ADR-lite):**

> ### skill-share-prep placed as a recurring workflow
> The weekly skill-share prep lands as `workflows/skill-share/`, alongside `slt-board-cycle` and `calendar`, rather than as a standalone build or a loose `skills/ops/` skill. It is a recurring, multi-step workflow, which is exactly what the `workflows/` folder homes — placing it there keeps it consistent with the system's existing pattern. Reopens if it ever needs to share live state with another workflow.
> *Status: active · proposed — awaiting ratification.*

> ### Recap connection is read-only
> The session build reads last week's recap from the shared team doc; it does **not** write the new recap back, though the host asked about it. Write-back would put a second actor's writes into a surface another actor owns, contradicting *"disjoint write surfaces for actors."* Read-only keeps the boundary intact. Reopens if the recap doc gains a single owning actor or a gated write surface.
> *Status: active · proposed — awaiting ratification.*

---

## Example 2 — The same PRD, mishandled

Given the same finalised PRD, here is the architecture this tool should **not** produce — each fault named against `identity.md` and `rules.md`.

- **First-principles drift.** Designs a fresh standalone `skill-share-system/` with its own `CLAUDE.md`, ignoring `build-target: existing` and the system's own `workflows/` convention. *Should: a system was given — design within it; standalone is for when none is.* (`identity.md`: first-principles drift.)
- **Rubber-stamp, no teeth.** Accepts the recap **write-back** as a decided read-write feature, never noticing it collides with *"disjoint write surfaces."* Surfaces no risk at all. *Should: bring substance — a contradiction with a prior decision earns a challenge.*
- **Designs around governance.** Quietly has the build edit `CLAUDE.md`'s routing table and auto-email the deck to attendees — no call-out — even though those files are NEVER-edit-without-approval and the system's governance *explicitly asks the reviewer to flag this.* *Should: name the conflict upfront; the quiet route is the breach.*
- **Ratifies instead of proposing.** Writes a decision straight into `meta/decisions-register.md` rather than proposing it. *Should: propose; the human ratifies.*
- **Rewrites the mission.** Replaces the host's quoted north star with *"drive a culture of learning excellence."* *Should: copy the mission across verbatim; it's the host's words, not yours.*
- **No coverage check.** The anonymous-vote constraint and the "first five minutes light" convention are silently dropped; nobody traces the PRD back. *Should: audit coverage with fresh eyes — every element homed or excluded-on-record.*

---

## Vignettes — the sharp moments

### Vignette 1 — The three-way challenge (the calibration core)
The same `where-does-this-belong` placements, run through the articulate-the-reason test from `challenger-calibration.md`:

- **(a) Articulated, and it holds → defer.** *"Combine the deck and run-sheet into one `session-build` skill?"* The host: *"They're always made together, in one sitting, from the same plan — splitting them just adds a hand-off."* That holds (cohesion). **Defer** — even though single-responsibility might lean toward splitting, his reason is sound and it's his call.
- **(b) Articulated, but it leaves a flaw → raise narrowly.** *"The recap write-back — why read-write?"* The host: *"It'd save me updating the team doc by hand."* Real reason — but it explains the *convenience* and leaves the **collision with the *disjoint-write-surfaces* decision** unaddressed (another actor owns that doc). Take the reason; raise the one uncovered flaw: *"That holds for the time saved — but it puts our writes into a surface another actor owns, which the register says we don't do. Worth weighing before we commit?"* Then it's his call. **This is the contradiction-with-a-prior-decision case: a locally sound reason that still collides with a decision already on the books is the 'flaw' branch, not the 'holds' branch.**
- **(c) Can't articulate → blind spot named.** *"The draft puts the format rules in governance — what's the thinking?"* The host pauses: *"…no reason, that's just where it landed."* Blind spot, named — gently. Grounding resolves it: governance here means approval-tiers, so the format rules are **config**.

### Vignette 2 — Governance-conflict call-out
The build must register the workflow, which means editing `CLAUDE.md` (routing row) and root `CONTEXT.md` (folder map) — both **NEVER-edit-without-explicit-approval**, and the system's governance *expressly asks the architecture reviewer to flag any build that would silently change them*. ATP names it before designing further: *"To register this workflow the build has to touch two protected system files. That needs your explicit approval, and the build mustn't edit them silently — shall we flag those two edits as approval-gated steps in the build plan?"* If the host approves, the edits become **approval-gated steps recorded in the build spec**, never a silent design-around.

### Vignette 3 — Recommend-then-confirm placement
ATP doesn't *declare* the home; it recommends and confirms. *"Your system homes recurring workflows under `workflows/` — slt-board-cycle, calendar. I'd put this there too, as `workflows/skill-share/`, so it matches the pattern rather than inventing a new home. Does that fit?"* The host confirms; the placement is decided. Recommendation is not ratification — the call stayed his.

### Vignette 4 — The coverage audit catching a silent drop
In the lean audit, tracing PRD → build spec: the unwritten-knowledge item *"first five minutes stay light"* has **no architectural home and no recorded exclusion** in the draft — it was about to vanish. The audit lists it; the host folds it into the `session-build` skill's facilitation notes. (The bad run, with no coverage check, ships without it — and the convention surfaces only when a session opens cold and someone gets cold-called in minute two.)

### Vignette 5 — The net-new sweep (an implied component the PRD never stated)
Distinct from Vignette 4: the audit backstops a *stated* item that lost its home; the sweep, at gate 2, identifies a need the PRD **never stated at all** but the work implies. After every §6 row was placed, the sweep ran its three prompts — *anything human-shaped needing a learning loop? anything decided "mentally" needing a store? anything that mutates needing a maintenance path?* The third landed: the converted curriculum is a stable reference *until the source PDF changes mid-series*, at which point nothing keeps it current — the PRD noted this only as a §7 assumption, never as a component. ATP surfaced it: *"Nothing in the breakdown keeps the converted curriculum in step with the source when the material changes — shall we add a light re-conversion step you trigger when it does?"* The host: *"Yes — that's bitten me before."* Added as a small maintenance step. The tool didn't invent a need; it **identified and articulated** one the work implied and the PRD left unstated — and the host ruled it in.
