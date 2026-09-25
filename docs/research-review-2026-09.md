# Research review and next experiments

Reviewed September 25, 2026. This records prospective work; no new inference was run for the review. Existing studies, allowances and evaluation assets retain their identities.

| Primary source | What changes our plan | Limit / disposition |
|---|---|---|
| [JevOut, September 24](https://arxiv.org/html/2609.30243v1) | Add plausible irrelevant context alongside option-order perturbations | Optimizer redirected 312/508 initially correct Jev decisions within 64 accepted evaluations per item; this is adversarial search, not deployment error. Automated answer-preservation checking merits independent review. Adopt the test question, not a universal failure-rate claim |
| [Conformal LLM Routing, ACL SRW July](https://aclanthology.org/2026.acl-srw.70.pdf) | Choose operating points against defined incremental error, with calibration/evaluation separation | Assumes exchangeability and suitable labels; guarantee is not per-request truth or subgroup safety. Both models wrong can count as no routing loss. Evaluate alongside absolute task failure |
| [Laya benchmarks](https://github.com/NandhaKishorM/laya/blob/main/BENCHMARKS.md) | Evaluate the exact task-tuned checkpoint, tokenizer and calibration configuration | Upstream reports typed accuracy 0.766 and ECE 0.213; base checkpoints fall below majority on that suite. Published Jev comparisons are not our paired run. Continue evaluation |
| [Verdict repository](https://github.com/Heman10x-NGU/openJev-verdict-2.0) | Separate the general Verdict checkpoint from specialized Verdict 2.0; pin engine and calibrator as well as weights | Correctness-head calibration and option-distribution calibration are different metrics. Do not relabel our existing caller observations as the newer model's results |
| [LLMRouterBench, January](https://arxiv.org/abs/2601.07206) | Include simple baselines and a fixed-model comparator | Broad benchmark reports several advanced/commercial routers failing to reliably beat a simple baseline. It does not decide our workload's winner |
| [JevRL, September technical report](https://jevrl.github.io/) | Retain direct Brier-training and majority baselines in future training research | One-seed synthetic pilot, no trained selective-abstention dataset; watch only |

## Next play: robustness and value before broader authority

### Question A — does context instability expose actionable risk?

Freeze fresh public/synthetic cases and family-disjoint splits. For each case, review neutral and misleading-but-answer-preserving additions independently from the target model. Compare current policy, single-order decisions, two-order averaging and an instability-abstention variant. Keep adversarial stress rates separate from naturalistic workload estimates. Known failures belong in regression fixtures, not a new held-out score.

Select any instability cutoff using calibration only. Report unsafe skips, unnecessary paid escalation, missed useful work, accepted coverage, per-family uncertainty, all-call latency/cost, and raw versus enforced choices. Passing requires correct enforcement regressions and a measured useful operating point; zero observed errors alone does not certify safety.

### Question B — does a calibrated gate improve the actual trade-off?

Define losses by action before observing results. Missing a valuable research item differs from spending time reviewing noise; an unsupported skip differs from unnecessary escalation. Compare current thresholds, deterministic rules and a simple classifier where applicable. Check the chosen method's threshold-selection assumptions. Report both relative routing loss and absolute accepted-task failure, including both-models-wrong cases. Keep weak-label, subgroup and temporal-shift limitations visible.

### Question C — which local candidate earns its resource cost?

Continue the existing offline adapter seam. Bind checkpoint, source, tokenizer, calibration, device and precision; test truncation, identity drift and resource refusal before inference. Compare identical fresh inputs against the existing policy. Measure cold load separately from warm request and end-to-end time. Use current permissions and an explicit execution envelope; publication of a plan is not permission to install weights or run models.

### Question D — is there practical value?

Continue the existing accepted-task pilot with a paired simplest-working baseline. Count task authoring, model calls, cache reads/writes, review, retries, failed runs, repair and operator time. Preserve negative results and prospective acceptance criteria. A candidate advances only when quality is retained and its practical cost or time improvement is supported within the measured scope.
