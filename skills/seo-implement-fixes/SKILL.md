---
name: seo-implement-fixes
description: Implement SEO findings in a codebase as isolated commits that can be measured afterwards. Use when asked to fix SEO issues, add missing meta tags or canonicals, fix 404 handling, or ship the changes from an SEO audit. Enforces one change per commit and template-level fixes.
---

# Implement SEO fixes

Turn a prioritized findings list into commits. Each commit must remain attributable to a result weeks later.

## Before touching code

Confirm the findings list has been prioritized and split into hygiene and bets. If it has not, do that first, using `docs/06-phase2-prioritization.md`.

Read the codebase before changing it. Identify the base layout, the head management API the framework provides, the router, and the config that controls 404 handling. Fixing the template beats fixing pages, and finding the template is the part that takes the time.

Work on a branch. Never commit directly to the default branch.

## Commit discipline

**Bets get one commit each.** One finding, one commit, one pull request.

```
seo-03: emit self-referencing canonical on all page templates

Every page rendered without a canonical link. Adds an absolute
self-referencing canonical in the base layout.

Affected: 72 indexable pages
Finding: seo-03
```

**Hygiene ships as one commit** listing its contents. It will not be measured individually, so splitting it buys nothing.

Never include unrelated changes. An unrelated refactor in the same commit destroys the deploy date's meaning and the measurement with it. If you spot an unrelated bug, write it down and keep going.

## Common implementations

**Missing metadata.** Use the framework's head API in the base layout, with per-page overrides. Do not inject tags manually into markup; manual injection survives until the next framework upgrade.

**Catch-all returning 200.** Fix in the router so unmatched paths return a real 404 status. Check the host configuration too, since static hosting SPA fallback settings cause this independently of application code.

**Canonical.** Absolute URL, matching protocol and host, one per page, self-referencing by default.

**hreflang.** Every language version references every other and itself. Non-reciprocal annotations are ignored.

**Language routing.** Real content at a stable URL per language. Server-side negotiation is acceptable for the first visit; client-side redirection as the only path is not.

**Structured data.** `Organization` and `BreadcrumbList` first. Validate before committing. Comprehensive type coverage is a later project.

**Redirects.** 301 to the specific successor URL, never to the homepage. 410 when nothing succeeds it. Check for chains after every addition.

## After the deploy

Verify in production, in the raw response rather than in the local build:

```bash
curl -sL https://example.com/ | grep -i "<link rel=\"canonical\""
curl -sI https://example.com/definitely-not-a-real-page-xyz123 | head -1
```

Record the deploy date in `templates/experiment-log.md` at the time of deploy, not from memory later. The observation window starts here, not at merge.

For bets, confirm the pre-registered metric and threshold were written down before the deploy. If they were not, the change can still ship, and it can no longer be reported as an experiment. Say that plainly rather than inventing a threshold afterwards.

Request indexing for one representative URL through Search Console URL Inspection. It guarantees nothing and removes one question from the later analysis.

## Rules

Do not ship SEO changes and a redesign in the same window if either will be reported on.

Do not add a tracking script, an analytics vendor, or a third-party widget as part of an SEO fix. Those are separate decisions with separate privacy consequences.

If a finding turns out to be wrong once you can see the code, say so and remove it from the list. Audits produce false positives, and shipping a fix for a problem that does not exist is worse than the original finding.
