---
name: seo-ai-visibility
description: Check and improve whether a site gets cited in AI assistant answers, and review the site's AI crawler policy. Use when asked about AI Overviews, ChatGPT or Perplexity citations, GEO or AEO, llms.txt, or whether to block AI crawlers. Treats crawler policy as a business decision to be recorded, not a default to inherit.
---

# AI search visibility

Two deliverables: a repeatable citation check, and a recorded decision about crawler policy.

## Ground the user first

Google states there are no additional requirements and no special optimization for appearing in AI Overviews or AI Mode, that a page needs to be indexed and eligible to show with a snippet, and that no new machine-readable files, AI text files, or markup are needed ([Google, AI features and your website](https://developers.google.com/search/docs/appearance/ai-features)).

So if the user is asking which markup to add, the answer is that Google says none is required, and the work is ordinary indexability plus extractable writing. Say this before doing anything else, since it changes what they are asking for.

Verify this against current documentation before repeating it. This area changes.

## Step 1: check eligibility

Confirm the pages in question are indexed and can show a snippet. Check for `noindex`, `nosnippet`, `data-nosnippet`, and a restrictive `max-snippet`. A page carrying any of these is excluded from the feature by its own configuration, and no writing change will fix that.

## Step 2: the citation check

Define ten to twenty questions a real buyer would ask, in the buyer's words. Run each against the assistants the business cares about. Record per question and per assistant: cited or not, which page, and which competitor appeared instead.

Report it as a dated observation with the run count, never as a score. Answers vary between runs and are affected by personalization, so a single check proves nothing. Repeat monthly with the same questions, and change the question set only deliberately, because changing it resets the comparison.

## Step 3: server-side evidence

Check access logs for documented AI crawler user agents: which paths are fetched, how often, and whether anything returns errors. Check analytics for referrals from assistant domains where they exist.

This is first-party evidence and it beats any third-party visibility estimate.

## Step 4: content changes that help

Answer the question in plain text near the top, in a sentence that survives being lifted out of context. Keep facts in text rather than in images. State prices, coverage, requirements, versions, and dates, which are usually the substance of the question and are routinely omitted. Attribute claims and show an update date.

Do not build a parallel page set for AI consumption. It is duplication with an unfalsifiable rationale.

## Step 5: crawler policy as a recorded decision

Read the `robots.txt` actually being served, in full. CDN-managed blocks are common and are frequently inherited rather than chosen.

Google states that `Google-Extended` does not affect inclusion in Google Search and is not a ranking signal ([Google, crawlers](https://developers.google.com/search/docs/crawling-indexing/google-common-crawlers)); it governs training and grounding in Gemini and Vertex AI. Blocking it therefore does not cost search visibility.

Put one question to the decision maker: do you want your content used to answer questions in assistants, accepting the mentions and referrals that may bring, and accepting that it also means your content grounds or trains systems you do not control?

Both answers are defensible. Record which was chosen, by whom, and on what date, then make `robots.txt` match. The record is the deliverable, because it prevents the same discussion from restarting every quarter.

## Rules

Do not promise citation. It is less predictable than ranking, which already cannot be promised.

Do not report a third-party "AI visibility score" as a measurement. Nobody outside the assistant vendors has the sampling frame to produce one.

Before recommending a new file that some system supposedly requires, find the operator who states they consume it. If the user adds it anyway, log it as a bet with a threshold like any other change.
