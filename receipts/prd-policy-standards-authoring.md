---
file-type: prd
slug: policy-standards-authoring
subject: Writing & maintaining the FMCG company's tech/data policies & standards suite
build-target: independent
target-workspace:
created: 2026-06-27
status: final
companion: output/build-notes-policy-standards-authoring.md
sanitisation: Company referred to as "an FMCG company in New Zealand" — not by name. See friction/sanitisation log.
finalised: 2026-06-27 (gate 1, Architecture Thinking Partner — owner-confirmed)
---

# PRD — Tech & Data Policy/Standards Authoring Suite

## Mission / North Star — why this is worth defending

*Drawn out in the person's own words. This section alone carries her voice; everything from § 1 down is neutral spec.*

- **True outcome — the north star:** A fast-growing FMCG company can no longer responsibly hold its boundaries through personal relationships alone. Writing the tech/data rules down — simply, clearly — is how the org manages real risk *and* stays upfront with its people. In her words:
  > "Setting expectations and boundaries, simply and effectively, is a form of care. It shouldn't condescend to them or treat them as stupid."

- **Why it matters:**
  > "What used to be okay when it was 6 people and a 'we just make it happen' mentality isn't what works when you're big enough to have JBPs with all the supermarkets in NZ. Having that change be unwritten is unclear, uncollaborative and unkind as well as irresponsible from a governance perspective."

  The org is mid-transformation (digital/technical/data); written, referenceable anchors also give long-tenured staff "a simple primer on how expectations are changing."

- **What the status quo costs — beyond hours:** Decisions made on the fly. *"When questions come up,"* the org is *"asking 'what should we do?' and invent[ing] it"* rather than knowing where the lines already are. With partners, it's *"a scramble"* instead of having something to hand.

- **Convictions — always / refuse:**
  - **Always** sit in a clear hierarchy matched to materiality — Policy → Standards → Guidelines (a Framework tier exists in principle but isn't needed for this data/tech suite).
  - **Always** be in natural language and understandable — *"minimising jargon and explicitly explaining or glossing it when it is required."*
  - **Always** follow the Einstein principle — *"as simple as it can be and no simpler"*; nothing ornate.
  - **Always** state intent, *"so that people can follow the principle of it rather than dictating every case and [being] used by the letter."*
  - **Always** make escalation, edge cases, approvers and owners explicit; and **always** carry an owner, a review cycle, and a materiality review trigger.
  - **Refuses** to let the suite contradict itself — *"each one that is built out shouldn't undermine or contradict the others and if they require us to go back and make changes, we should do that rather than just pretending it's fine because it's annoying."* (The refuse-the-slower-path line.)

- **The one thing that has to be true — and how you'd know:**
  > "When questions come up, we're not asking 'what should we do?' and invent it — we know where the lines are and how it works because we've already established them. And when we work with new partners, we have something to hand when requested rather than a scramble."

> **Voice exception — this section only.** Everything below is neutral spec.

---

## 1 · Problem statement

- **Outcome:** A coherent, maintained suite of tech & data policies, standards and guidelines that establishes where the lines are — so the org acts from settled position rather than improvising, and can hand partners a credible document set on request. Written as care: plain, intent-led, never condescending.
  - *Success criteria (built):* (a) When a tech/data question arises, the answer is *looked up*, not invented. (b) A partner request is met by handing over an existing document, not a scramble. (c) The suite holds together — a new document doesn't silently contradict an existing one; conflicts trigger a go-back-and-fix, not a shrug.

- **Friction reduced / improvement delivered:** The data/tech policy space is largely a **void** — foundational pieces aren't in place, so positions get "shot from the hip" as questions arise. The org has scaled past the point where unwritten, relationship-held boundaries are responsible, but the written layer hasn't caught up.
  - *Where it hurts most (build priority):* The **void itself** — "a lot of foundational pieces aren't in place" — is the biggest issue, and it carries a real risk: the owner's own *"want to boil the ocean and do it all at once."* So the build's first job is to make the foundation + a prioritised roadmap exist, so the work is sequenced rather than attempted all at once. The two highest-pain individual documents to tackle first: **appropriate device usage** (where shoot-from-the-hip answers happen now) and **AI use** ("the wild west — we need a clear position given what is happening with the tech").

## 2 · Constraints / non-negotiables

Workflow-wide rules over every document the suite produces. (Several are stated once as convictions in the mission; carried here as neutral spec.)

- **Materiality hierarchy** — every document is classified and structured as Policy, Standard, or Guideline by materiality. Top-level for this suite is a *policy* (no framework tier required). Standards sit as detail under a policy; guidelines are non-binding "how to apply."
- **Plain language** — natural language, minimal jargon, jargon glossed where unavoidable; Einstein-simple, never ornate.
- **Intent-led** — each document states what it's trying to achieve so it can be followed in principle, not gamed by the letter.
- **Explicit machinery** — escalation paths, edge cases, named approvers, and a named owner appear in every document.
- **Lifecycle metadata** — every document carries an owner (defaults to the head of data & analytics), a review cycle, and a materiality review trigger.
- **Suite cohesion** — no document may contradict another; an emergent conflict obliges a go-back-and-amend across the suite, not a workaround.
- **NZ regulatory floor** — every document must clear the relevant NZ regulatory baseline (e.g. Privacy Act 2020) for its subject.
- **Governance bar** — policies must satisfy the board / CEO bar; the owner is the hired domain expert and sets the quality bar the documents must meet.

## 3 · Outputs needed

*Three distinct homes: the **documents themselves** live in **company infrastructure**; the **build roadmap / cohesion map** is an **ICM working artifact**; the **KM register** that tracks each live document is a **separate external KM layer** (see § 4 / § 7 for the tooling decision).*

- **A finished, approved document** (policy / standard / guideline) → **company infrastructure: on-prem drive or SharePoint, as appropriate per document** — conforms to the house template + voice print + the owner's applicable standard sections; carries intent, scope, rules, escalation, edge cases, approvers, owner, review cycle, materiality trigger. *This is the recurring unit.*
- **The house template** → suite foundation — the fresh-designed format/structure each document type conforms to. (Built early, then reused every run.)
- **The voice print** → suite foundation — an extracted profile of *how the owner writes* policies/standards/guidelines, plus a library of real worked examples of edge-case / escalation / approval handling, mapped to this org. (Built early from her prior-role suite, then reused.)
- **The standard-sections library** → suite foundation (living) — the owner's own set of standard sections that recur across documents, used as a starting point alongside industry-standard content. Seeded in part during the roadmap foundation and **built out as documents are written**. Distinct from the template (structure) and voice print (style): this is *recurring content*.
- **The build roadmap / cohesion map** → **ICM working artifact (lives in the ICM)** — a roadmap-up-front of what will be built, in what priority order, and how the pieces hang together; the living sequencing-and-cohesion artifact the owner works from; drives cohesion choices. *Distinct from the KM register below — this is the owner's build/sequencing view, held in the ICM.*
- **The KM register (per-policy lifecycle)** → **KM layer: Notion preferred, or a SharePoint list** — the durable, org-visible index of each live document's approval status, effective date, owner, version, and next review date; tracking that must outlive the ICM session. *Tooling open — see § 7.*
- **Approval record** (should-have, MVP, not a must-have) → **KM layer (part of the KM register above)** — capture of who approved each document and when; deliberately *not* housed solely in the owner's ICM system, because the org needs durable institutional memory of approvals.

## 4 · Inputs available

- **Company handbook + adjacent existing policies** — internal (e.g. appropriate use of tech, securing devices) — analysed up front to find what's covered vs the void, and what to compose.
- **Transformation plans + decisions already made** — some in email, some only in the owner's head — source material for positions.
- **The owner's prior-role data policy suite** — written by her at a previous job — adapted, but primarily **analysed** to (a) build the voice print and (b) extract worked edge-case/escalation/approval examples to map across.
- **Industry-standard baselines** — a starting floor for content ("we don't need to overbake them").
- **The owner's content view + standard-sections library** — for each document, the owner's own view of what it needs to contain; plus her set of **standard sections that go in everything**, applied as a starting point alongside the industry-standard baseline. The library **builds out as documents are written** (grows with the suite); some of it is **known/decided up front in the roadmap foundation**. An explicit input the owner supplies as each document is picked up — not something the engine infers for her.
- **NZ regulatory floor** — Privacy Act 2020 and other relevant baselines — the legal minimum each document must clear.
- **The owner's redesign authority** — already granted; she can define the house template fresh.

**Unwritten knowledge the build needs:**

- **Decisions made "mentally"** — positions and priority-order judgments the owner holds but hasn't written down; the build must surface and capture these as it seeds the roadmap.
- **The owner's expert sense of "what you'd expect to find based on industry standards"** — decided as the roadmap and voice prints are seeded, not pre-listed.

## 5 · Steps

The suite runs in two layers: a **foundation layer** (once, up front — part of this build) and a **repeating unit** (per document). Described as the owner wants it to run.

### Foundation layer (once)

#### Step F1 — Analyse the existing landscape
- **What happens:** Analyse the company handbook + adjacent existing policies to map what's already covered, where the void is, and what should be composed.
- **Produces:** a gap analysis feeding the roadmap → suite foundation.
- **Who acts:** the owner, with ICM assistance (analysis + synthesis).
- **Trigger / frequency:** once, at suite stand-up (re-run when the landscape materially shifts).

#### Step F2 — Build the voice print + worked-examples library
- **What happens:** Analyse the owner's prior-role suite to extract her writing voice for each document type, plus real worked examples of edge-case / escalation / approval handling, mapped to this org.
- **Produces:** the voice print + worked-examples library → suite foundation.
- **Who acts:** the owner shaping; ICM extracting/proposing.
- **Trigger / frequency:** once (refreshed if the house voice evolves).

#### Step F3 — Define the house template
- **What happens:** Design the document template(s) fresh — the structure every policy/standard/guideline conforms to (intent, scope, rules, escalation, edge cases, approvers, owner, review cycle, materiality trigger).
- **Produces:** the house template → suite foundation.
- **Who acts:** the owner (redesign authority granted), with ICM drafting.
- **Trigger / frequency:** once (versioned thereafter).

#### Step F4 — Seed the roadmap / register
- **What happens:** Populate the suite register with what will be built and in what priority order — making deliberate choices up front to support end-state cohesion, including surfacing the owner's "mental" decisions and priorities. Where the owner already knows what a given document needs, or which standard sections it should carry, capture those decisions here so they seed the standard-sections library up front. Explicitly counters the "boil the ocean" risk by sequencing.
- **Produces:** the suite register / roadmap (living) → KM layer; initial standard-sections / content decisions → standard-sections library.
- **Who acts:** the owner deciding; ICM structuring and challenging.
- **Trigger / frequency:** once to seed; revised continuously as things emerge.

### Repeating unit (per document)

#### Step 1 — Select the next document and set the owner's brief
- **What happens:** Take the next item off the roadmap by priority — or slot in an emergent need (partner request, transformation decision, regulatory prompt). The owner sets her brief for it: what *she* wants in this document, and which of her **standard sections** apply as the starting point alongside the industry-standard baseline.
- **Produces:** a scoped document brief (owner's content view + applicable standard sections) → feeds Step 2.
- **Who acts:** the owner sets the brief; ICM surfaces roadmap state, applicable standard sections, and flags cohesion implications.
- **Trigger / frequency:** roadmap priority order, or emergent need.

#### Step 2 — Draft to house standard
- **What happens:** ICM produces a voiced draft to the house template + voice print, starting from the owner's applicable standard sections and her content brief, grounded in source material, industry-standard basics (not overbaked), and the NZ regulatory floor for the subject.
- **Produces:** a draft document (interim — feeds Step 3).
- **Who acts:** ICM creates the voiced draft; the owner shapes (she shapes, it does not author).
- **Trigger / frequency:** on selection from Step 1.

#### Step 3 — Refine, hand-polish, and check cohesion
- **What happens:** The owner reviews, refines (with or without ICM assistance), and hand-polishes to her bar; checks the draft against the rest of the suite for contradictions and triggers a go-back-and-fix if one surfaces.
- **Produces:** an approval-ready document (interim — feeds Step 4).
- **Who acts:** the owner; ICM assists on request and flags cohesion conflicts against the register.
- **Trigger / frequency:** on draft ready.

#### Step 4 — Approve per tier
- **What happens:** Route for approval by document type — **Policy → CEO sign-off**; **Standards & Guidelines → issued by the owner under the approved policy, with CEO & SLT consulted (not a formal approval gate)**.
- **Produces:** an approved document → company infrastructure (on-prem / SharePoint); an approval record → KM layer (should-have).
- **Who acts:** the owner; CEO (policies); CEO & SLT consulted (standards/guidelines).
- **Trigger / frequency:** on approval-ready document.

#### Step 5 — Register, store, and maintain cohesion
- **What happens:** Store the approved document in company infrastructure; update the suite register in the KM layer (status, owner, version, next review date); where this document forced changes elsewhere, make those amendments rather than deferring them. Fold any new recurring section back into the standard-sections library.
- **Produces:** stored document (company infra); updated register (KM layer); grown standard-sections library; cohesive suite.
- **Who acts:** the owner; ICM updates the register and tracks review/materiality triggers.
- **Trigger / frequency:** on approval; and on each review-cycle / materiality trigger thereafter.

## 6 · Draft artifact breakdown

**A proposal, not a decision.** Final placement is the architect's call in the build conversation. Uncertain rows flagged.

| Element (from the workflow above) | Proposed artifact type | Notes / open question |
|---|---|---|
| House template (document format/structure) | reference (config) | The fixed shape each document conforms to. |
| Voice print — how the owner writes | reference (config) | **Flag:** reference vs memory — it's a style/voice profile applied as a writing standard; could be a reference the drafting skill consumes, or a memory shaping judgment. Architect to call. |
| Worked-examples library (edge-case/escalation/approval, mapped to org) | reference (config) | Derived from prior-role suite; ground-truth examples. |
| Standard-sections library (owner's recurring sections, grows with the suite) | reference (config) | **Flag:** living/growing content, not fixed — reference that the drafting skill consumes *and* the workflow appends to. Distinct from template (structure) and voice print (style). Architect to confirm it's a reference vs a working artifact given it mutates. |
| Owner's per-document content brief (what she wants in *this* one) | working artifact | Per-run input the owner supplies at Step 1; not inferred by the engine. |
| Materiality hierarchy (Policy/Standard/Guideline definitions + when each applies) | reference (config) | The taxonomy. Applying it to a given document is a skill step. |
| NZ regulatory floor (Privacy Act etc.) | reference (config) | Stable domain facts; per-subject baselines. |
| Analyse existing landscape (F1) | skill | Foundation procedure. |
| Extract voice print + examples (F2) | skill | Foundation procedure. |
| Define house template (F3) | skill | Foundation procedure (one-time). A one-off pass producing a template to drop in is an acceptable outcome — need not be a permanent skill (see § 7). |
| Seed/maintain the roadmap (F4) | skill | Foundation + ongoing; prioritisation procedure. |
| Draft a document to house standard (Step 2) | skill | The core recurring procedure. |
| Refine / hand-polish / cohesion-check (Step 3) | skill | Procedure; cohesion *rule* split out below. |
| Build roadmap / cohesion map (what's built, in what order, how it hangs together) | working artifact (ICM) | **Owner-ruled:** working artifact, held in the ICM. Distinct from the KM register (below) — the external per-policy lifecycle record. |
| Approval tiers (policy→CEO; standards/guidelines→owner issues, CEO/SLT consulted) | governance / rules | The approval authority model. **Proposed, owner to confirm before it hardens** — see § 7. |
| Suite-cohesion obligation (no contradiction; go back and fix) | governance / rules | The behavioural *stance* that drives it may also warrant a memory — **flag** split: rule (must maintain cohesion) → governance; stance (fix it even when annoying) → memory. |
| Owner + review cycle + materiality review trigger (lifecycle) | governance / rules | Mandatory metadata + review obligations. |
| Plain-language / Einstein / intent-led writing stance | memory | Behavioural stance shaping every drafting judgment. |
| "Don't boil the ocean" — sequence, don't do it all at once | memory | Guards against the owner's stated tendency; shapes roadmap judgment. Governs *content* pace, not the ICM build (see § 7). |
| Owner identity / expert judgment / "she shapes, it doesn't author" | role card | The owner is the expert and final bar; ICM augments, never authors. |
| Document store (company infrastructure — on-prem drive / SharePoint) | connection (spec) | Where approved documents *live*. Per-document choice of on-prem vs SharePoint. Distinct from the KM register below. |
| KM register — per-policy lifecycle: approval status, effective date, owner, version, next review (external) | connection (spec) | **Flag:** Notion preferred (could grow org-wide beyond tech/data) **or** a SharePoint list. Distinct from the build roadmap (above). Should-have MVP, not designed now; permissions proposed-only until ratified. |

## 7 · Open questions & assumptions

- **Decided — target system: independent.** The owner has ruled this is its own ICM workspace (`build-target: independent`), and will make the case for that to the architecture stage herself. Not an open question; recorded so the architect knows it's a deliberate ruling to be defended, not a default.
- **Decided — build scope: the whole engine.** Architect both the foundation layer and the recurring per-document loop in this build. "Don't boil the ocean" governs the *content* pace (not 0-to-full-suite-in-a-week), **not** the ICM build. A **one-off pass that produces a template to drop in** (e.g. defining the house template) is an acceptable architecture outcome for something done once — it need not be a permanent skill. *(Owner-ruled at gate 1.)*
- **Decided — documents live in company infrastructure.** Approved policies/standards/guidelines live on the **on-prem drive or SharePoint** (per document, as appropriate) — *not* in the ICM and *not* in the KM tool.
- **Resolved — roadmap ≠ KM register.** The PRD previously placed "suite register / roadmap" in two homes (§ 3 KM layer; § 6 ICM working artifact). Split at gate 1 into three: the **build roadmap / cohesion map** (ICM working artifact), the **approved documents** (company infrastructure), and the **KM register** (external KM layer). See friction-log F4.
- **Open — KM-register tooling (Notion vs SharePoint list):** The KM register (approval status, effective date, owner, version, next review) goes in **Notion or a SharePoint list**. Owner leans **Notion** — already being brought in for the team, and could grow beyond tech/data to provide this KM function org-wide. Carried open into architecture to validate; decide before the KM-dependent outputs ship.
- **Open — KM-layer MVP:** Should-have, deliberately undesigned in this run. What's the minimum that counts as "ownership, versioning, review-due and approval are durably tracked outside the ICM"?
- **Open — emergent-vs-roadmap arbitration:** When an emergent need jumps the queue, what (if anything) governs re-prioritising the roadmap so cohesion choices aren't undone ad hoc?
- **Proposed (owner to confirm before it hardens) — approval tiers:** Policy → CEO sign-off; Standards/Guidelines → owner issues under the approved policy, with CEO & SLT consulted (not a formal gate). Owner is ~98% confident but will not let it harden into governance unconfirmed. Gate 2 records it as **proposed**, not settled; owner ratifies before it becomes a governance rule.
- **Assumption — owner defaults:** The owner (head of data & analytics) is the default owner for every document in this suite unless stated otherwise.
- **Assumption — no framework tier:** This data/tech suite needs no Framework-tier document; top-level is a policy. Revisit only if scope widens beyond data/tech.

---

*Freeform detail and forward-looking build ideas: see `output/build-notes-policy-standards-authoring.md`.*
