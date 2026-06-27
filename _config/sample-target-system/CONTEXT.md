# CONTEXT — current state

> This file is the starting point for every session. It contains current state — not rules or conventions (those live in `.claude/CLAUDE.md`).
> Update the "Current state" section when things change significantly.

---

## What this workspace is

Mira's personal operating system. It captures raw notes daily, processes them into structured trackers, meeting notes, and person files, and surfaces what matters at session start. Leo (the chief-of-staff agent) orchestrates the workspace; specialists handle bounded domains (calendar, the governance cycle, relationship intelligence).

The workspace is markdown-first and single-writer: Mira is the only author. The agent proposes; Mira approves. The files are the system.

---

## Folder map

| Folder | Purpose |
|---|---|
| `daily/` | Raw daily notes — one file per day, fast unstructured capture |
| `meetings/` | Processed meeting notes — one file per meeting |
| `people/` | One file per person — open items, context, interaction log |
| `trackers/` | Tracker items: `items/` (one .md file per item) |
| `config/` | Stable context: `role.md`, `stakeholders.md`, `rhythms.md`, `projects.md`, `preferences.md`, `operating-principles.md` |
| `tools/` | Deterministic scripts (e.g. the tracker-query tool) — mechanical work the judgment layer relies on |
| `meta/` | Decisions register / ADR and other cross-system records |
| `data/` | Established organisational reference (frameworks, templates — read when task-relevant) |
| `work-knowledge/` | Vaults: `working-memory/` (inbox + themes), `insights-vault/` (incl. `inputs/` staging area), `strategy-vault/`, `narratives/`, `data/` (personal reference — not read by system) |
| `workflows/` | Recurring workflows: `slt-board-cycle/` (governance cycle), `calendar/` (baseline processing) |
| `memory/` | Layer 3 memory: learned patterns, feedback, stable domain knowledge |
| `_system/` | System health and meta: `flags.md`, `resolved-flags.md`, `run-log.md`, `approval-log.md`, `observations.md` |

---

## Current priorities

See `config/role.md` for the full mandate, `config/projects.md` for all active projects, and `config/goals.md` for 90-day priorities and the end-of-year success definition (the briefing skill cross-references `goals.md` for drift detection).

---

## System state

- **People files:** Created per the per-person convention; template at `people/TEMPLATE-person.md`.
- **Tracker items:** All items in `trackers/items/` per-item convention. Archived items live outside the active system and are never read unless explicitly asked. Deterministic retrieval runs from `tools/` first at triage, sweep, and session-start — full-read only what it surfaces.
- **Specialists:** Calendar, SLT/Board cycle, and relationship-intelligence specialists each have a role card and an invocation contract (`CONTEXT.md`).
- **Decisions register:** Lives in `meta/` — the concrete-shape record of architecture decisions, beside the operating principles.

---

## System history and known deferrals

This section exists so cold-read sessions have context before forming a view. Gaps here are intentional decisions, not neglect.

| Item | Status | Detail |
|---|---|---|
| **System rebuild** | Complete | Rebuilt from a markdown foundation; per-item tracker, role cards, and skill files built from that point. Prior content archived. |
| **Calendar baseline** | Active — CSV workflow | Weekly rolling CSV (14-day window) → rolling baseline. Fortnightly governance CSV → governance baseline. Both processed by the calendar specialist via `workflows/calendar/inputs/exports/`. |
| **Vault synthesis workflows** | Active | Capture is live for the insights and strategy vaults. Synthesis-workflow design is currently run on demand at Mira's request. |
| **PDP / development cycle** | Not yet mapped | Cadence not yet modelled in the system. To be added as a recurring workflow. |
