---
file-type: build-spec
slug: policy-standards-authoring
subject: Tech & Data Policy/Standards Authoring Suite — ICM engine
source-prd: output/prd-policy-standards-authoring.md
scope: standalone
reference-architecture: generic-icm-baseline
created: 2026-06-27
status: ready
ratified: 2026-06-27 (coverage audit clean pass — owner-ratified)
companion-adr: output/adr-proposals-policy-standards-authoring.md
---

# Build Spec — Tech & Data Policy/Standards Authoring Suite

## 0 · Orientation — what this builds, and the mission it serves

**What it is:** A standalone ICM workspace that runs a recurring, human-in-the-loop workflow — *draft and maintain one tech/data policy, standard or guideline to the owner's house standard, reviewed and approved* — repeatedly across a suite. It has a one-time **foundation** layer (analyse the landscape, extract the owner's voice, define the house template, seed a sequencing roadmap) and a recurring **document pipeline** (select → draft → refine & cohesion-check → approve → register/store/maintain). The owner is the expert and the final bar; the engine augments and shapes, it never authors.

**The mission it serves** *(quoted verbatim from the PRD — the owner's own words)*:

> "Setting expectations and boundaries, simply and effectively, is a form of care. It shouldn't condescend to them or treat them as stupid."

And the one thing that has to be true, by which the build knows it worked:

> "When questions come up, we're not asking 'what should we do?' and invent it — we know where the lines are and how it works because we've already established them. And when we work with new partners, we have something to hand when requested rather than a scramble."

**Scope & placement:** Standalone — its own ICM workspace, designed against the generic ICM baseline. Fully hermetic and self-supplying (owner's scope ruling): the engine reaches into no external system at runtime; approved documents are *exported* to company infrastructure and *mirrored back* for cohesion-checking, never read live. Designed independent from the outset to preserve the owner's option to take it from her style to the company's house style and ship a version to peers — the engine/config split below is what makes that swap clean.

## 1 · The architecture — structure

Canonical ICM pipeline: each foundation step and each pipeline stage is a **self-contained folder** with its own contract (`CONTEXT.md`), skill, optional stage-local `references/`, and `output/`. Stage N's `output/` is stage N+1's input — the chain is explicit and every hand-off is an inspectable, human-editable surface. The live pipeline is **stage-major** (audit unit = the stage); a completed run is **archived document-major** (full per-document history in one place) before the pipeline runs again.

```
policy-standards-authoring/
├── CLAUDE.md                          ← L0 entry contract: map, routing, naming               [ENGINE]
├── identity.md                        ← role card: owner-as-expert, shapes-not-authors          [ENGINE]
├── CONTEXT.md                         ← L1 task routing + shared resources                      [ENGINE]
├── governance.md                      ← approval tiers · cohesion obligation · lifecycle meta    [ENGINE]
├── decisions-register.md              ← living: engine + captured-position decisions; consulted  [DATA]
├── roadmap.md                         ← build roadmap / cohesion map (what to build, in order)   [DATA]
├── memory/                                                                                      [ENGINE]
│   ├── writing-stance.md              ← plain / Einstein / intent-led
│   ├── dont-boil-the-ocean.md         ← sequence; don't do it all at once
│   └── suite-cohesion-stance.md       ← fix contradictions even when annoying
├── foundation/                        ← run-once setup; each step a self-contained folder        [ENGINE]
│   ├── CONTEXT.md                     ← foundation contract + where each output installs
│   ├── input/                         ← suite source: handbook, prior-role suite, reg texts
│   ├── f1-analyse-landscape/  (CONTEXT.md · skill.md · output/  → gap analysis → roadmap + register)
│   ├── f2-build-voiceprint/   (CONTEXT.md · skill.md · output/  → voice-print + worked-examples → _config)
│   ├── f3-define-template/    (CONTEXT.md · skill.md · output/  → house-template → _config)
│   └── f4-seed-roadmap/       (CONTEXT.md · skill.md · output/  → roadmap + standard-sections seed + captured decisions)
├── document-pipeline/                 ← the recurring engine; each stage a self-contained folder  [ENGINE]
│   ├── CONTEXT.md                     ← pipeline contract + the chaining map (output N → input N+1)
│   ├── 01_select-and-brief/
│   │   ├── CONTEXT.md · skill.md · references/
│   │   ├── input/                     ← ★ owner's run-specific drop for this document
│   │   └── output/[doc-slug]/         ← brief.md → input to 02
│   ├── 02_draft-to-standard/  (CONTEXT.md · skill.md · references/ · output/[doc-slug]/ → draft.md → 03)
│   ├── 03_refine-and-checks/   (CONTEXT.md · skill-refine.md · skill-3a-cohesion.md · skill-3b-regulatory-clearance.md · references/ · output/[doc-slug]/ → approval-ready.md, gated on 3a+3b → 04 + capture-learnings)
│   ├── 04_approve-per-tier/   (CONTEXT.md · skill.md · output/[doc-slug]/ → approval record → 05 + KM register)
│   ├── 05_register-store-maintain/ (CONTEXT.md · skill.md · output/[doc-slug]/ → store/register; updates cohesion-index + mirror; archives the run)
│   └── capture-learnings/     (CONTEXT.md · skill.md · output/[doc-slug]/ → proposed voice-print/memory updates, gated)
├── reference/
│   └── materiality-hierarchy.md       ← Policy/Standard/Guideline taxonomy                       [ENGINE]
├── tools/                             ← deterministic local scripts (mechanical only)            [ENGINE]
│   ├── index-standard-sections.*      ← maintain the standard-sections index
│   ├── build-cohesion-index.*         ← regen cohesion-index/index.md; drift detection
│   └── archive-run.*                  ← gather a completed run's stage outputs → document-major archive
├── _config/                           ← DEPLOYMENT-SPECIFIC — the swappable layer                [CONFIG]
│   ├── owner.md                       ← who the owner is (head of Data & Analytics)
│   ├── house-template.md              ← F3 output: document structure
│   ├── voice-print.md             ★   ← F2 output: how the owner writes
│   ├── worked-examples.md             ← F2 output: edge/escalation/approval exemplars
│   ├── standard-sections/         ★   ← living library + index (F4 seeds; Step 5 promotes into)
│   ├── regulatory-floor.md            ← NZ Privacy Act 2020 + per-subject baselines
│   └── approval-tiers.md              ← CEO/SLT model (proposed, owner-confirms before it hardens)
├── connections/                       ← external connection specs (proposed perms until ratified)
│   ├── document-store.md              ← company infra (on-prem / SharePoint): where approved docs live
│   └── km-register.md                 ← Notion (business tier): lifecycle register + approval record
├── cohesion-index/                    ← summarised search surface (tiered)                       [DATA]
│   ├── index.md                       ← top-level searchable index across the suite
│   └── [doc-slug].md                  ← detailed per-document summary
├── mirror/                            ← local full-text copy of approved suite (hermetic Tier-3)  [DATA]
│   └── [doc-slug].md
└── archive/                           ← completed runs, document-major (full set per doc)         [DATA]
    └── [doc-slug]/                    ← brief → draft → approval-ready → approval record → register, archived at close
```

**Engine vs config — the seam the build must hold.** The **engine** (everything `[ENGINE]`: entry contract, role card, governance *shape*, memory, foundation + pipeline stage folders, materiality taxonomy, tools) is generic and reusable — this is what ships to a peer. The **config** (`_config/`, `connections/`) is deployment-specific. The two ★ files — `_config/voice-print.md` and `_config/standard-sections/` — are the **portability seam**: swap those two and re-run F2, and the same engine writes in a different house voice (owner's style → the company's house style). The build must not let deployment specifics (owner identity, NZ regs, the company's approval tiers, Notion/SharePoint specifics) leak up into the engine.

## 2 · Build detail — per component

**Stage-folder anatomy (foundation steps and pipeline stages alike):** `CONTEXT.md` (the stage contract — its Inputs naming the prior stage's `output/`, its Process, its Outputs), `skill.md` (the procedure), `references/` (stage-local reference, where needed), and `output/` (the hand-off + human edit surface; per-`[doc-slug]` subfolder in the pipeline). The table below details what each unit holds.

| Component | Holds | Engine/config | Notes |
|---|---|---|---|
| `CLAUDE.md` | Map, routing table (task → files), naming | engine | Routing covers: foundation run, a document run (01–05), capture-learnings, cohesion-check, archive. |
| `identity.md` | Owner-as-expert role card; **shapes-not-authors** stance | engine | Owner *identity* read from `_config/owner.md`; the stance is engine. |
| `governance.md` | Approval tiers (ref `_config/approval-tiers.md`); suite-cohesion *rule*; lifecycle metadata mandate (owner, review cycle, materiality trigger on every doc) | engine | Specific tiers are config; the obligation/structure is engine. |
| `decisions-register.md` | Living record of (a) engine/architecture decisions and (b) **captured policy-position & priority decisions** (PRD's "mental decisions"). Engine **consults** at 01, 03, F4 | data (living) | GAP 2. Serves the north star ("we've already established them"). Distinct from `roadmap.md` (what to build when). |
| `roadmap.md` | What will be built, priority order, how the suite hangs together; drives sequencing + cohesion choices | data (living) | Owner-ruled working artifact (gate 1). Distinct from KM register (lifecycle) and decisions-register (rulings). |
| `memory/writing-stance.md` | Plain / Einstein / intent-led drafting stance | engine | Voice-print *split*: stance here; style profile in `_config/voice-print.md`. |
| `memory/dont-boil-the-ocean.md` | Sequence, don't attempt the whole suite at once | engine | Governs *content* pace, not the ICM build. |
| `memory/suite-cohesion-stance.md` | Fix contradictions even when annoying; never shrug | engine | The *stance* behind the cohesion *rule*. |
| `foundation/f1-analyse-landscape/` | Stage: analyse handbook + adjacent policies → gap analysis (`output/`) → seeds roadmap + register | engine | Reads `foundation/input/`. Re-run when landscape shifts. |
| `foundation/f2-build-voiceprint/` | Stage: analyse prior-role suite → voice-print + worked-examples (`output/`, reviewed → installed to `_config`) | engine | One-off pass producing config to drop in (owner's gate-1 ruling). Refreshed if voice evolves. |
| `foundation/f3-define-template/` | Stage: design house template fresh (`output/` → `_config/house-template.md`), pinning the named sections every document carries: **intent · scope · rules · escalation · edge cases · approvers · owner · review cycle · materiality trigger** | engine | One-off pass; versioned thereafter. |
| `foundation/f4-seed-roadmap/` | Stage: populate roadmap + seed standard-sections + **capture mental decisions → decisions-register**; **work through the industry-standard baselines here**, pinning anything to treat as a floor/input in roadmap development | engine | Counters "boil the ocean" by sequencing. Industry baselines are a starting floor, fixed per-subject at foundation rather than as a standing config artifact. |
| `document-pipeline/01_select-and-brief/` | Stage: take next roadmap item (or emergent need); owner sets brief + names applicable standard sections; engine surfaces roadmap state, applicable sections, **consults decisions-register**. Reads `input/`; writes `output/[slug]/brief.md` | engine | Owner's run-specific drop folder lives here (`input/`). |
| `document-pipeline/02_draft-to-standard/` | Stage: voiced draft to house template + voice-print, from brief + applicable sections, grounded in source, industry basics (not overbaked), reg floor. Reads 01's output; writes `draft.md` | engine | Engine drafts; owner shapes. |
| `document-pipeline/03_refine-and-checks/` | Stage: owner refines/hand-polishes (refine skill); **3a — tiered cohesion-check** (index → per-doc summary → mirror; go-back-and-fix on conflict); **3b — regulatory-floor clearance check** (verify the doc *clears* the NZ reg floor, §2 "must clear"). 3a and 3b are distinct skills/contexts so they're not conflated, but run in the one refine pass. Reads 02's output; writes `approval-ready.md` only once **both** checks clear | engine | Feeds capture-learnings. |
| `document-pipeline/04_approve-per-tier/` | Stage: route approval — Policy → CEO sign-off; Standards/Guidelines → owner issues, CEO & SLT consulted. Writes approval record → KM register | engine | Tiers **proposed** (config), owner-confirms before they harden. |
| `document-pipeline/05_register-store-maintain/` | Stage: export approved doc → company infra; update KM register + roadmap; **promote-to-standard gate** (fold new recurring sections in on owner's explicit call); update `cohesion-index/` + `mirror/`; make forced cross-suite amendments; **archive the run document-major**; clear stage outputs for the next run | engine | The maintenance hub. Keeps cohesion-index + mirror current *by construction*. |
| `document-pipeline/capture-learnings/` | Stage (GAP 1): read delta between 02's `draft.md` and 03's `approval-ready.md`; **propose** updates to `_config/voice-print.md` + `memory/`; owner ratifies | engine | The learning loop — maintenance counterpart to F2. Gated: never silent. |
| `reference/materiality-hierarchy.md` | Policy / Standard / Guideline definitions + when each applies (no Framework tier) | engine | "No Framework tier" is a config-scoped call. |
| `tools/index-standard-sections.*` | Deterministic: maintain standard-sections index; detect drift/duplication | engine | Local script (ICM canon). **Mechanical only.** |
| `tools/build-cohesion-index.*` | Deterministic: regen `cohesion-index/index.md`; flag drift | engine | **Mechanical only.** |
| `tools/archive-run.*` | Deterministic: gather a completed run's stage outputs into `archive/[slug]/` document-major | engine | **Mechanical only.** |
| `_config/*` | house-template, voice-print ★, worked-examples, standard-sections ★ (+ index), regulatory-floor, approval-tiers, owner | config | Deployment-bound; the swappable layer. |
| `connections/document-store.md` | Company infra (on-prem / SharePoint) — export target for approved docs | config | Permissions proposed-only until ratified. |
| `connections/km-register.md` | Notion (business tier) — status, effective date, owner, version, next-review, **approval record** | config | Owner-ruled; **conditional on the formal-register safeguards being put in place** (see ADR). |
| `cohesion-index/` | `index.md` (searchable) + `[slug].md` (per-doc summaries) — Tiers 1–2 of the cohesion check | data (living) | Generated at Step 5. |
| `mirror/` | Local full-text copy of approved suite — Tier 3, read only on a flagged concern | data (living) | Hermetic fallback. Kept current at Step 5. |
| `archive/[slug]/` | Completed run, document-major: the full brief → registered history | data | Written at close (Step 5) before the pipeline runs again. |

## 3 · The artifact breakdown — resolved

| Element (from PRD §6) | Artifact type | Home | Confirmed? |
|---|---|---|---|
| House template | reference (config) | `_config/house-template.md` | ✅ |
| Voice print — *writing stance* | memory | `memory/writing-stance.md` | ✅ (R1 split) |
| Voice print — *style profile* | reference (config) ★ | `_config/voice-print.md` | ✅ (R1 split) |
| Worked-examples library | reference (config) | `_config/worked-examples.md` | ✅ |
| Standard-sections library | reference (config), living ★ | `_config/standard-sections/` | ✅ (R2: gate + tools) |
| Owner's per-document brief | working artifact | `document-pipeline/01_.../output/[slug]/brief.md` | ✅ |
| Materiality hierarchy | reference (config) | `reference/materiality-hierarchy.md` | ✅ |
| NZ regulatory floor | reference (config) + **enforcement gate** | `_config/regulatory-floor.md`; **"must clear" enforced at Step 3b** | ✅ |
| Analyse landscape (F1) | skill (stage folder) | `foundation/f1-analyse-landscape/` | ✅ |
| Extract voice-print + examples (F2) | skill (stage folder) | `foundation/f2-build-voiceprint/` | ✅ |
| Define house template (F3) | skill (one-off pass) | `foundation/f3-define-template/` | ✅ |
| Seed/maintain roadmap (F4) | skill (stage folder) | `foundation/f4-seed-roadmap/` | ✅ |
| Draft to house standard (Step 2) | skill (stage folder) | `document-pipeline/02_draft-to-standard/` | ✅ |
| Refine / hand-polish / cohesion + reg-clearance (Step 3) | skill (stage folder) | `document-pipeline/03_refine-and-checks/` (3a cohesion · 3b clearance) | ✅ |
| Build roadmap / cohesion map | working artifact | `roadmap.md` | ✅ (gate 1) |
| Approval tiers | governance | `governance.md` + `_config/approval-tiers.md` | ✅ proposed |
| Suite-cohesion obligation — *rule* | governance | `governance.md` | ✅ (R3 split) |
| Suite-cohesion obligation — *stance* | memory | `memory/suite-cohesion-stance.md` | ✅ (R3 split) |
| Lifecycle metadata (owner/review/materiality trigger) | governance | `governance.md` (captured/stored); **trigger *firing* deferred to the review engine — §7** | ✅ |
| Plain-language / Einstein / intent-led stance | memory | `memory/writing-stance.md` | ✅ |
| "Don't boil the ocean" | memory | `memory/dont-boil-the-ocean.md` | ✅ |
| Owner identity / expert / shapes-not-authors | role card | `identity.md` (+ `_config/owner.md`) | ✅ |
| Document store (company infra) | connection spec | `connections/document-store.md` | ✅ |
| KM register (lifecycle + approval record) | connection spec | `connections/km-register.md` (Notion — explicit owner call at architecture, closing PRD §7's open KM-tooling question) | ✅ (R4) |
| **Cohesion-check mechanism** | data (tiered) | `cohesion-index/` → `mirror/` | ✅ (R3) — net-new |
| **Deterministic helpers** | local script | `tools/` | ✅ (R2) — net-new |
| **Learning loop** | skill (stage folder) | `document-pipeline/capture-learnings/` | ✅ (GAP 1) — net-new |
| **Internal decisions-register** | working artifact (living) | `decisions-register.md` | ✅ (GAP 2) — net-new |
| **Run archive (document-major)** | data | `archive/[slug]/` | ✅ — net-new |

## 4 · Placement & fit

**Standalone — follows the generic ICM baseline**, with deliberate, owner-ratified choices (all within ICM canon):

- **Canonical stage folders + output→input chaining.** Each foundation step and pipeline stage is a self-contained folder (`CONTEXT.md` + `skill.md` + `references/` + `output/`); stage N's `output/` is stage N+1's input. The glass-box audit trail is the structure, not a flattened set of skill files.
- **Stage-major live, document-major archive.** Live audit unit is the stage (canonical); a completed run is archived document-major (`archive/[slug]/`) before the pipeline runs again, so each policy's full history is co-located for the durable record.
- **`tools/` (deterministic local scripts).** Within ICM canon (local scripts are first-class); **mechanical only — no branching logic** (branching stays human).
- **Tiered cohesion-check (`cohesion-index/` → `mirror/`).** Scoped-context discipline: never load the full suite. Tier 1 `index.md` → Tier 2 per-doc summary → Tier 3 mirror full-text, escalating only on a flagged concern.
- **Hermetic mirror, not a live connector.** Honours the scope ruling. Mirror + cohesion-index update inside Step 5, so they can't drift from the stored documents.
- **Three living registers, deliberately separate** — `roadmap.md` (what to build when), `decisions-register.md` (what we decided and why), external `km-register` (per-document lifecycle).

**Governance conflicts:** none with an external system (standalone). One internal discipline: **approval tiers are proposed, not hardened** — encode as proposed-pending-confirmation until the owner ratifies.

## 5 · Build plan — staged and gated

Each stage is a reviewable unit; the owner gates each. Ordered by dependency.

1. **Engine skeleton** — `CLAUDE.md`, `identity.md`, `CONTEXT.md`, `governance.md` (tiers as *proposed*), `reference/materiality-hierarchy.md`, the three `memory/` files. *Gate: the spine reads right.*
2. **The registers** — `decisions-register.md` + `roadmap.md` scaffolds. *Gate: the two are clearly distinct.*
3. **Foundation** — `foundation/` with F1–F4 as stage folders + `foundation/input/`. *Gate: each foundation pass is runnable cold and its output installs to the right home.*
4. **Document pipeline** — `document-pipeline/` stages 01–05 + `capture-learnings/`, each a folder with contract/skill/output, the chaining map in the pipeline `CONTEXT.md`. *Gate: a document run flows 01→05 with each `output/` feeding the next.*
5. **Cohesion + tools + archive** — `cohesion-index/`, `mirror/`, `archive/`, and `tools/` (index, cohesion, archive — mechanical). *Gate: tiered cohesion-check works; tools stay mechanical; a completed run archives document-major.*
6. **Config + connections** — `_config/` and `connections/`. *Gate: deployment specifics live only here; engine clean.*
7. **Run the foundation for real** — F1–F4 on the actual handbook + prior-role suite to populate `_config/` and seed the roadmap. *Gate: the factory is configured; first document can start.*

*The build is the next conversation, not this one.*

## 6 · End-of-build audit

Run by a cold subagent when the build is done:

- **Fidelity / cohesion** — builds what the PRD specced (foundation + full per-document engine); hangs together; mission served (quoted intact, not drifted).
- **Architecture** — engine/config split clean (no deployment leak); three registers genuinely distinct; placements match §3; no duplication.
- **Mechanism** — skills and gates work; a document flows 01→05 with `output/` chaining; the **Step 3b regulatory-clearance gate** and the **3a cohesion-check** both fire before approval-ready; promote-to-standard gate and learning-loop gate fire (nothing silent); a completed run archives document-major.
- **Build-specific:**
  - **Stage-folder integrity** — every foundation step and pipeline stage is a folder with contract + skill + `output/`; no stage flattened to a bare file; the chain is explicit in each `CONTEXT.md`.
  - **Hermetic seam** — no skill reads an external system live; the only external touches are *export* (document-store) and *register-write* (km-register), at Step 4/5.
  - **Portability** — swapping `_config/voice-print.md` + `_config/standard-sections/` changes the house voice without touching the engine.
  - **Tools stay mechanical** — no `tools/` script makes a branching decision.
  - **Cohesion currency** — `cohesion-index/` and `mirror/` cannot be staler than the last Step 5.

## 7 · Open questions & risks carried forward

- **Open (PRD §7):** emergent-vs-roadmap arbitration — what governs re-prioritising when an emergent need jumps the queue. Carried; design at build or first-real-use.
- **Open (PRD §7):** KM-register MVP — the minimum fields that count as "ownership, versioning, review-due and approval durably tracked." **Tool resolved to Notion by explicit owner call at architecture** (closing the PRD's open KM-tooling question — see ADR); this open item is now only the MVP field set, TBD when `connections/km-register.md` is built.
- **Deferred to future scope — the review engine.** Lifecycle metadata (review cycle + materiality trigger) is *captured and stored* in this build; the **firing behaviour is a recognised future-scope component**: a *review engine*, triggered on a review-cycle date rolling around **or** a materiality trigger, that re-reviews the document's content, updates versioning, makes required updates, and re-classifies/re-routes the tier where materiality has shifted. Explicitly deferred and recorded (here + an ADR), not silently dropped — resolves the audit's GAP-A as a conscious deferral.
- **Risk accepted (owner, R4):** the approval record lives in Notion rather than company-governed infra. Accepted on the owner's reasoning (business-tier, org infrastructure, owner owns the call) — **conditional on the formal-register safeguards being put in place**.
- **Risk flagged (R2):** a write-back-on-use standard-sections library can bloat/drift — mitigated by the promote-to-standard gate (owner's explicit call) + deterministic index/drift tools. Mitigation is load-bearing; skipping the gate returns the risk.
- **Assumption (PRD §7):** approval tiers — **proposed, owner confirms before it hardens** (~98% confident; will not let it harden unconfirmed).
- **Assumption:** owner (head of D&A) is the default document owner unless stated otherwise.
- **Aside — the governance bar.** PRD §2 names a "board / CEO bar"; the operative approval gate is **CEO sign-off** (§5 Step 4). "Board" was the owner's conservative framing (the residual ~2%), not an operative gate — noted so the build doesn't encode a board-approval step that isn't there.

## 8 · Decisions

The decisions that shaped this architecture are proposed — not ratified here — in the companion: `output/adr-proposals-policy-standards-authoring.md`. The owner ratifies them (into the new workspace's own `decisions-register.md` once built, and/or her build-decisions log).

---

*This build spec is the architecture; the ADR proposals are the decisions behind it; the finalised PRD is the source. The three share the `policy-standards-authoring` slug and travel together to the build.*
