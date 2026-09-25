# Jev skills

> **This is experimental. We haven't validated it for production use.**
> We have results from small synthetic studies and early trials. Independent
> human review is incomplete, and we haven't shown general reliability, safety,
> or cost savings. Test it on data that represents your use case, supervise
> trials, and keep permissions and required checks in place. Things may change.

We're figuring out where Jev and similar decision models actually help. So far,
we've found useful routing decisions, missed useful items, and cases where doing
less work still cost more. This repo brings those results and our agent workflows
together.

Start here for the use cases and current position. [Aldertrace](https://github.com/rustybladerunner/aldertrace)
contains the routing study, saved results, and code you can run to check them.
We're independent of TypeSafe and the other model authors.

## Business review — September 2026

**Reviewed September 25. Our position: keep testing small routing decisions.
Give them more responsibility only when the results justify it.**

This is a monthly business review of an experimental project. We aren't reporting
commercial deployments or audited financial results.

### What we're trying to improve

Sometimes the next step is a small choice: which queue gets an item, which tool
fits a request, or whether a check needs to run again. A decision model chooses
from a menu we define. The software can then inspect that choice before acting.

We want **lower total cost per accepted result, acceptable errors, and less
review work**. If a rule, exact match, or current test result already answers the
question, use that. Try a decision model when the remaining choice needs an
interpretation of text. Writing code, drafting an answer, and doing research still
need their own tools.

### Where we'd use it

| Use case | What the model can help with | What we need to check |
|---|---|---|
| Research and support triage | Rank items, suggest a queue, flag unclear requests | How many useful items it misses and how much review time it saves. Keep items recoverable until discard quality is established |
| Tool or workflow routing | Choose from a small list of available actions | Code must check permissions, tools, budget, and required inputs |
| Repeated reading or checks | Suggest work that might already be done | Skip only when current evidence meets the requirement. Count the cost of making the routing decision |
| Reranking retrieved material | Put useful, permitted results nearer the top | Compare with the existing ranking method. Keep source records and privacy controls |
| Choosing a cheaper model | Suggest when a smaller model could do the job | Compare accepted answers, retries, time, and full cost with using one fixed model |
| Repeated local decisions | Classify text with a suitable local model | Count loading, memory use, cut-off inputs, and fallback costs. Running locally doesn't establish correctness |

A model score doesn't authorize payments, trades, access changes, deletion, or
shell commands. Those actions need explicit permission and checks in code.

### What has worked, and what hasn't

| What we tried | What happened | What that tells us |
|---|---|---|
| Skipping prerequisites with evidence checks | Jev allowed **34/40** eligible skips; rules allowed **20/40**. Both recorded **0/40 prohibited skips** | Jev handled more eligible cases in this small synthetic study. That doesn't establish production safety |
| Routing application requests | Three live checks selected chat, draft-only, and clarification. Replaying the same request ID made no new call | The routing and replay checks worked. The downstream draft failed, so the whole task did not succeed |
| Ranking research material | **109/146** agreement with an agent-written answer key; **AUC 0.78** | Worth testing for ranking. It found only **20/42** useful items at the 0.5 threshold, so automatic discard isn't justified |
| Changing option order | **6/120** decisions changed between refusal and paid authoring | Repeating one order missed a weakness that changing the order exposed. We changed the refusal policy |
| Applying reviewed code changes | A separate coding worker produced accepted edits and passing checks | The editing process worked in those trials. Jev didn't write the patches, and these results don't prove Jev saved money |

You can [replay the first study](https://github.com/rustybladerunner/aldertrace/blob/main/experiments/v002/REPORT.md).
The later results are our summaries of private run records. This repo doesn't
independently reproduce them. The [case studies](docs/case-studies.md) give the
counts, failures, and limits without publishing private source material.

### Costs and scorecard

| Measure | What we know | What we'll do with it |
|---|---|---|
| Additional eligible skips | +14 on the 40-case synthetic subset | Keep testing whether text-based routing adds useful coverage |
| Estimated input tokens saved in v002 | **-12,240 tokens** for Jev | Making the decisions cost more input than the assumed reading avoided. We can't claim token savings |
| Full cost per accepted task | A general benefit is unproved | Count authoring, cached reads, review, failures, and retries |
| Consistency across option orders | **5%** of 120 decisions changed | Test changes to context as well as option order |
| Human review of labels | Incomplete | Treat the findings as provisional. Agreement between agents isn't human review |
| Commercial return or customer adoption | Not measured | Make no revenue, customer, payback, or 99% automation claim |

One accepted coding-worker run used **35% fewer new frontier tokens**, but an
illustrative cost calculation made it about **2.1 times as expensive**. More calls
and repeated context reads outweighed the reduction. Here, frontier refers to the
larger model used for coding and review. Another task passed on its first cheap-model
proposal, but we didn't have a paired baseline or complete authoring costs.
Useful results, but no proven Jev return on investment yet.

### Jev and the other candidates

These tools expose similar kinds of choices, but they aren't interchangeable
versions of one model. Their published benchmark scores aren't a shared test of
our workload.

| Candidate | What it is | Where we are with it |
|---|---|---|
| [TypeSafe Jev](https://docs.typesafe.ai/introduction) | Hosted service for choosing typed outputs | Tested in Aldertrace and small routing/triage trials. Each use case still needs validation |
| [Laya](https://github.com/NandhaKishorM/laya) | A family of local decision models | We've reviewed source and tested an adapter with simulated responses. No completed matched test of local model quality |
| [Verdict / Verdict 2.0](https://github.com/Heman10x-NGU/openJev-verdict-2.0) | A general Verdict model and a separate model for typed workflows | Our local DecisionEngine observations don't establish results for every model in that repo |
| [SimpleJev](https://github.com/featherless-ai/simple-jev) | A classification endpoint using an underlying open model | A candidate to test. We don't have a matched internal quality result |
| [Aldertrace local scorer](https://github.com/rustybladerunner/aldertrace/tree/main/logitpick) | Scores single-letter choices with an existing Ollama model | Experimental and incompletely evaluated. A concentrated score distribution isn't a probability of being correct |
| Rules or a simple classifier | Fixed rules or a small learned baseline | Include them whenever they fit. A more complex model needs to justify its cost |

Skills, memory systems, evaluation tools, and coding workers support this work.
They aren't additional decision models, and we shouldn't give one component
credit for another's results.

### What we should test next

The September 24 [JevOut preprint](https://arxiv.org/html/2609.30243v1) gives us a
reason to test changes to context. Its optimized attacks don't measure ordinary
traffic. The [ACL conformal-routing paper](https://aclanthology.org/2026.acl-srw.70/)
suggests a way to choose thresholds around a defined error cost, subject to its
data and label assumptions. [LLMRouterBench](https://arxiv.org/abs/2601.07206)
supports keeping simple baselines in the comparison.

1. Change context and option order while keeping the correct answer the same.
   Save disagreements before averaging scores.
2. Define the cost of each wrong action. Choose refusal thresholds on separate
   calibration data, then test once on fresh groups of cases.
3. Compare local candidates on the same inputs after checking the exact model,
   resources, and license.
4. Measure complete accepted tasks, including all costs, before expanding automation.

The [research review](docs/research-review-2026-09.md) explains the test plans and
what would count as progress. Writing a plan doesn't mean we've run it or approved
new model calls.

## Use the workflows

- **[jev-integrate](jev-integrate/SKILL.md):** check a change against the current
  code, evidence, and regression checks.
- **[jev-hypothesize](jev-hypothesize/SKILL.md):** turn a claim about efficiency
  into a limited, repeatable comparison.

These are instructions for a coding agent. Installing them doesn't grant access,
a spending allowance, or permission to publish.

## Try the example

With an existing Python 3.11 or newer installation, run these from this directory:

```sh
python -B examples/demo.py
python -B -m unittest discover -s examples -v
```

The example runs a real check on disposable synthetic files. It considers five
proposed skips. One has current passing evidence; the other four have stale,
failed, mismatched, or missing evidence. The runner creates the check receipt in
code. A written claim or a loaded dictionary saying "the check passed" isn't enough.

Expected result: five proposed skips, one permitted skip, four rejected skips.
The cost example assumes 500 input tokens avoided and 600 spent on routing,
leaving **-100**. These are teaching values. No model or tokenizer runs, and the
example isn't a Jev performance benchmark.

For **jev-integrate**, accepting every `skip` would permit four unsupported skips.
For **jev-hypothesize**, the claim that routing reduces input fails once its own
cost is counted.

## Install and use

Copy either skill folder into the skills directory your agent host supports.
Keep `SKILL.md` and `references` together. For Codex, select `$jev-integrate` or
`$jev-hypothesize` after the host discovers it. Other hosts may need a different
import process; we haven't established automatic discovery across hosts.

Give the agent a concrete task:

> Use jev-integrate to review this routing change against our current code.
> Reproduce the reported failure before changing anything.

> Use jev-hypothesize to test whether routing saves total input tokens.
> Start with our existing results and allowance. Do not run paid calls.

Each skill includes a project-context template. Point it to the records your
project already uses. For Aldertrace, keep the existing protocol and domain memory.
For a new project, fill in what you know and mark the rest unknown. A missing
budget never means permission to spend.

## Limits and publication

These workflows came from Aldertrace's routing and recovery experiments. The
example checks evidence handling and cost arithmetic. It doesn't measure whether
the skills improve a coding model, make Jev safe in production, or lower task cost.

We used AI assistance for coding and review. Agreement between models isn't
independent human validation. Contributions should show the problem, how to
reproduce it, the expected result, and any new limitation.

Before every public update, check the exact content and history for secrets and
personal data. Follow the [publication checklist](PUBLICATION.md). A clean scan
doesn't prove there's nothing sensitive. For writing, follow [our style guide](STYLE.md).

MIT licensed; see [LICENSE](LICENSE). We don't claim affiliation with or endorsement
from Jev's authors. Mount Jeverest remains a future idea.
