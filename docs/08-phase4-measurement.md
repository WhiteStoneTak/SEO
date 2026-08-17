# Phase 4: measurement

## Declare the threshold before the deploy

Written before shipping, a threshold is a test. Written afterwards, it is a rationalization, because by then you know which metric moved and will choose that one.

For each bet, fix four things in advance and commit them to the repository:

1. **One primary metric.** Total impressions for a named query set is usually the right choice for a title or content change. Indexed page count works for index control fixes. Pick one, not three.
2. **The threshold.** A number and a direction, for example "+15% or better against the equivalent prior period".
3. **The observation window.** A date, computed from the deploy date.
4. **Known confounders.** Seasonality, other deploys in the window, campaigns, competitor moves, reported algorithm updates.

## Observation windows

These are working assumptions from practice. No search engine publishes such figures, and they vary with site size, crawl frequency, and authority. Calibrate against your own data and update the table for your own use.

| Change | Assumed window |
| --- | --- |
| Index control fix, such as removing `noindex` | 1 to 2 weeks |
| Title and meta description changes | 2 to 4 weeks |
| Structured data | 2 to 4 weeks |
| Content added or consolidated | 4 to 12 weeks |
| Performance improvement | 4 to 8 weeks, limited by field data accumulation |

If a fix has produced no crawl activity at all by the end of the window, that is a crawling problem, not a failed experiment. Check the Crawl Stats report before concluding anything.

## Reading Search Console honestly

Compare against the equivalent prior period, not the immediately preceding one, unless you are certain there is no weekly or seasonal pattern. B2B sites collapse on weekends and again over holidays, and comparing a holiday week to a working week produces a story that is entirely an artifact.

Average position is a weighted average across every query and every impression. It moves when a page starts ranking at position 40 for a new query, which looks like a decline and is not one. Watch impressions and clicks for the specific query set instead.

Position and click-through rate move independently. A title rewrite that raises CTR at an unchanged position is a success, and a report focused only on position will call it a failure.

## Three verdicts

Every experiment gets one of three, entered in [templates/experiment-log.md](../templates/experiment-log.md).

**Improved.** Threshold met or exceeded. Record the number and, in the same row, the confounders that could also explain it.

**No change.** Did not reach the threshold. Record it. This is the entry that makes the log worth reading, and the one most vendors omit.

**Worse.** Investigate before reverting. Sometimes a drop in impressions accompanies a rise in qualified clicks, which is the intended outcome of removing pages that attracted the wrong readers.

## Reporting

Use [templates/client-report.md](../templates/client-report.md). One row per change containing what changed, the commit, the deploy date, the metric, the pre-registered threshold, the observed number, the verdict, and the confounders.

Do not write "this change caused that result". Present the elements and let the reader draw the line themselves. Anyone with repository access can check every element of that report, and that verifiability is the thing being sold.
