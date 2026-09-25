# How we write about this work

Write as the maintainer explaining what we tried, what happened, and what we
should do next. Be direct, practical, and willing to say that something didn't
work. Keep the business-review structure where it helps readers make a decision.

Use the [Google developer documentation style guide](https://developers.google.com/style)
as the main reference, especially its [voice and tone guidance](https://developers.google.com/style/tone).
Use short, clear instructions and consistent terms. These habits also fit the
purpose of [ASD-STE100](https://www.asd-ste100.org/about_STE.html), but we haven't
audited this project against its controlled vocabulary and writing rules. Don't
claim STE compliance.

- Start with the result or purpose. Explain the method after the reader knows why
  it matters. Prefer familiar words and active verbs.
- Use "we" for work done on this project and "you" for reader instructions.
  Contractions are fine. Don't invent a team, customer, personal story, or human
  review to make the text sound more personal.
- Explain a technical term when readers need it. Replace phrases such as
  "incremental safe coverage" with the actual result: "14 more eligible skips
  in this test." Avoid buzzwords, forced slang, and elaborate metaphors.
- Use tables for comparisons and numbered steps for procedures. Keep narrative
  paragraphs connected rather than turning every thought into a bullet.
- Put uncertainty next to the claim. Keep counts, denominators, model versions,
  costs, failed runs, and unknown measurements. Don't turn a rewrite into a
  stronger claim than the evidence supports.
- Keep the experimental notice prominent. A working demo, a passing check, a
  useful model, and a production system are different claims.
- Give clear instructions for actions that affect data, permissions, or spending.
  A friendlier tone must not weaken a requirement.
- Before publication, follow [the privacy checklist](PUBLICATION.md). Personal
  voice doesn't mean personal data. Use reviewed summaries and synthetic examples.

For example:

> We tried Jev on a small set of routing cases. It found more eligible skips than
> our rules did, but routing cost more input tokens than the assumed reading it
> avoided. That's useful to know, and it isn't a savings claim.

Read the draft aloud before publishing. If a sentence sounds like a report
template, say the same thing plainly. Preserve the evidence when you simplify it.
