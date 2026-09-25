# Research worth testing next

Reviewed September 25, 2026. This is a plan for further experiments. We made no
new model calls for this review and haven't changed the existing studies,
budgets, or evaluation data.

| Source | What we'd take from it | What it doesn't establish |
|---|---|---|
| [JevOut, September 24](https://arxiv.org/html/2609.30243v1) | Test plausible but irrelevant context as well as changed option order | The optimizer redirected 312/508 initially correct decisions within 64 accepted evaluations per item. That's an attack search, not an ordinary-traffic error rate. Its automated check that the correct answer stayed the same needs independent review |
| [Conformal LLM Routing, ACL SRW July](https://aclanthology.org/2026.acl-srw.70.pdf) | Choose thresholds around a defined error cost. Keep calibration separate from evaluation | It assumes suitable labels and exchangeable data: roughly, calibration and evaluation examples must come from the same distribution. It doesn't guarantee each answer or every subgroup is safe. If both models are wrong, routing loss can still be zero |
| [Laya benchmarks](https://github.com/NandhaKishorM/laya/blob/main/BENCHMARKS.md) | Test the exact model version, tokenizer, and calibration setup | The authors report typed accuracy 0.766 and expected calibration error (ECE) 0.213. Base models score below the majority baseline on that suite. Their Jev comparison isn't our own paired test |
| [Verdict repository](https://github.com/Heman10x-NGU/openJev-verdict-2.0) | Keep general Verdict and specialized Verdict 2.0 results separate. Record engine, calibrator, and weights | Calibration of a correctness score differs from calibration of the option scores. Our existing caller results don't become results for a newer model |
| [LLMRouterBench, January](https://arxiv.org/abs/2601.07206) | Include simple baselines and a comparison that always uses the same model | Several advanced or commercial routers didn't reliably beat a simple baseline in that benchmark. It doesn't tell us which option wins on our workload |
| [JevRL, September technical report](https://jevrl.github.io/) | Keep direct Brier-score training and majority baselines in any future training comparison | This is a synthetic pilot with one seed and no trained selective-abstention dataset. Worth watching; not a reason to adopt it yet |

## Does changing the context change the decision?

Create fresh public or synthetic cases. Keep related case families in separate
development, calibration, and test groups. Review neutral and misleading additions
independently of the model being tested, checking that the correct answer stays
the same.

Compare the current policy, one option order, two-order averaging, and a version
that refuses when the answers change too much. Keep attack-test results separate
from estimates of normal use. Known failures belong in regression tests, not in
a supposedly fresh test score.

Choose any disagreement threshold using calibration data only. Report prohibited
skips, unnecessary paid calls, missed useful work, accepted decisions, uncertainty
by case family, and the time and cost of every call. Show recommendations and
permitted actions separately. We need passing enforcement checks and a useful
measured trade-off. Zero observed errors alone won't establish safety.

## Can a refusal threshold improve the trade-off?

Define the cost of each wrong action before seeing results. Missing a useful
research item has a different cost from reviewing an irrelevant one. Skipping a
required check differs from paying for work we didn't need.

Compare the existing thresholds, fixed rules, and a simple classifier where one
fits. Check the assumptions behind threshold selection. Count both the extra
errors caused by routing and failed tasks overall, including cases where both
models are wrong. Keep uncertain labels, subgroup differences, and changes over
time visible in the results.

## Which local model is worth its resource cost?

Continue with the existing offline adapter. Record the exact model, source,
tokenizer, calibration, device, and precision. Before inference, test cut-off
inputs, changed model identity, and refusal when resources aren't available.

Use identical fresh inputs for the candidate and current policy. Measure initial
loading, warm requests, and complete-task time separately. Any live run needs
the existing permissions and explicit resource and spending limits. This plan
doesn't authorize installing weights or running models.

## Does it help us finish useful work?

Continue the accepted-task pilot with a paired comparison against the simplest
method that works. Count task authoring, model calls, cached reads and writes,
review, retries, failures, repair, and operator time.

Set acceptance criteria before the run and keep negative results. Move a candidate
forward only when it retains quality and shows a cost or time benefit within the
scope we actually measured.
