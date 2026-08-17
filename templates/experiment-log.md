# Experiment log

One row per bet. Hygiene commits are recorded at the bottom and are not evaluated individually.

Rows for the first six columns are filled in **before** the deploy. Filling them afterwards turns a test into a rationalization.

| ID | Change | Scope | Commit | Deploy date | Primary metric | Threshold | Window ends | Observed | Verdict | Confounders |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| seo-03 | self-referencing canonical on all templates | 72 pages | `abc1234` | 2026-09-01 | indexed page count | +10 pages | 2026-09-15 | | | none known |
| seo-07 | rewrite titles on the service templates | 18 pages | `def5678` | 2026-09-08 | impressions, service query set | +15% vs equivalent prior period | 2026-10-06 | | | quarter-end seasonality |

Verdict: improved, no change, worse.

## Filled example

| ID | Change | Scope | Commit | Deploy date | Primary metric | Threshold | Window ends | Observed | Verdict | Confounders |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| seo-11 | added FAQ structured data to 12 pages | 12 pages | `9ab3cd1` | 2026-06-02 | clicks, FAQ query set | +10% | 2026-06-30 | +1.4% | no change | none identified |

Notes on seo-11: the markup validated and Search Console reported it as detected. Click-through did not move measurably. Left in place because it is not harmful, and not repeated on the remaining templates, since the expected return no longer justifies the work.

Entries like this one are the point of the log.

## Hygiene commits

Shipped together, not measured individually.

| Commit | Deploy date | Contents |
| --- | --- | --- |
| `1234abc` | 2026-09-01 | 404 status for unmatched routes, `html lang`, removed stale `noindex` from 3 pages, fixed 2 broken canonicals |

## What was decided against

Work that was considered and not done, with the reason. Prevents the same proposal from returning every quarter.

| Proposal | Decided | Reason |
| --- | --- | --- |
| | | |
