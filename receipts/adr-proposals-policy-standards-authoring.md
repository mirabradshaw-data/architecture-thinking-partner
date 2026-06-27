---
file-type: adr-proposals
slug: policy-standards-authoring
source-build-spec: output/build-spec-policy-standards-authoring.md
created: 2026-06-27
status: proposed
---

# ADR Proposals — Tech & Data Policy/Standards Authoring Suite

Decisions that shaped this architecture, proposed for ratification. Standalone build — these are fresh entries (no existing register to match or supersede); the owner ratifies them into the new workspace's own `decisions-register.md` once built, and/or her build-decisions log. **Proposed, not ratified** — strip the italic *proposing context* line on ratification.

---

### Standalone, independent workspace

The suite is built as its own ICM workspace, not wired into the owner's personal operating system. It produces company documents and a company-facing KM register (a different output class); it has a self-contained foundation (template, voice-print, standard-sections, approval tiers that differ from the owner's standard governance); the owner intends to ship the PRD and build spec as exemplars but not build-and-ship this instance; and independence from the outset preserves the option to take it from her style to org house style and ship a version to peers. Coupling it into the personal system would add coupling without shared governance and risk the two bleeding together.

Reopens if the suite ever needs to share live governance or state with the personal system.

Status: active
*Proposing context (strip on ratification): owner ruled `independent` at the PRD stage and confirmed at ATP scope, against a gentle wider-vs-standalone challenge. — proposed, awaiting ratification.*

### Engine/config split as the portability seam

The workspace separates a reusable **engine** (entry contract, role card, governance shape, memory, foundation + pipeline stage folders, materiality taxonomy, tools) from a deployment-specific **`_config/`** (+ `connections/`). The two files `_config/voice-print.md` and `_config/standard-sections/` are the designated swap seam: replacing them and re-running F2 changes the house voice (owner's style → org house style) without touching the engine. This is what makes the "ship to peers" option real rather than a future rewrite.

Reopens if a third deployment surfaces a stance currently in the engine that is actually deployment-specific (move it to `_config/`).

Status: active
*Proposing context (strip on ratification): serves the owner's reason for independence (reason 4 — style → house style portability). — proposed, awaiting ratification.*

### Three living registers, deliberately separated

`roadmap.md` (what to build, in what order, how it hangs together), `decisions-register.md` (what we decided and why — engine + captured positions), and the external KM register (per-document lifecycle: status/effective/owner/version/next-review) are three distinct artifacts in three homes. The PRD originally conflated the first and third under "suite register / roadmap"; gate 1 split them, and gate 2 added the decisions-register as a third.

Reopens if two of the three are found to be maintained as one in practice.

Status: active
*Proposing context (strip on ratification): resolves the §3/§6 conflation (friction-log F4) and homes GAP 2. — proposed, awaiting ratification.*

### Internal decisions-register the engine consults

A living `decisions-register.md` records engine/architecture decisions **and** captured policy-position & priority decisions (the PRD's "decisions made mentally"). The engine consults it at stage 01 (what's already decided), stage 03 (does this contradict a settled position), and F4 (capture). This stops the system being a blank slate the owner re-explains to, and directly serves the north star — "we know where the lines are because we've already established them."

Reopens if the register grows unwieldy and warrants splitting engine-decisions from position-decisions.

Status: active
*Proposing context (strip on ratification): GAP 2, owner-identified. — proposed, awaiting ratification.*

### Voice print split: stance to memory, profile to config

The PRD flagged "voice print — reference vs memory." Resolved as a split: the *writing stance* (plain / Einstein / intent-led) is a **memory** that shapes every drafting judgment (`memory/writing-stance.md`); the *style profile + exemplars* is a **config reference** the drafting skill consumes (`_config/voice-print.md`), and is the portability seam.

Reopens if the stance and the profile prove inseparable in use.

Status: active
*Proposing context (strip on ratification): resolves PRD §6 voice-print flag (R1). — proposed, awaiting ratification.*

### Standard-sections: promote-to-standard gate + deterministic helpers

The standard-sections library is a config reference that the workflow writes back to (Step 5 folds in new recurring sections). To prevent a write-back-on-use library bloating and drifting into a junk drawer, a section earns entry only through an explicit **promote-to-standard gate** (the owner's call at Step 5), and deterministic `tools/` maintain the index and flag drift. Local scripts are first-class in ICM canon; they are constrained to **mechanical work only** (no branching).

Reopens if the gate proves too heavy for the cadence, or if a tool starts needing to make a judgment (which would mean it should be a skill, not a script).

Status: active
*Proposing context (strip on ratification): R2; mitigates the drift risk in build-spec §7. — proposed, awaiting ratification.*

### Cohesion via a tiered cohesion-index, with a hermetic mirror

Cohesion-checking (Step 3) runs against a summarised search surface, not the full policy texts: Tier 1 `cohesion-index/index.md` → Tier 2 `cohesion-index/[slug].md` (per-doc summary) → Tier 3 `mirror/` (local full text), escalating only on a flagged concern. The mirror is a local copy, not a live connector, to honour the hermetic scope ruling; mirror and index update inside Step 5, so they cannot be staler than the last stored document.

Reopens if summaries prove insufficient to catch real conflicts (then the mirror tier carries more load), or if the hermetic ruling is relaxed (then a connector is back on the table).

Status: active
*Proposing context (strip on ratification): R3; scoped-context discipline + hermetic ruling. — proposed, awaiting ratification.*

### Learning loop: capture-learnings refreshes voice-print and memory

A `capture-learnings/` stage, triggered off Step 3, reads the delta between the engine's draft and the owner's hand-polished version and **proposes** updates to `_config/voice-print.md` and `memory/`. Without it the voice-print is static — built once at F2 and never learning from the owner's shaping. Gated: proposals only, the owner ratifies, never silent.

Reopens if the proposals prove noisy and need a confidence threshold before surfacing.

Status: active
*Proposing context (strip on ratification): GAP 1, owner-identified. — proposed, awaiting ratification.*

### KM register and approval record in Notion (business tier)

The KM register — status, effective date, owner, version, next-review, **and the approval record** — lives in Notion at business-tier licensing, which is becoming the owner's team infrastructure (demand intake, ticketing, KM/documentation). The approval record is the most audit-relevant slice; placing it in Notion rather than company-governed infra was challenged on the owner's own durability reasoning (the documents went to company infra for durable institutional memory). The owner ruled Notion, owns that decision, and will put the safeguards in place to make it a formal register — an **explicit call made at the architecture stage**, which closes the PRD's deliberately-open KM-tooling question (PRD §7 carried it "to validate"; the owner validated and decided Notion here).

**Accepted risk, conditional:** the formal-register status depends on those safeguards being implemented. Reopens if the safeguards don't materialise, or if records-management governance requires the approval record in the company tenant.

Status: active · until:<formal-register safeguards confirmed in Notion>
*Proposing context (strip on ratification): R4; the one accepted risk carried from gate 2. — proposed, awaiting ratification.*

### Pipeline stages as folders; stage-major live, document-major archive

Each foundation step and pipeline stage is a self-contained folder (`CONTEXT.md` + `skill.md` + `references/` + `output/`), with stage N's `output/` feeding stage N+1 — the canonical ICM glass-box audit trail, not a flattened set of skill files. The live audit unit is the stage (stage-major); on completion a run is archived **document-major** (`archive/[slug]/`) so each policy's full history is co-located, before the pipeline runs again.

Reopens if concurrent document runs make stage-major outputs hard to navigate before archival.

Status: active
*Proposing context (strip on ratification): owner-ruled after gate-2 caught a flattening (friction-log F6). — proposed, awaiting ratification.*

### Approval tiers proposed, not hardened

Policy → CEO sign-off; Standards/Guidelines → owner issues under the approved policy, CEO & SLT consulted (not a formal gate). The owner is ~98% confident but will not let this harden into governance unconfirmed. The build encodes the tiers as **proposed-pending-confirmation** in `_config/approval-tiers.md`, referenced by `governance.md`; they become a hard governance rule only on the owner's ratification.

Reopens on owner confirmation (hardens) or on a change to the org's approval model.

Status: until:<owner confirms the tiers>
*Proposing context (strip on ratification): carried from PRD §7. — proposed, awaiting ratification.*

### Hermetic, self-supplying engine

The engine reaches into no external system at runtime. Approved documents are *exported* to company infrastructure and *mirrored back* locally for cohesion-checking; the KM register is *written to* at Steps 4–5; nothing is *read live* from an external system mid-run. This was the owner's scope-phase ruling ("fully hermetic and self-supplying"), and it is load-bearing: it justifies the `mirror/`, the tiered cohesion-index (rather than a live connector), the export-not-read connection model, and the end-of-build "hermetic seam" audit criterion. Recorded here because the architecture rests on it and it was not in the PRD.

Reopens if the cost of maintaining the mirror outweighs the value of hermeticism, or if a live connector becomes necessary (e.g. real-time corpus checks).

Status: active
*Proposing context (strip on ratification): records the scope ruling the coverage audit found undocumented (audit S1). — proposed, awaiting ratification.*

### Review engine — recognised future scope (deferred)

Every document carries lifecycle metadata — a review cycle and a materiality review trigger. This build *captures and stores* that metadata but does not act on it. The firing behaviour is a recognised **future-scope component**: a *review engine*, triggered on a review-cycle date rolling around **or** a materiality trigger, that re-reviews the document's content, updates versioning, makes required updates, and re-classifies/re-routes the document's tier where materiality has shifted. Deferred deliberately — named and recorded so it is a conscious exclusion, not a silent gap.

Reopens when the suite has enough live documents that review/materiality triggers begin firing — that is the signal to build the review engine.

Status: active · until:<review/materiality triggers start firing in practice>
*Proposing context (strip on ratification): resolves coverage-audit GAP-A as a conscious deferral. — proposed, awaiting ratification.*

### NZ regulatory floor enforced as a Step 3b clearance gate

The NZ regulatory floor (§2 non-negotiable: every document "must clear" the relevant baseline) is enforced, not just supplied. Beyond being a drafting input at Step 2, a dedicated **Step 3b regulatory-clearance check** verifies the document *clears* the floor before it can become approval-ready — a distinct skill/context from the 3a cohesion-check (so the two aren't conflated), run in the same refine pass (no extra pipeline pass). Mirrors how suite-cohesion got both a rule and a check, rather than leaving a non-negotiable as passive reference material.

Reopens if per-subject regulatory complexity warrants a heavier verification step than an in-pass check.

Status: active
*Proposing context (strip on ratification): resolves coverage-audit W2 (a non-negotiable with no enforcement home). — proposed, awaiting ratification.*

---

*Proposed for ratification into the workspace's `decisions-register.md` (once built) and/or the owner's build-decisions log. Nothing here is written to a live register by this stage.*
