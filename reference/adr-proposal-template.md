---
file-type: template
workspace: architecture-thinking-partner
last-updated: 2026-06-26
status: active
referenced-by: [gate2-architecture]
---

# ADR-Proposal Template

The shape of the artifact gate 2 produces alongside the build spec: `output/adr-proposals-[slug].md` — the decisions worth recording, **proposed for the target system's decisions register**. These are *proposals*: this stage proposes, the person ratifies them into the register (see `rules.md`). You never write to the real register, and you never silently rewrite an existing decision — propose, append, supersede; the human commits.

## Match the target's register first

If the target system has a decisions register, **match its format and conventions** — it's ground truth (`where-does-this-belong.md`). Read it: prose or table, its heading style, its status vocabulary. Produce proposals in *its* shape so they paste straight in. The shape below is the standard ICM **ADR-lite** — the default for a standalone build or a system whose register doesn't specify one.

The produced file opens with this frontmatter:

```
---
file-type: adr-proposals
slug: [slug]                          # carries over from the PRD / build spec
source-build-spec: output/build-spec-[slug].md
target-register: [path to the system's decisions register]   # if wider; omit if standalone
created: [YYYY-MM-DD]
status: proposed                      # proposals — the person ratifies into the register
---
```

## What earns an entry

Propose an entry for a decision that **shaped the architecture and someone later would need the reasoning for** — the concrete shapes the build took and why: a placement call against the system's conventions, an engine/config split, a reuse-vs-build choice, a governance-conflict resolution, a deliberate trade-off or risk accepted at gate 2. Not every small choice — the ones that would otherwise become an unexplained "why is it like this?" later.

## Entry shape — prose (ADR-lite default)

One entry per decision: a title, a short paragraph of *what was decided and why*, and — where useful — the named trigger that would reopen it. Status is `active`, `until:<trigger>`, or `superseded:<later decision>`.

```
### [Decision title — the shape the architecture took]

[What was decided and why, in a short paragraph: the concrete choice, and the reasoning that
makes it the right call. Point at the reasoning; keep it tight. Where it resolves something the
PRD left open or sits against a prior decision, say so.]

[Optional: the named trigger that would put this back on the table — "Reopens if …".]

Status: active | until:<trigger> | superseded:<existing decision this replaces>

*Proposing context (strip on ratification): [what in this build raised it — e.g. resolves the §6
placement of X; supersedes the system's existing "Y" decision]. — proposed, awaiting the person's ratification.*
```

The entry itself is in the register's native shape so it drops in clean; the italic *proposing context* line is meta — it helps the person decide, and is removed when they ratify.

## Entry shape — table (when numerous, or the register is already tabular)

When there are **many** decisions, or the **target register already uses a table**, produce a table instead — same content, less bloat (this mirrors the tabular form some real registers use):

| Decision | What & why | Reopens if | Status | Proposing context (strip on ratify) |
|---|---|---|---|---|
| [title] | [the choice + the reasoning, tight] | [named trigger, or —] | active / until:<trigger> / superseded:<X> | [what raised it; awaiting ratification] |

Match whichever form the target register uses; default to prose for a handful, table for many.

## Superseding an existing decision

If the build's architecture replaces a decision already in the register, **propose a supersede — never silently rewrite the existing entry**. Name the decision being superseded in the status (`superseded:<that decision>`) and state in the new entry what changed and why. The person ratifies the supersede; the original stays in the register's history (it appends and supersedes, it doesn't erase — see the register's own note).

## Before you hand off

- Each entry records a decision that genuinely shaped the architecture, with the reasoning — not trivia.
- The format matches the target system's register (prose or table); standalone uses the ADR-lite default.
- Nothing is written to the real register; every entry is a proposal, marked as such.
- Any supersede is proposed as a supersede, naming what it replaces — never a silent rewrite.
- Risks the person consciously accepted at gate 2, if they shaped a decision, are captured here (not just in the build spec's §7), so the register carries the *why* behind a knowingly-accepted trade-off.
