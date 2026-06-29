# Receipts — a real worked run

One complete, real run of the Architecture Thinking Partner — proof it works on real work, and a worked example to learn from. It picks up cold from the upstream **[Chalky](https://github.com/mirabradshaw-data/chalky-prd)** run (`mira-run`) and turns that PRD into a build plan. Lightly sanitised — the company appears only as "an FMCG company in New Zealand."

The **input** side of this run — the PRD this tool consumed — lives in the [Chalky receipts](https://github.com/mirabradshaw-data/chalky-prd/tree/main/receipts/mira-run).

| File | Type | Written by | What it is |
|------|------|------------|------------|
| `prd-policy-standards-authoring.md` | Output | Model, from Mira | The PRD it picked up, reviewed with me, and set draft → final. |
| `build-spec-policy-standards-authoring.md` | Output | Model, with Mira | The build spec — ICM structure, build detail, placement and fit, a staged-and-gated build plan, and an end-of-build audit. |
| `adr-proposals-policy-standards-authoring.md` | Output | Model, with Mira | The decisions worth recording, proposed in the shape of my decisions register. |
| `assessment-atp-first-run.md` | Meta | Model | The model-side assessment of how the run went against this tool's brief and README. |
| `owner-account.md` | Meta | Mira | My architect's-eye account from the gates — the human counterpart to the model assessment. |
| `what-we-changed.md` | Meta | Mira | The frictions the run surfaced and the fixes folded back in before shipping. |
| `audit-mode-stub-EXPERIMENTAL.md` | Meta | Mira | A stance-flip I spotted through the run — using ATP as a "step 0" to audit and help populate a system, not just design within one. A worked idea, **not wired into the tool**. |

## The real-system run (artifacts held private)

The README's headline — ATP's first full run against my complete live system (a tabular ADR 67 decisions deep) — isn't shipped as files here, and deliberately: that system is real, in daily use, and holds the IP I kept out of the public sample. What I can put on the record is the outcome.

ATP proved its teeth. It didn't nod the architecture through — it surfaced a real flaw in an existing decision, where I (the architect) had conflated two things that could be cleanly partitioned, and that decision was overturned and reshaped on the spot.

The specifics: my cross-system principles — the architecture and rules both my systems inherit — were, before this run, promoted to the cross-system layer only when *applicable* to both, to keep context lean. ATP showed they could be promoted without being *activated*: present for every build-time activity, but sliced out of runtime context by the system's existing structure — so promoting them cost nothing at runtime, and they were already there for all build-time work. A strict improvement, and I adjusted the register immediately, on its first real run.

The inspectable proofs in this folder are the sample run and the red-team; this note stands in for the real-system result they can't show without exposing a private system.

## Red-team — proving the claims

Commissioned before shipping: a model-run adversarial test of ATP's guardrails and domain honesty. The full results were reviewed inline; the summary lives in the file below.

| File | Type | Written by | What it is |
|------|------|------------|------------|
| `red-team.md` | Meta | Model | Adversarial test — all 6 hard/soft declines fired cleanly, and ATP correctly refused two non-ICM problems (a coffee-shop layout and an e-commerce backend) rather than force-fitting. |
