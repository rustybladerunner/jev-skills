# What we've tried and what happened

Reviewed September 25, 2026. These are experimental results, not audited business
results. The first study has public evidence you can replay. The others are our
summaries of private run records and aren't independently reproduced here. We
haven't included private project names, work orders, prompts, account details,
or raw conversations in these summaries.

## 1. Jev found more cases where a prerequisite could be skipped

The [Aldertrace v002 study](https://github.com/rustybladerunner/aldertrace/blob/main/experiments/v002/REPORT.md)
used 80 held-out synthetic cases: 40 eligible skips and 40 prohibited skips. Code
checked the evidence before allowing any skip. With Jev's recommendations, it
allowed 34 eligible skips. Fixed rules and the chat model each allowed 20. All
three recorded zero prohibited skips on these cases.

Those 14 additional eligible skips are the useful result. The limits matter:
labels are provisional, there are few independent case families, and Jev's input
accounting estimate was -12,240 tokens saved. Routing cost more input than the
assumed reading avoided. We haven't shown lower cost for a complete task.

The model's recommendation and the permitted action are separate. An agent saying
a check passed doesn't replace a result recorded by the check runner.

## 2. Live routing worked; the downstream draft didn't

On September 21, three integration checks used `typesafe/jev-1.13-20260917` and
selected the expected chat, draft-only, and clarification routes. Request times
were 503, 404, and 444 ms. Reported Jev cost totaled $0.000050988. Replaying a
request with the same ID made no new call. The pilot cap blocked a fourth new request.

The clarification route avoided a downstream chat call in that case. The draft-only
route didn't authorize execution. But the drafting model then failed to return a
usable draft. So the routing check passed while the complete task failed.

Three selected cases check the integration; they don't measure general accuracy.
Source: our summary of a private integration record.

## 3. Research ranking showed promise, but missed useful items

On September 24, we compared decisions on 146 public posts with one agent's
labels: 42 keep and 104 drop. Jev agreed on 109/146. Its ranking AUC was 0.78,
a measure of how well the scores separated the two groups. At threshold 0.5,
it found 20/42 keeps, and 20/35 of its keep decisions matched the labels.

No tested threshold reached the prespecified 85% agreement target. Some disagreement
came from a mismatch between the written criterion and the digest's relevance to
the project. Those agent-written labels aren't a definitive answer key.

That supports testing ranking and annotation. It doesn't support throwing items
away automatically. A local Verdict caller abstained on 113/146 keep decisions.
Of its 33 committed outputs, 18 agreed. We didn't establish a better local replacement.

Source: our summary of a private operational study. The posts were public; the
maintainer's selection history remains private.

## 4. Changing option order found a problem that repeat runs missed

We tried four cyclic option orders on 120 items. Six items changed their top choice,
all between `skip` and `frontier_author`. Repeating the same order agreed on 120/120.
Repeating a test was therefore not enough to find this problem.

We responded by averaging two orders and refusing or requesting review when the
averaged P(skip) reached 0.30. That's a local rule based on these observations.
It isn't a calibrated probability of being correct or a production safety guarantee.
Both original score distributions must be kept because averaging can hide disagreement.

Changes to context and fresh quality tests are still open work. Source: our
summary of private order-test records. The 600 calls include rotations and repeats,
not 600 different items.

## 5. Reviewed code changes passed, but savings are still unproved

A separate coding worker proposed limited patches. A deterministic executor
applied them only after review of the exact work order and acceptance checks.
Jev didn't generate the patches. Earlier weak proposals failed checks and stayed
in the record as failures.

In a capped test-generation rerun, the accepted worker route used 11,099 new
frontier-model tokens versus 16,970 for a manual route. It made 6 frontier calls
versus 3 and read 3,389,319 cached tokens versus 1,330,136. An illustrative pricing
calculation put its cost around 2.1 times the manual route.

This was a rerun of a task we'd already seen, informed by development work. It
wasn't a fresh randomized evaluation. Earlier attempts and development costs also
prevent us from presenting that selected run as savings for the whole effort.

A later dispatcher-authored task passed on one cheap-model proposal. It needed no
frontier drafting calls and two frontier review/apply calls totaling 4,698 new
tokens. We didn't measure task-authoring cost or run a paired manual comparison.

These trials show that the reviewed editing process can work. They don't show
lower total cost or establish how much Jev contributed to the result.

## What we'll report next time

Record the exact model and artifact versions, number of unique cases, label
source and review status, proposed and permitted actions, missing or invalid
results, and accepted work. Count operator time, startup and warm-request time,
retries, and every usage category. Keep estimates separate from provider reports
and invoices.

Publish only evidence checked for secrets and personal data. Keep confidential
originals private. A synthetic test, an integration check, an operational trial,
and a held-out model evaluation answer different questions; say which one ran.
