# Case studies and evidence boundaries

Review date: September 25, 2026. We separate published reproducible evidence from maintainer-reported operational aggregates. Private project names, work orders, prompts, account details and raw session transcripts are not bundled. These summaries report engineering observations, not independently audited commercial results.

## 1. Jev added semantic coverage in a prerequisite-routing study

The [Aldertrace v002 report](https://github.com/rustybladerunner/aldertrace/blob/main/experiments/v002/REPORT.md) covers 80 held-out synthetic cases, including 40 eligible and 40 prohibited skips. Jev with deterministic evidence enforcement allowed 34 eligible skips, compared with 20 for deterministic rules and 20 for the chat arm. All three enforced policies recorded zero prohibited skips on these fixtures. Jev's 14 additional eligible skips are the useful result.

The caveats matter: labels remain provisional, there are few independent families, and the observable input proxy was -12,240 for Jev. There is no demonstrated end-to-end saving. Raw recommendations and permitted actions are separate; an agent's statement that a check passed is not runner evidence.

## 2. A live routing integration honored its boundaries

A September 21 three-case integration check resolved to `typesafe/jev-1.13-20260917` and matched the expected chat, draft-only and clarification routes. Request latencies were 503, 404 and 444 ms; reported Jev cost totaled $0.000050988. Stable-ID replay made no new call, and a fourth new request was blocked by the pilot cap.

Clarification avoided downstream chat inference in that case. Draft-only did not authorize execution. The subsequent drafting model failed to return a usable draft, so the successful Jev routing check did not establish successful task completion. Three selected cases are a smoke test, not an accuracy benchmark. Source class: maintainer-reported private integration receipt.

## 3. Research triage helped rank material, but could miss valuable items

On September 24, 146 public posts were compared against one agent's digest labels: 42 keep and 104 drop. Jev agreed on 109/146 and produced ranking AUC 0.78. At threshold 0.5 it recovered 20/42 keeps, with precision 20/35. No tested threshold met the prespecified 85% agreement bar. Some disagreement reflected a mismatch between the written criterion and the digest's project relevance.

The useful outcome was a bounded ranking/annotation role and evidence against automatic discard. A local Verdict caller abstained on 113/146 keep decisions; of its 33 committed outputs, 18 agreed. This was not a win for a local replacement. Source class: maintainer-reported operational study; labels are not gold and public posts do not make personal selection history public.

## 4. Order testing found a refusal boundary that repeats missed

Four cyclic option orders across 120 items changed the top choice on 6 items. Every change crossed `skip` and `frontier_author`. An identical-order repeat agreed on 120/120, so repeatability alone missed the weakness. The operational response was two-order averaging and refusal/review when averaged P(skip) reached 0.30.

That threshold is a local empirical rule, not calibrated correctness or a production guarantee. Preserve both raw distributions: averaging can hide disagreement. Fresh context-perturbation and quality evaluation remain open. Source class: maintainer-reported order-test receipts; 600 calls include rotations and repeats, not 600 unique items.

## 5. Reviewed worker outputs succeeded; Jev ROI remains unproved

A separate coding worker proposed bounded patches, which a deterministic executor applied only after exact-order review and acceptance checks. Jev did not generate these patches. Earlier weak proposals failed checks and were retained as failures.

In a capped test-generation rerun, the accepted worker route used 11,099 new frontier tokens versus 16,970 for a manual route. It took 6 frontier calls versus 3, and 3,389,319 cache-read tokens versus 1,330,136. An illustrative relative-price calculation put cost around 2.1 times the manual route. This was a development-informed rerun of a previously seen task, not a fresh randomized evaluation. Earlier attempts and worker-development costs prevent treating the selected run as campaign savings.

A later dispatcher-authored task passed on one cheap-model proposal. It used no frontier drafting calls and two frontier review/apply calls totaling 4,698 new tokens. Task-authoring cost was unmeasured and no paired manual run existed. Successful bounded execution is supported; lower total cost and Jev's incremental contribution are not.

## Reporting contract

For future case studies record the exact model and artifact identities, unique cases, labels and review status, raw/enforced choices, invalid or missing outcomes, accepted deliverables, operator work, cold/warm timing, retries and all usage categories. Distinguish estimated cost from provider reports and invoices. Publish screened evidence only; confidential originals remain private. A synthetic fixture, transport smoke, operational observation and held-out model evaluation are different evidence classes.
