# Antipatterns

Practices that get sold, invoiced, and reported on, and that do not survive examination. Recognizing them is useful in two directions: it stops you from buying them, and it tells you what a client's previous vendor left behind.

## The composite score

A hundred-point grade from an SEO checker, or a vendor authority metric such as Domain Authority or Domain Rating. No search engine consumes these numbers. They are vendor models, useful at best as a rough relative comparison, and they move when you fill in a meta description.

Reporting a score increase as a result substitutes a number the client cannot interpret for work they could have understood.

## Keyword density and its descendants

Repeating the target phrase a set number of times, adding a keyword list to the footer, stuffing alt text with phrases nobody would say aloud. This has not worked in a long time, and the pages carrying it are usually worse for readers, which is the part that does have an effect.

## Buying links in bulk

Directory packages, paid guest post networks, and comment links violate Google's spam policies and have been devalued repeatedly. The measurable outcome is an invoice.

Links that matter come from someone deciding your page was worth citing. That is a communications and product problem, and no document can turn it into a checklist.

## Publishing volume as a strategy

"Ten articles a month" is a production schedule, not a plan. Ten pages nobody searches for produce ten pages of maintenance and a thinner site overall. Decide which query has no page ([05](05-phase1b-onpage-content.md)) and write that page.

## Expanding every thin page

The instinct that short pages need more words is wrong. Consolidation, `noindex`, and deletion are all faster than writing and frequently better. Adding 800 words to a page that already answered its question makes it worse for the reader.

## Optimizing performance first

Performance work is measurable, satisfying, and safe, which makes it attractive when the actual problem is that the pages are not indexed. Google states that Core Web Vitals are used by its ranking systems and that good scores do not guarantee ranking ([Google, page experience](https://developers.google.com/search/docs/appearance/page-experience)). If LCP is already under 2.5 seconds in field data, the remaining headroom is small. Check index coverage before opening a profiler.

## Shipping everything on one day

Fifteen changes deployed together produce one uninterpretable graph. If nothing is being claimed afterwards, this is fine and fast. If a result will be reported, isolate the bets ([06](06-phase2-prioritization.md)).

## Reporting position as the headline

Average position in Search Console is weighted across all queries and impressions. Ranking newly at position 40 for ten new queries lowers it, which is progress that reads as decline. Report impressions and clicks for a defined query set.

## Redirecting everything to the homepage

The standard move during a migration, and it is treated as a soft 404 rather than as a redirect. Map each old URL to its closest successor, and return 410 where none exists. See [checklists/migration](../checklists/migration.md).

## Blocking crawlers by accident

CDN defaults and copied `robots.txt` files routinely block AI crawlers, staging paths, or, occasionally, everything. Read the file that is actually being served, and record who chose the current policy and when ([11](11-ai-search-visibility.md)).

## Claiming causation

"Our work tripled organic traffic" requires ruling out seasonality, competitor changes, algorithm updates, and every other change shipped in the same period. Almost nobody does that, and reporting the commit, the date, the threshold, and the graph is both more honest and harder for a competitor to copy.

## New-file cargo cults

Every few months a new file appears that a site is supposedly required to publish for AI systems. Google's position is that no new machine-readable files, AI text files, or markup are needed to appear in its AI features ([Google, AI features and your website](https://developers.google.com/search/docs/appearance/ai-features)). Before adding one, find the operator who states they consume it, and if you add it anyway, record it as a bet with a threshold like anything else.
