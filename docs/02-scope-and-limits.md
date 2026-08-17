# Scope and limits

## What this method covers

Corporate sites, product and service sites, documentation sites, and B2B lead generation sites, roughly ten to a few hundred indexable pages, where you or your client can change the source code or the CMS templates.

## What it does not cover

Large e-commerce catalogs, where faceted navigation, parameter handling, and crawl budget dominate every other consideration. News publishing, where freshness and Top Stories eligibility follow different rules. Multi-location local SEO, where Google Business Profile matters more than anything on your own domain. App store optimization, which shares vocabulary with SEO and nothing else.

The principles hold in those contexts. The priority order does not.

## The two halves of SEO work

Splitting the work this way is useful because it tells you where an external vendor stops and where repository access starts to pay.

**Doable from outside the codebase.** Keyword research, competitor analysis, SERP inspection, backlink review, content briefs, technical diagnosis by crawling, and reporting. Any competent agency delivers these. They are covered in [04](04-phase1-technical-audit.md), [05](05-phase1b-onpage-content.md), and [09](09-data-layer.md).

**Requires commit access.** These are the reason this repository exists.

| Capability | Why an external vendor cannot do it |
| --- | --- |
| Fix at the template level and change every page at once | No deploy path. The recommendation becomes a ticket that waits |
| One change, one commit, one PR | Cannot control commit granularity, so effects stay entangled |
| Block regressions in CI | Cannot see the deploy that silently drops the meta tags six weeks later |
| Trace a rendering failure to its cause | Requires reading the router, the data fetching layer, and the build config |
| Pre-register a threshold and publish the misses | Publishing failures is commercially unattractive when you are selling retainers |
| Self-host the data layer and hand over raw exports | The proprietary dashboard is the product |
| Treat AI crawler policy as a business decision | Sits between legal, product, and marketing, and belongs to none of them |

## Limits that no method removes

Rankings cannot be guaranteed. Any vendor promising a position is either buying ads or lying.

Backlink data is a proprietary asset. Ahrefs, Majestic, and Semrush each maintain their own crawl of the web, and no open source project reproduces that index. [09-data-layer](09-data-layer.md) explains how to buy the data per request instead of renting a subscription, which lowers the cost but does not remove the dependency.

Search volume is likewise external. Google Keyword Planner gives bucketed figures and wants an active ads account. Third-party estimates are models, not counts.

Results take time. The fastest change described here, releasing an accidental `noindex`, still needs a recrawl before anything moves. See [08-phase4-measurement](08-phase4-measurement.md) for the working assumptions.

## What to say out loud before starting

Put this in the proposal, not in a footnote.

- No ranking guarantee, no traffic guarantee, no resistance to core updates
- No link acquisition outreach, since relationship building is not a deliverable a document can specify
- Measurement starts when the property is verified, so early results have no comparison period
- Phase 2 is a valid stopping point, and stopping there is not a failure of the engagement
