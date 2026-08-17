---
name: seo-keyword-to-page
description: Map the queries a business cares about to the pages that should win them, and identify gaps, cannibalization, and intent mismatches. Use when asked which content to write, why a page is not ranking for its target term, or how to plan a content roadmap. Works with or without an OpenSEO MCP connection for volume data.
---

# Query to page mapping

Produce one table: for each target query, the single page that should win it, and the verdict on whether that page exists and is suitable.

## Step 1: build the query set

Sources, in order of usefulness:

1. Search Console, the queries already producing impressions. First-party and free
2. What the client says customers ask, in the customer's words rather than the company's
3. Terms competitors rank for
4. Keyword expansion from an OpenSEO MCP connection, if one is configured

Terminology mismatch is common and worth checking explicitly. Organizations describe their product in internal vocabulary while buyers search in ordinary words, and the gap between the two is often the whole problem.

Keep the set small enough to act on. Twenty to fifty queries is a working roadmap; three hundred is a spreadsheet nobody opens.

## Step 2: attach demand and difficulty

With OpenSEO MCP available, pull volume and competition for the set in one batch. Pull once, cache it, and reuse it, since every request costs money.

Without it, order by judgement and say so in the output. Volume estimates are modeled numbers, never traffic forecasts, and an unavailable estimate is less harmful than a fabricated one.

## Step 3: find the page that should win

For each query, search it and record the current top results and the format they take. If the top ten are all comparison tables, the query wants a comparison table.

Then locate the client's page for that intent, whether or not it currently ranks. Assign one verdict per query:

| Verdict | Meaning | Action |
| --- | --- | --- |
| Covered | One suitable page exists | Improve title, description, internal links |
| Gap | No page addresses this intent | Write one. Highest value and highest cost |
| Cannibalized | Two or more pages compete | Consolidate into one, redirect the others |
| Mismatch | A page exists, aimed at the wrong intent | Edit rather than add |
| Out of reach | Results are dominated by sources this site cannot displace | Drop from the target set and say why |

Marking queries out of reach matters. A roadmap that includes unwinnable terms wastes the budget that the winnable ones needed.

## Step 4: check what the site already earns

Pull Search Console queries and find pages ranking at positions 5 to 20 with meaningful impressions and low click-through. These are usually cheaper wins than anything new, since the page already has standing and needs a better title, a clearer opening, or internal links.

## Step 5: output

One row per query: query, estimated volume with its source, current best page, current position if known, verdict, action, and cost.

Then the ordered shortlist of what to do first, with reasoning. Gaps sort by demand divided by cost to produce. Cannibalization sorts high because consolidation is cheap and immediate.

## Rules

Never present modeled search volume as expected traffic.

When a query set was supplied by the client, keep their terms and add yours as a separate group, so the difference between what they assumed and what the data shows stays visible.

Content briefs for gap rows use the five-line format in `docs/05-phase1b-onpage-content.md`. Leaving a line blank means the page is not ready to write.
