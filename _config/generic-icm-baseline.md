---
file-type: reference / baseline
workspace: architecture-thinking-partner
last-updated: 2026-06-26
status: active
referenced-by: [scope-standalone-or-wider, gate2-architecture]
load: at the scope step when standalone; held through gate 2
---

# Generic ICM Baseline — the default reference architecture

The reference architecture this tool designs against **when there's no existing system** (the standalone case). It is the **canonical ICM pattern**, not any one builder's house style — grounded in the ICM / Model Workspace Protocol canon (Jake Van Clief & David McDermott) and the material in the Clief Notes community ([skool.com/cliefnotes](https://www.skool.com/cliefnotes/)). When a *target system* is given instead, that system's own conventions and decisions are ground truth and override this baseline (`where-does-this-belong.md`, `rules.md`); this is the fallback that guarantees there's always a sound architecture to design against.

> **Use it as a design target, not a template to copy.** It describes what a sound ICM workspace *is* — its layers, file types, structure, and mechanisms. Place the PRD's elements into this shape; don't impose section labels, voice, or conventions beyond what the canon prescribes. Where the canon leaves a choice open (see the last section), that latitude is the builder's.

---

## 1 · What ICM is

ICM replaces framework-level orchestration with **file-system structure**. Instead of code coordinating a multi-step AI workflow, a well-organised folder hierarchy holds the context for each step, and one orchestrating agent reads the right files at the right moment. The defining property is the **glass box**: every artifact is plain text a human can open, read, and edit, so the system is interpretable by construction.

A problem is **ICM-shaped** when the workflow is:

- **Sequential** — step 2 follows step 1;
- **Reviewable** — a human should check each step's output; and
- **Repeatable** — the same pipeline runs again with different input.

For this class, ICM gives full orchestration with no framework code, no server, and no developer dependency for day-to-day operation. (Work that is a single deterministic task, a one-off, or needs real-time / high-concurrency / heavy automated branching is *not* ICM-shaped — see the decline guidance in `rules.md`.)

## 2 · Core principles

The five canonical design principles — the baseline holds to all five:

1. **One stage, one job.** Each unit of the workspace handles a single step and writes its output to its own folder.
2. **Plain text as the interface.** Units communicate through markdown and JSON files — no binary formats, no database, no proprietary serialisation. Anything can be inspected or edited in a text editor.
3. **Layered context loading.** A unit loads only the context it needs for its step (prevention, not compression). Within content, *reference material* (stable across runs) is split from *working artifacts* (per-run).
4. **Every output is an edit surface.** Each step's output is a file a human can open, edit, and save before the next step runs.
5. **Configure the factory, not the product.** A workspace is set up once with the builder's preferences, conventions, and structure; thereafter each run produces a new deliverable using the same configuration.

Underneath: separation of concerns, human-in-the-loop review at every boundary, and **scoped context** (target ~2–8k tokens per step — no unit reads everything).

**Single responsibility per file** is the same logic at file granularity: each file does one job. If two files say the same thing, **merge them**; if one file carries two distinct jobs, **split it** — the reasoning that decomposes a multi-step procedure into separate stage skills rather than one sprawling file. Apply it with judgment, not to an extreme: the aim is cohesion, not fragmentation for its own sake.

## 3 · The layer model

A workspace is organised as five context layers. Layers 0–2 are structural (routing and contracts); Layers 3–4 are content.

| Layer | File | Question it answers | Role | Ideal tokens |
|---|---|---|---|---|
| **0** | `CLAUDE.md` | "Where am I?" | Map + routing table; read first, every task | ~800 |
| **1** | workspace `CONTEXT.md` | "Where do I go?" | Task routing + shared resources | ~300 |
| **2** | stage `CONTEXT.md` | "What do I do?" | The stage contract: Inputs / Process / Outputs | 200–500 |
| **3** | reference material | "What rules apply?" | Stable factory config — internalise as constraints | 500–2k |
| **4** | working artifacts | "What am I working with?" | Per-run content — process as input | varies |

*(The simplified deployment names these Map / Rooms / Tools across three layers; the structure is the same. The five-layer model is the full reference.)*

## 4 · The file taxonomy

The canonical artifact types — the type system the PRD's elements are placed into (the operational lens is `where-does-this-belong.md`):

- **Entry contract** (`CLAUDE.md`) — identity, folder map, naming conventions, and the routing table. Read first.
- **Context** (`CONTEXT.md`) — a folder's or stage's current-state contract: inputs, process, outputs.
- **Role card** — identity, ownership, and judgment stance: who does the work and why. (A *specialist* when the work warrants a distinct character.)
- **Skill** — a packaged, repeatable procedure for a step.
- **Governance / rules** — permissions, approval, and escalation: who can do what, what needs review.
- **Reference (config)** — stable knowledge, conventions, templates, and lenses; deployment-scoped reference is **config**.
- **Working artifact** — per-run content being produced or acted on.
- **Connection spec** — configuration for an external tool / MCP (optional; permissions in it are proposed defaults until ratified into governance).
- **Local script** — mechanical work that needs no AI (fetching, moving, formatting, parsing). A first-class element of the protocol; use it for the deterministic parts.

## 5 · Structure & decomposition

A workspace is **a folder**. The work is decomposed into single-job units — one of two canonical shapes:

- **Pipeline** (sequential): **numbered stage folders** whose numbering encodes execution order. Each stage carries its own contract, reference material, and output.
- **Rooms** (parallel): **named workspaces/rooms** for distinct modes of work, routed from the entry contract. Each room carries its own context and skills.

Choose by the work's shape: a sequential, staged workflow → pipeline; a set of parallel modes/domains → rooms. Either way: one unit, one job. The canonical pipeline tree:

```
workspace/
├── CLAUDE.md                 ← L0: map, routing table, naming
├── CONTEXT.md                ← L1: task routing + shared resources
├── stages/
│   ├── 01_[job]/
│   │   ├── CONTEXT.md         ← L2: stage contract (Inputs / Process / Outputs)
│   │   ├── references/        ← L3: stage-local reference
│   │   └── output/            ← L4: hand-off point + human edit surface
│   ├── 02_[job]/
│   │   ├── CONTEXT.md
│   │   ├── references/
│   │   └── output/
│   └── 03_[job]/ …
├── _config/                  ← L3: shared config (conventions, style, structure)
├── shared/                   ← L3: cross-stage shared resources
└── setup/
    └── questionnaire.md      ← one-time factory configuration
```

**`output/` chaining:** stage N's `output/` is stage N+1's input. A human can edit what's in `output/` before the next stage runs, and the next stage reads whatever is there — the review gate lives at every boundary.

## 6 · Conventions & mechanisms

- **The routing table** (in `CLAUDE.md`) — the central mechanism. A table mapping a task to the files to read and skip: `Task | Go to | Read | (Skills)`. Without it, the agent reads everything and wastes context.
- **The stage contract** (L2 `CONTEXT.md`) — Inputs / Process / Outputs. The Inputs list **tags each file as L3 (stable) or L4 (per-run)**. This is the file system doing the work a framework would otherwise do in code.
- **Configure the factory** — a one-time setup (`setup/questionnaire.md` → `_config/`) configures the workspace; each run produces a deliverable through that config. The **engine (generic, reusable) is kept separate from `_config/` (deployment-specific)** so the workspace redeploys by swapping config.
- **Review gates** — at every stage boundary the human inspects and optionally edits `output/` before the next stage runs.
- **Naming conventions as the database** — files are found and moved by naming patterns declared in `CLAUDE.md`; no SQL, no vector store.
- **Scoped loading** — each unit loads only its layers; lazy-load reference material at the step that needs it, not at entry.
- **Single agent, context-switched** — the same model runs every stage; the folder structure controls what context it receives. If it delegates to sub-agents, the same structure supplies their context.
- **Plain text & Git** — everything is markdown/JSON, diffable and reversible; the workspace definition is the system.

## 7 · What the canon leaves to the builder

Latitude the canon does not fix — design these per the build, and record the call (an ADR proposal) where it's load-bearing:

- **A skill's internal shape** — what files a skill bundle contains is unspecified.
- **`shared/` vs `_config/` vs stage-local `references/`** — the boundary between them is not delineated; decide by scope (cross-stage → `shared/`; factory config → `_config/`; one stage → its `references/`).
- **Context ordering within a layer** — unspecified; the canon prescribes *what* loads, not the order.
- **Conditional / automated branching** — out of canonical scope (humans branch by choice between stages); designing automated branching moves toward being a framework.
- **Verification / audit / traceability** — a working practice and proposed future contract section (`Verify`), not yet required; design it in where the build needs provenance.
- **Pipeline vs rooms nesting** — the canon supports both but gives no rule for nesting one in the other.

## 8 · Provenance

Grounded in the ICM / Model Workspace Protocol canon (Jake Van Clief & David McDermott; open source, MIT) and the material in the Clief Notes community ([skool.com/cliefnotes](https://www.skool.com/cliefnotes/)). "ICM" and "MWP" name the same framework. This baseline is the **standalone default**: when a real target system is provided, design against *that* system as ground truth, and treat this only as the fallback the canon guarantees.
