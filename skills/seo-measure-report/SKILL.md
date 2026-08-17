---
name: seo-measure-report
description: Evaluate whether shipped SEO changes worked and write the report. Use when asked whether an SEO change had an effect, to analyze Search Console data after a deploy, or to produce a client-facing results report. Enforces pre-registered thresholds and refuses to claim causation.
---

# Measure and report

Decide whether each shipped change met the threshold that was written down before it shipped, then present the material without asserting causation.

## Step 1: check the experiment was set up

For each change, confirm four things exist from before the deploy: a single primary metric, a numeric threshold with a direction, an observation window with an end date, and a list of known confounders.

If any is missing, the change can be described but not evaluated. Say so in the report and do not construct a threshold retroactively, because by now you know which metric moved and would pick that one.

## Step 2: confirm the window has closed

Working assumptions from `docs/08-phase4-measurement.md`:

| Change | Window |
| --- | --- |
| Index control fix | 1 to 2 weeks |
| Title and description | 2 to 4 weeks |
| Structured data | 2 to 4 weeks |
| Content added or consolidated | 4 to 12 weeks |
| Performance | 4 to 8 weeks |

These are practice-derived, not published by any search engine. Reporting inside an open window is fine when labeled as interim, and never as a verdict.

If Crawl Stats shows no crawl activity for the affected URLs, this is a crawling problem rather than a failed experiment. Report it as such.

## Step 3: pull the data

From Search Console, for the defined query set or page set: impressions, clicks, click-through rate, and average position, for the observation window and for the equivalent prior period.

Use the equivalent prior period, not the immediately preceding one, unless you are certain there is no weekly or seasonal pattern. B2B traffic collapses on weekends and over holidays.

Calculate every comparison numerically rather than by eye, and keep the raw export alongside the report.

## Step 4: assign a verdict

Improved, no change, or worse. One of the three, against the pre-registered threshold, with no adjustment of the threshold at this stage.

Read position and click-through rate as independent. Higher CTR at an unchanged position is a success for a title change. Average position moving down because the site started ranking for new terms is not a decline.

For a "worse" verdict, investigate before recommending a revert. Falling impressions with rising qualified clicks is the intended result of removing pages that attracted the wrong readers.

## Step 5: write the report

Use `templates/client-report.md`. One row per change: what changed, the commit, the deploy date, the primary metric, the pre-registered threshold, the observed value, the verdict, and the confounders.

Include the "no change" rows. Their presence is what makes the rest of the report credible.

## Rules

Never write that a change caused a result. Present the commit, the date, the threshold, the observation, and the confounders, and let the reader draw the line.

Name confounders even when they weaken the story: other deploys in the window, seasonality, a campaign, a reported algorithm update, a competitor's change.

Do not report a vendor authority metric or a checker score as a result.

Do not extrapolate. Two good weeks are two good weeks, not an annual projection.

When the data is too sparse to conclude anything, which is normal on small sites, say that and give the date when there will be enough.
