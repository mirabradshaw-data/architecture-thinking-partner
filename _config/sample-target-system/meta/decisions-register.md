# Architecture decisions register (ADR-lite)

> **What this is.** A light record of architecture decisions — the concrete shapes the system took, why, plus what would reopen it. Each entry is short and points at the reasoning. Append and supersede — never silently rewrite.

## Schema

One entry per decision: a title, a short paragraph of what was decided and why, and — where useful — the named trigger that would put it back on the table. Status is `active`, `until:<trigger>` (the decision retires when a named event fires), or `superseded:<later decision>`.

---

## Recent decisions

### Memory stays unified
All learned memory lives in one `memory/` store, with `load-with:` tags routing the right files to the right task, rather than being split into per-agent stores. Keeping it unified means a single canonical home, no duplication, and no question about which copy is authoritative. Reopens if the system ever needs agents to be portable independently of the shared memory.

### Sort conventions
The workspace uses explicit, stable sort conventions so that ordering is predictable for both humans and tools — numeric prefixes to group and order actors, and a small set of reserved prefixes to mark "build-reference" and "never-touch" material distinctly. Predictable ordering is what lets a deterministic tool prove it returns the same result every run. Reopens if a better scheme emerges or the renumber-on-insert cost becomes annoying.

### Deterministic / interpretive boundary
Reliability-critical mechanical work — date arithmetic, file mechanics, status flips, parsing, filtering, diffing, staleness checks — moves to a deterministic substrate of scripts. Interpretation — tiering an item, deciding to re-commit, defer, or close, spotting an anomaly, routing, de-duplication — stays with the judgment layer. The split puts each kind of work where it is trustworthy: machines for the mechanical, judgment for the interpretive.

### Disjoint write surfaces for actors
Each actor in the system owns a disjoint write surface — no two actors write to the same place — and the gates that control writes live at the boundaries between surfaces. This makes it unambiguous who changed what, keeps an allow-list able to scope writes tightly, and means a mistake is contained to one surface rather than smeared across the system.

### Subagent no-ASK-action rule
A fully abstracted sub-agent never performs an ASK-tier action itself. It produces proposals and staged artifacts only; the orchestrator and Mira gate whether anything is applied. Abstracted sub-agents run non-interactively and so cannot pause to ask — defaulting them to "read and return, never act" keeps an un-approved action from slipping through where no one could have approved it or stalls their workflows.

### Glass-box preservation for sub-agents
When a sub-agent does work, that work stays auditable: output is staged in a known place, appended with a timestamp, copied rather than cut (the source is never destroyed), and a run-log line records each invocation. You can always reconstruct what a sub-agent did from the artifacts it left behind, rather than having to trust an opaque step.

### Fixture-pinning
A deterministic tool's regression fixture pins both the as-of date and the input data it runs against — it never diffs the tool's output against live system state. A check that compares against live state quietly rots: as the real data drifts, the "expected" answer drifts with it, so the check keeps passing while no longer testing anything. Pinning both the date and the input freezes a real answer the tool must keep reproducing.

### Single-consumer state channels
A mutable state bit (for example, a "processed" marker) is only a valid signal if three things hold: it has exactly one consumer, it flips last — after the work it represents has actually committed — and its history is preserved in the run log. These constraints stop a status flag from drifting out of step with reality, which is the classic way a "done" marker comes to lie.

### Three-layer audit
Auditing the system is separated into three layers: scripts gather the evidence (the facts), a fresh-context reviewer forms judgments on a rotation, and promotion of anything into the system's durable record is human-only. Separating evidence from judgment from promotion keeps the cheap mechanical part automated, the interpretive part genuinely fresh-eyed, and the consequential part under human control.

### Decided against a synthetic malformed-input fixture suite
A pre-built suite of synthetic malformed-input fixtures was considered and rejected. At single-writer scale, the cheaper and truer test is real usage flowing through an input-integrity check that ships with the tool — that surfaces the malformations that actually occur, rather than the ones imagined in advance. Reopens if malformations start recurring, the integrity check gets heavily rewritten, or the system gains other writers or scale.
