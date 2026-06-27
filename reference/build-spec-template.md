---
file-type: template
workspace: architecture-thinking-partner
last-updated: 2026-06-27
status: active
referenced-by: [gate2-architecture]
---

# Build-Spec Template

The shape of the artifact gate 2 produces: `output/build-spec-[slug].md` — the architecture that turns a finalised PRD into something a build conversation can pick up cold. It says *what to build, how it's structured, where it lands, and how to build it* — not the build itself (this stage specs; it doesn't instantiate — see `rules.md`).

Fill it in conversation and **confirm it with the person** before it stands; the build spec ships at `status: draft` and is ratified by the person, like everything else this stage produces. The section order below is the finished artifact's shape — gather and reorganise into it; don't march the person through it.

The produced build spec opens with this frontmatter:

```
---
file-type: build-spec
slug: [slug]                          # carries over from the source PRD — ties the suite's outputs together
subject: [short name of the build]
source-prd: output/prd-[slug].md      # the finalised PRD this was built from (status: final)
scope: standalone | wider
target-system: [name]                 # the existing system, if wider; omit if standalone
reference-architecture: generic-icm-baseline | [target-system config]
created: [YYYY-MM-DD]
status: draft                         # draft at gate 2 → promoted to 'ready' at coverage-audit-and-close (audited + ratified)
companion-adr: output/adr-proposals-[slug].md
---
```

---

## 0 · Orientation — what this builds, and the mission it serves

One paragraph a cold reader starts from: what the workspace is (the ICM-shaped job it does), and — **carried from the PRD's mission, not lost** — the north star it points at. State the scope (standalone or wider) and, in a line, where it lands. The *why* leads, because the architecture serves it; an architecture that's drifted from the mission is the failure mode in `identity.md`.

> **Never rewrite the mission.** The mission is the person's own words (the upstream stage held it as a quoted voice-exception). **Copy it across and quote it exactly** — verbatim from the PRD's mission section. Don't reword it, summarise it, neutralise it into spec, or "improve" it. The architecture serves the mission; it has no licence to author or alter it. The same holds for any other quoted-voice content the PRD carries.

- **What it is:** [the workspace and the recurring, human-in-the-loop job it does]
- **The mission it serves:** [the north star — **quoted exactly from the PRD, verbatim**; never paraphrased or neutralised]
- **Scope & placement:** [standalone · or within `[target-system]`, landing at `[location]`]

## 1 · The architecture — structure

The annotated folder tree — the ICM structure the build creates. One line per file/folder on what it is. Mark the **engine vs config split**: the reusable engine (identity / rules / skills / reference) and the deployment-specific config, so the build keeps them separate.

```
[workspace-name]/
├── CLAUDE.md          ← [entry contract]
├── identity.md        ← [role card]
├── ...                ← [one line each]
├── skills/
│   └── ...
├── reference/
├── _config/           ← [deployment-specific — what changes per deployment]
└── output/
```

*Note which pieces are the reusable engine and which are deployment-bound `_config` — the build must not let deployment specifics bleed into the engine. The flat `skills/` shown above is the simple/parallel shape; for a **sequential pipeline**, skills become numbered stage folders — see the pipeline callout below.*

> **Pipeline builds — stages are folders, not files.** If the build is a sequential pipeline (one step's output feeds the next), draw the canonical **numbered stage-folder** pattern, not a flat `skills/` list — echoing the baseline (`_config/generic-icm-baseline.md` § 5). Each stage is its own folder carrying its contract, reference, and output:
> ```
> workspace/
> ├── CLAUDE.md                 ← L0: map, routing table, naming
> ├── CONTEXT.md                ← L1: task routing + shared resources
> ├── stages/
> │   ├── 01_[job]/
> │   │   ├── CONTEXT.md         ← L2: stage contract (Inputs / Process / Outputs)
> │   │   ├── references/        ← L3: stage-local reference
> │   │   └── output/            ← L4: hand-off point + human edit surface
> │   ├── 02_[job]/ …
> │   └── 03_[job]/ …
> ├── _config/                  ← deployment-specific config
> ├── shared/                   ← cross-stage shared resources
> └── setup/
>     └── questionnaire.md      ← one-time factory configuration
> ```
> **`output/` chaining:** stage N's `output/` is stage N+1's input, with a human edit/review gate at every boundary. **Preserve the per-stage contract and the output-chaining** — flattening stages into single `.md` files loses the glass-box audit trail that *is* the pipeline. (Parallel modes rather than a sequence → **rooms**, not stages; see baseline § 5.) **Wider build?** Draw this stage-folder *shape* as a delta per the standalone-vs-wider note below — not a from-scratch redraw of the whole system.

> **Standalone vs wider — draw the right tree.** **Standalone:** draw the full new structure as above. **Wider (into an existing system):** don't redraw the whole system as if from scratch — show the **delta in context**. Either present **current-state → future-state**, or annotate a single tree marking each node **[new]**, **[modified]**, or **[existing]** (untouched files shown only where they give the new parts their context). The reader needs to see exactly what's added, what's changed, and where it slots in — grounded in the system's actual structure (`where-does-this-belong.md`), not a generic layout.

## 2 · Build detail — per component

For each file or component the build creates: what it holds, the key content, and any decision that shapes it. Enough that a build conversation writes the file without re-deriving it. Flag what's **reused or extended from the target system** vs **newly built**.

### [file / component]
- **What it holds:** [content and purpose]
- **Engine or config:** [reusable engine · deployment-specific]
- **Reuse / new:** [extends `[existing system artifact]` · new]
- **Key decisions / notes:** [anything load-bearing the build needs]

*Repeat per component.*

> **Few components → blocks; many → a table.** The per-component block above is for a handful of components that each need detail. When the build has **many** components, switch to a markdown table to avoid bloat — `Component · Holds · Engine/config · Reuse/new · Notes` — keeping the same fields in one scannable grid rather than dozens of repeated blocks.

## 3 · The artifact breakdown — resolved

The PRD's §6 breakdown, **resolved** — this is what gate 2 finishes that the PRD left open. Each element classified through `where-does-this-belong.md` to a type *and* a home, confirmed with the person. No flagged-for-later rows (that was the upstream stage); every row is recommended and confirmed.

| Element (from the PRD) | Artifact type | Home (where it lands) | Reuse / new | Confirmed? |
|---|---|---|---|---|
| [element] | [skill / memory / reference / governance / role card / context / connection / working artifact] | [folder / file, in the system's idiom] | [reuse `[X]` · new] | ✅ / open |

*Any element the person placed against the recommendation: note their call and the reasoning (run through `challenger-calibration.md`).*

## 4 · Placement & fit

**Wider:** where the build lands in the target system and how it fits — confirmed with the person.
- **Lands at:** [folder / location, in the system's conventions]
- **Inherits:** [the governance, conventions, and patterns it sits under]
- **Reuses:** [what it shares with or extends in the existing system, rather than duplicating]
- **Governance conflicts:** [any rule the build would cross, surfaced upfront, and how it resolved — never designed around silently; see `rules.md`]

**Standalone:** the build follows the generic ICM baseline shape (`_config/generic-icm-baseline.md`); note any deviation and why.

## 5 · Build plan — staged and gated

The execution sequence: the stages to build it, each **gated by the person** — the same stage → show → gate rhythm these builds run on. Order by dependency; keep each stage a reviewable unit.

1. **[Stage]** — [what it builds]
2. **[Stage]** — [...]
3. ...

*The person gates each stage. The build is the next conversation, not this one — this spec is the thing it picks up.*

## 6 · End-of-build audit

The fresh-context audit to run when the build is done — the load-bearing properties this specific build must hold, checked by a cold subagent. Tailor the dimensions to the build; the three standing ones:

- **Fidelity / cohesion** — does it build what the PRD specced, and does it hang together; is the mission still served?
- **Architecture** — sound structure, engine/config separation clean, no duplication, placed right in the system?
- **Mechanism** — do the skills and gates actually work as written?

Add any build-specific checks (e.g. a terminology rule, an accessibility non-negotiable, a seam that must stay clean).

## 7 · Open questions & risks carried forward

Named, not papered over — where the build conversation picks up.

- **Open (from gate 1):** [a gap finalisation marked open rather than resolved]
- **Risk accepted (from gate 2):** [a risk surfaced and the person chose to carry — recorded so the build knows it was a conscious call, not an oversight]
- **Assumption:** [something taken as given that the build should check]

## 8 · Decisions

The decisions worth recording are proposed — not ratified here — in the companion: `output/adr-proposals-[slug].md`. The person ratifies them into the target system's decisions register (see `adr-proposal-template.md`). Point to it; don't restate the entries.

---

*This build spec is the architecture; the ADR proposals are the decisions behind it; the finalised PRD is the source. The three share the `[slug]` and travel together to the build.*
