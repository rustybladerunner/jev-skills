# Jev skills

> **Experimental research and workflows — not validated for production use.**
> Results come from limited synthetic studies and early operational trials, with
> incomplete independent human validation. They do not establish general
> reliability, safety, or cost savings. Validate each use case on representative
> data, keep consequential actions subject to explicit authorization and checks,
> and supervise trials. Interfaces and recommendations may change.

A practical guide to using decision models, with reusable agent workflows and evidence from our own experiments.

This is the front door for our Jev work. [Aldertrace](https://github.com/rustybladerunner/aldertrace) holds the reproducible routing study and enforcement instruments. These projects are independent of TypeSafe and the other model authors.

## Business review — September 2026

**Reviewed September 25. Decision: use bounded semantic recommendations; expand authority only where measured task outcomes justify it.** This is a monthly business review format for an experimental project, not a claim of commercial deployment or audited financial results.

### Business purpose

Some software needs a small decision before it needs an expensive answer: which queue should receive this item, which tool is appropriate, or whether a prerequisite needs another check. A decision model turns text into named choices that software can inspect. The business objective is **lower total cost per accepted outcome, with acceptable errors and less review work**.

Use deterministic code when a rule, exact match or verified receipt already answers the question. Use a decision model for the remaining semantic ambiguity. Use a generative model when the work requires writing or inventing an answer. The decision model does not replace that work.

### Where it fits

| Use case | Useful role | Boundary / measure of success |
|---|---|---|
| Research and support triage | Rank items, suggest topic or queue, flag ambiguity | Measure recall of useful items and review time; retain recoverable items until discard quality is established |
| Tool or workflow routing | Recommend from a small, explicit menu | Trusted code checks permissions, available tools, budget and required inputs |
| Prerequisite routing | Identify potentially redundant reading or checks | Skip only when current evidence meets the declared requirement; count routing overhead |
| Candidate reranking | Rank already retrieved, permitted material | Compare with existing similarity/ranking rules; preserve provenance and privacy |
| Cheap/expensive model selection | Suggest when a smaller model may suffice | Measure accepted answers, retries, latency and full cost against a fixed-model baseline |
| Local decision workloads | Evaluate an appropriate local checkpoint for repetitive classification | Include loading, memory pressure, truncation and fallback costs; local does not imply correct |

Payments, trades, access grants, irreversible deletion and arbitrary shell execution require their own authorization and deterministic controls. A model score is not that authorization. Open-ended planning, code generation and factual research require capabilities beyond a finite-choice interface.

### What has worked for us

| Outcome | Evidence | What we can claim |
|---|---|---|
| More eligible prerequisite skips | Jev plus enforcement: **34/40**, deterministic rules: **20/40**; both **0/40 observed prohibited skips** | Added semantic coverage on a small synthetic held-out study; not a production safety guarantee |
| Routing basic application requests | Three distinct live integration checks selected chat, draft-only and clarification; stable-ID replay made no new call | Working transport, schema and routing boundary. A downstream draft failed, so this was not full workflow success |
| Useful research ranking signal | **109/146** agreement with an agent-written relevance key; **AUC 0.78** | Supports annotation/ranking experiments. Recall was **20/42** at the 0.5 threshold: insufficient for automatic discard |
| Detecting a consequential weakness | Choice order changed **6/120** decisions, all refusal versus paid-authoring routes | The experiment improved our refusal policy; repeating one order was not enough to reveal the problem |
| Bounded editing with acceptance checks | A separate coding worker produced accepted, reviewed edits and tests | This is execution-pipeline evidence, not proof that Jev wrote code or caused savings |

The first row is [publicly replayable](https://github.com/rustybladerunner/aldertrace/blob/main/experiments/v002/REPORT.md). Later rows are **maintainer-reported operational aggregates**, with private source receipts retained and not independently reproduced by this repository. [Case studies](docs/case-studies.md) record the denominators, failures, attribution and accounting boundaries.

### Economics and scorecard

| KPI | Current reading | Decision |
|---|---|---|
| Incremental safe coverage | +14 eligible skips on the 40-case synthetic subset | Continue bounded semantic-routing research |
| Net observable input proxy | **-12,240 tokens** for Jev in v002 | Routing overhead exceeded stipulated reading avoided; no token-saving claim |
| End-to-end cost per accepted task | Broad benefit unestablished | Include authoring, cached reads, review, failures and retries |
| Stability | **5%** option-order flips on 120 operational test items | Evaluate context perturbations as well as option order |
| Human label validation | Incomplete | Keep findings provisional; agent agreement is not human adjudication |
| Commercial ROI / customer adoption | Not measured | No revenue, customer, payback or 99% automation claim |

One accepted coding-worker run used **35% fewer new frontier tokens**, yet an illustrative pricing calculation made it about **2.1 times as expensive** because frontier calls and context rereads increased. Another dispatcher-authored task passed on its first proposal, but lacked a paired baseline and complete authoring accounting. These are useful engineering successes and cost lessons, not demonstrated Jev ROI.

### Jev and related models/tools

These are different implementations with a similar decision interface, not interchangeable versions of one model. Published benchmark percentages are not a common leaderboard for our workloads.

| Candidate | What it is | Our current position |
|---|---|---|
| [TypeSafe Jev](https://docs.typesafe.ai/introduction) | Hosted typed-decision service | Measured in Aldertrace and bounded routing/triage pilots; use task-specific validation |
| [Laya](https://github.com/NandhaKishorM/laya) | Local decision-model family with distinct checkpoints | Source reviewed; fake-response adapter tested. No completed matched local quality evaluation |
| [Verdict / Verdict 2.0](https://github.com/Heman10x-NGU/openJev-verdict-2.0) | Upstream distinguishes a general Verdict checkpoint from a specialized typed-workflow model | Our local DecisionEngine observations must not be attributed to every model in that repo |
| [SimpleJev](https://github.com/featherless-ai/simple-jev) | Classifier/decision endpoint over an underlying open model | Candidate interface; no matched internal quality result |
| [Aldertrace local scorer](https://github.com/rustybladerunner/aldertrace/tree/main/logitpick) | One-token letter scoring through an existing Ollama model | Experimental scorer; entropy concentration is not correctness probability; local comparison incomplete |
| Deterministic rules / simple classifier | Exact policy or a small learned baseline | Always include when the task permits; a model must earn its overhead |

Skills, evidence frameworks, memory systems and coding workers are **tools around models**. They should not be counted as additional models or credited with results from a different component.

### Risks and next decisions

The September 24 [JevOut preprint](https://arxiv.org/html/2609.30243v1) adds context sensitivity to the evaluation agenda. Its optimized attack results are not ordinary-traffic failure rates. The [ACL conformal-routing paper](https://aclanthology.org/2026.acl-srw.70/) offers a risk-based threshold approach, with distribution and label assumptions. [LLMRouterBench](https://arxiv.org/abs/2601.07206) reinforces the need for simple baselines.

1. Test fresh, answer-preserving context changes and option permutations; record raw disagreement before averaging.
2. Calibrate refusal against explicit action losses on separate data, then evaluate once on fresh held-out families.
3. Continue a matched local-candidate comparison after checkpoint, resource and licensing prerequisites are satisfied.
4. Prove practical value on accepted tasks with all costs counted before expanding automation.

See the [research review and acceptance criteria](docs/research-review-2026-09.md). These are next decisions, not completed experiments or authorization to run them.

## Use the workflows

- **[jev-integrate](jev-integrate/SKILL.md):** review changes against existing code, evidence and regression checks.
- **[jev-hypothesize](jev-hypothesize/SKILL.md):** turn an efficiency claim into a bounded, reproducible comparison.

The skills are instructions for a coding agent. Your agent and tools perform the work; installation grants no access, spending allowance or permission to publish.

## Try the example

Python 3.11 or newer is enough. From this directory:

```sh
python -B examples/demo.py
python -B -m unittest discover -s examples -v
```

The example runs a real check on disposable synthetic files. It then compares
five proposed skips with the evidence needed to permit them. One has current
passing proof. The others have stale, failed, mismatched or missing proof.
An explanation saying "the check passed" cannot supply a runner receipt. The
runner constructs the receipt in code; text or a deserialized dictionary is not
accepted as one.

Expected result: five proposed skips, one permitted skip, four rejected skips.
The accounting example also shows why avoiding one read can still cost more
overall: 500 illustrative input tokens avoided minus 600 of routing overhead
leaves **-100**. Those token values are assigned for teaching. No model is called,
no tokenizer is used, and the example is not a Jev performance benchmark.

For **jev-integrate**, the proposed shortcut is accepting every `skip`
recommendation. The example exposes the four failures that shortcut would allow.
For **jev-hypothesize**, the hypothesis is that routing reduces total input.
The same example gives a negative result once overhead is counted.

## Install and use

Copy either named skill folder into the skills directory supported by your agent
host, keeping `SKILL.md` and its `references` folder together. For Codex, select
`$jev-integrate` or `$jev-hypothesize` after the host discovers the installed skill.
Other hosts may need their own import mechanism; cross-host discovery is not claimed.

Then give the agent a concrete request, for example:

> Use jev-integrate to review this proposed routing change against our current
> implementation. Reproduce any claimed regression before changing code.

> Use jev-hypothesize to design a test of whether routing saves total input
> tokens. Start from our existing results and allowance. Do not run paid calls.

Each skill includes a small project-context template. Map it to the records your
project already has. For Aldertrace, use its existing protocol and domain memory.
For a new project, fill in the relevant facts; mark missing facts unknown. Never
invent prior results or turn a missing budget into permission to spend.

## What this does and does not establish

These workflows came from Aldertrace's prerequisite-routing experiments and
failure-recovery work. The runnable example demonstrates the evidence boundary
and accounting arithmetic. It does not measure whether these Markdown skills
improve a coding model, make Jev safe in production, or reduce real task cost.

The work was developed with AI coding and review assistance. Model-generated
agreement is not independent human validation. Contributions should include a
reproduction, the expected outcome, and any new limitation they introduce.

MIT licensed; see [LICENSE](LICENSE). Jev is a third-party service. This project
does not claim affiliation or endorsement. Mount Jeverest remains a future idea.
