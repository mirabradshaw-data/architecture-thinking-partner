# Architecture Thinking Partner — turn a PRD into a build

> **Hand it a PRD; it designs the ICM architecture *within your system* — challenging your thinking, never overruling it.** The downstream half of a two-tool ICM suite: [Chalky](https://github.com/mirabradshaw-data/chalky-prd) `→ PRD → ATP → build spec`.
>
> *Proven on real work: on its first run against a live system with a 67-decision ADR it proved its teeth — surfacing a flaw the architect had missed and overturning an existing decision. ([receipts](receipts/))*

The Architecture Thinking Partner takes a confirmed **PRD** and turns it into sound ICM architecture — a **build spec** a build conversation can pick up cold, that fits the system it lands in and the decisions already made. It's an ICM workspace: an interpretable engine you point at any system by swapping one config. It's the downstream half of a pair — a PRD interviewer draws the work out and stops at a PRD; this finishes what it deliberately leaves open (the flagged breakdown, the build target) and owns **draft → final**.

Most architecture review either **rubber-stamps** you (nods the plan through and adds nothing) or **hijacks** you (designs over your work and makes you fight to keep what you already knew was right). This does neither: it assumes a competent architect, designs *within* the system you already have rather than from first principles, surfaces the blind spots and the contradictions with decisions you've already made — and challenges with substance while leaving every call yours.

## Who this is for

This is for someone building their own architectural **taste** in ICM — whether you've already developed a strong feel for how a system should be shaped, or you're working to grow one. It's a **sparring partner** for the architecture step: you bring your ideas, your judgement, and your hard-won learnings; it challenges them, surfaces the blind spots, and tests them against the system and the decisions already made — so you come out with a sharper build *and* a sharper sense of why. It assumes you're in the room, thinking — especially when the work joins an existing system with its own conventions and prior calls.

If what you want is an ICM that simply *does* the architecture for you — hands back a folder layout with none of your input or thinking — this won't be to your taste. The whole point is that the architecture stays yours: the tool makes it better, it doesn't stand in for you.

## How to use it

The person drops a PRD into `input/` and types **ARCHITECT** to start (the trigger lives in `CLAUDE.md`). Three ways to run it:

1. **Claude Project** — add these files as project knowledge, put the PRD in the conversation, and type `ARCHITECT`. With no filesystem, it hands you each output as an artifact to save (named as below).
2. **Claude Desktop (local folder connector)** — point Desktop at this folder, drop the PRD into `input/`, and type `ARCHITECT`; outputs are written into `output/`.
3. **Drop into an ICM workspace** — place the folder in your existing workspace, route to it, and type `ARCHITECT`.

**Standalone or wider.** If the work joins an existing system, point it at that system — swap `_config/sample-target-system/` for your own system's `CLAUDE.md` / `CONTEXT.md` / governance / decisions, so recommendations fit what's there. If it stands alone, it designs against the **generic ICM baseline** that ships in `_config/`. Either way it always has a sound architecture to design against.

## What you get

One run produces a linked set, sharing a slug:

- **A finalised PRD** (`output/prd-[slug].md`) — the PRD it picked up, reviewed with you and set **draft → final**.
- **A build spec** (`output/build-spec-[slug].md`) — the mission carried across **in the person's own words**, then the ICM structure, build detail, the resolved artifact breakdown, placement and fit against the system, a staged-and-gated build plan, and an end-of-build audit. Once it's been audited against the PRD and you've ratified it, it's promoted to **`ready`**.
- **ADR proposals** (`output/adr-proposals-[slug].md`) — the decisions worth recording, **proposed** in the shape of your decisions register for you to ratify.

The set travels together; a build conversation starts from it cold. It stops at a `ready` spec — building the thing is the next stage, with you in the room.

## What it will not do

- **It won't make the call.** It recommends, challenges, and confirms; placement and design stay yours.
- **It won't ratify.** It proposes ADR entries; you write them to the register.
- **It won't build the thing.** It produces a spec, not a workspace — no skill files, no folders instantiated. That's the next stage, with you in the room.
- **It won't design around your governance.** Where the build would cross one of your rules, it names the conflict upfront rather than quietly routing around it.
- **It won't design from first principles when a system is given.** It grounds in your conventions and your prior decisions; the textbook is for when there's no system to honour.
- **It won't rewrite your mission, act externally, or stand in for an expert.** Your north star is copied across verbatim, not neutralised into spec; nothing is sent or fetched without asking; and harm-risk domains (medical, legal, crisis) get a straight decline — with an offer to help you prepare for the real expert instead.

## Ships with a sample

It ships with a sanitised **sample target-system** (`_config/sample-target-system/`) — a worked existing system, with its own conventions, governance, and decisions register — so you can see the wider mode (designing into a system that's already there, on *its* terms) without wiring up your own first. Swap it for your own system's config to point the tool at your build.

This sample target-system is a public-shareable version of the work system that I, the builder of this workspace, run. That's my actual CLAUDE.md file (with a few removals), the real-life tree structure, and actual architectural decisions cherry-picked from my ADR (the real one is in tabular form and 67 decisions deep). It's been adjusted for privacy, security and personal reasons and because handing away that much IP in a public git felt ill-advised. But it's there and it is in heavy use on a daily basis. If you're curious about what I run, I recommend having a look around. I tidied it up so that it could hopefully add value for others.

## A real worked run — receipts

The `receipts/` folder holds an actual end-to-end run of the suite, lightly sanitised: a PRD that **Chalky** (the upstream interviewer) produced, picked up here cold and turned into a build plan.

- the finalised **PRD**, the **build spec**, and the **ADR proposals** it produced;
- **`assessment-atp-first-run.md`** — the model-side assessment of how the run went against this tool's own brief and README;
- **`owner-account.md`** — my architect's-eye account from the gates (the human counterpart to that assessment);
- **`what-we-changed.md`** — the frictions the run surfaced and the fixes folded back in before shipping;
- **`audit-mode-stub-EXPERIMENTAL.md`** — a stance-flip I identified through the run: using ATP as a "step 0" to *audit and help populate* a system, rather than design within one taken as done. A candidate future feature, shipped as a worked idea — **not wired into the tool**.

The **input** side of this run — the PRD this tool consumed — lives in the **[Chalky receipts](https://github.com/mirabradshaw-data/chalky-prd/tree/main/receipts/mira-run)** (the companion tool's worked example); this tool's `input/` ships empty, ready for your own PRD.

**Beyond the shipped example.** The worked run above used the generic ICM baseline. Since then, ATP has had its **first full run against my complete live system** — the real thing, with a tabular ADR 67 decisions deep. It did exactly what it was built to do: it **proved its teeth**. It didn't nod the architecture through — it surfaced a real flaw in an existing decision, where I (the architect) had conflated two things that could be cleanly partitioned, and that decision was overturned and reshaped on the spot.

The specifics, for the curious: my cross-system principles — the architecture and rules both my systems inherit — were, before this run, promoted to the cross-system layer only when *applicable* to both, to keep context lean and omitted if irrelevant. ATP showed they could be promoted without being *activated*: present for every build-time activity, but sliced out of runtime context by the system's existing structure — so promoting them cost nothing at runtime, and they were already there for all build-time work. A strict improvement, and I adjusted the register immediately, on its first real run. Teeth proven; headline claim met.

## Part of a suite

The Architecture Thinking Partner is the **downstream** half of a two-tool suite. It consumes a PRD; its upstream companion, **[Chalky](https://github.com/mirabradshaw-data/chalky-prd)**, draws the work out of the person and produces that PRD. Run Chalky first, then hand its PRD here — the seam is the PRD, picked up cold without re-asking what the work is.

## Built by & inspiration

Built by **Mira Bradshaw** with assistance from Claude (Claude Code). It's the downstream half of a suite: a PRD interviewer (Chalky) draws the work out and produces the PRD; this turns that PRD into architecture. The engine is generic — only the target-system config changes — so the same reviewer serves any system you point it at.

The thing I keep coming back to: a model is often the better coder these days, but the engineering and especially the architecture — what fits the system, what honours the decisions already made, what the build is really *for* — is a judgement worth keeping with the human. That judgement is heavily reliant on memory, taste, decisions, experience and, as much as we try to provide those to a model with ICM, AI is fundamentally a blank slate (tabula rasa) every time the context clears. This tool is built to *augment* the human judgement, never to replace it. And to set up the model with enough relevant context to be a thinking partner worth talking to in the architectural domain.

## A note on this version

Everything around the tool has moved; the tool has not. In step with a new version of the upstream **Chalky**, I brought its table-format `receipts/README.md` here for suite consistency, added a top-of-page hook, and recorded ATP's first full run against my real live system (see "Beyond the shipped example" above). Before the final push I also had a model red-team ATP's own claims — that its declines fire, and that it stays honest about its domain rather than force-fitting non-ICM problems. They held ([`receipts/red-team.md`](receipts/red-team.md)). As with Chalky: proving the claims means you don't touch the thing you're proving — so the engine, the sample target-system, and the worked run are all exactly as they shipped (the commit history shows it either way).

## License

Released under the [MIT License](LICENSE) — © 2026 Mira Bradshaw. Use it, adapt it, build on it.

## Acknowledgements

- **Jake Van Clief**, for ICM — the Interpretable Context Methodology this is built on, learnt through [*Clief Notes*](https://www.skool.com/cliefnotes).
