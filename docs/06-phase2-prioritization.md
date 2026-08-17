# Phase 2: prioritization

Estimated time: one hour.

You now hold a list of problems and no order. This phase produces the order, and the order is the deliverable. An engagement can legitimately end here.

## A starting formula

```
score = severity x (0.4 + 0.6 x reach) / cost
```

| Term | Values |
| --- | --- |
| severity | critical 10, high 6, medium 3, low 1 |
| cost | S 1, M 3, L 8 |
| reach | affected pages / indexable pages, between 0 and 1 |

The `0.4 + 0.6 x reach` term keeps a critical single-page problem from being buried by a trivial site-wide one, while still rewarding fixes that apply everywhere.

This formula is not correct in any deep sense. Its job is to fix the starting point of the argument as a number, so that disagreements become explicit. Keep every input value in the findings file. When someone disputes the order, change a weight and recompute rather than debating adjectives.

## Overrides that beat the formula

Apply these after computing, and write down the reason whenever you override.

| Situation | Decision |
| --- | --- |
| A page meant to be public carries `noindex`, a wrong canonical, or a `Disallow` | Do this first, ahead of everything. The page is not ranking badly, it is absent |
| The fix is one template and covers many pages | Move it up. Highest return per hour available in this work |
| LCP is already under 2.5s in field data | Move performance down. Little headroom left |
| Many thin pages | Consolidate, `noindex`, or delete before writing anything new |
| Structured data missing entirely | Ship `Organization` and `BreadcrumbList` only. Comprehensive coverage is a later project |
| The client's revenue depends on one page | That page's issues outrank their formula position |
| A replatform is scheduled within a quarter | Fix only what survives the migration. See [checklists/migration](../checklists/migration.md) |
| The fix requires a team that is not available | Rank it honestly and mark it blocked. Do not silently drop it |

## Separate hygiene from bets

Sort the ordered list into two buckets, because they are shipped and measured differently.

**Hygiene.** Defects with no plausible upside to leaving them in place. Broken canonicals, soft 404s, invalid structured data, missing `lang`, orphaned staging URLs. Ship them together in one commit. Do not attempt to measure them individually, since attributing a result to one of fifteen simultaneous fixes is not possible.

**Bets.** Changes where a reasonable person could expect either outcome. A title rewrite across a template, a content consolidation, a navigation restructure. One commit each, one pre-registered threshold each, one observation window each. These are the rows that end up in the experiment log.

Most audits produce many hygiene items and two or three bets. That ratio is normal and worth stating to the client, because it explains why the report is long and the experiment log is short.

## What to hand over

A single ordered table: rank, finding, affected pages, severity, cost, computed score, any override and its reason, and the bucket. Plus the sentence describing what happens if nothing is done at all, which is the only honest baseline for a go or no-go decision.
