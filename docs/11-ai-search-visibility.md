# AI search visibility

Facts checked on 2026-08-17 against Google's documentation. This area moves quickly, so re-check before quoting.

## What Google says

Google states there are no additional requirements and no special optimizations for appearing in AI Overviews or AI Mode. A page needs to be indexed and eligible to appear in Search with a snippet. Google also states explicitly that no new machine-readable files, AI text files, or markup are required ([Google, AI features and your website](https://developers.google.com/search/docs/appearance/ai-features)).

Two consequences worth keeping in mind. Any product sold as "AI Overview optimization markup" is selling something Google says is unnecessary. And traffic from these features is included in the normal Search Console Performance report under the web search type, which means there is no separate AI dashboard to check.

The controls that limit appearance are the existing snippet controls: `nosnippet`, `data-nosnippet`, `max-snippet`, and `noindex`. Using them to stay out of AI answers also reduces or removes normal snippets, so this is not a free opt-out.

## What actually helps

Since eligibility is ordinary eligibility, the work is ordinary work, weighted toward extraction.

Answer the question in plain text near the top of the page, in a sentence that survives being lifted out of its surroundings. Content that only makes sense after three paragraphs of context is hard to cite.

Keep facts in text rather than in images or in a diagram, since alt text carries less than a sentence does.

State the things a reader needs and pages routinely omit: prices, coverage areas, supported versions, requirements, dates. These are frequently the substance of the question being asked.

Attribute claims to sources, and keep an update date visible. Both help a human evaluate the page, and both give a model something to anchor to.

## Measuring it

There is no equivalent of Search Console for third-party assistants, which means measurement here is manual and small-sample. Do it anyway, because the alternative is having no idea.

Define ten to twenty questions a real buyer would ask. Run them against the assistants that matter for the business. Record, per question and per assistant, whether the site was cited, which page, and which competitor appeared instead. Repeat monthly with the same questions.

Keep the sample honest. Answers vary between runs, personalization affects results, and a single check proves nothing. Report it as a repeated observation with the run dates attached, never as a metric.

Server logs are the other source. Requests from documented AI crawler user agents show what is being fetched and how often, and referral traffic from assistant domains, where it exists, appears in ordinary analytics.

## Crawler policy is a business decision

Most sites inherit their AI crawler rules from a CDN default and never revisit them. Blocking `GPTBot`, `ClaudeBot`, `CCBot`, `Google-Extended`, and similar agents is a defensible choice, and so is allowing them. Making the choice by accident is not.

Google states that `Google-Extended` does not affect a site's inclusion in Google Search and is not used as a ranking signal ([Google, crawlers](https://developers.google.com/search/docs/crawling-indexing/google-common-crawlers)). It governs training and grounding in Gemini and Vertex AI. So blocking it does not cost search visibility, and it does affect other surfaces.

The question to put to the client, in one sentence: do you want your content used to answer questions in assistants, given that this may bring mentions and referrals, and given that it also means your content trains or grounds systems you do not control?

Reasonable answers differ by business. A consultancy whose product is its expertise may want maximum citation. A publisher whose product is the article itself may not. Write down which was chosen, by whom, and on what date, then make `robots.txt` match. That record is worth more than the setting, because it is what stops the same discussion from restarting every quarter.

## What to avoid

Do not build a separate page set for AI consumption. It is content duplication with an unfalsifiable rationale.

Do not report "AI visibility scores" from third-party tools as if they were measurements. Nobody outside the assistant vendors has the sampling frame required to produce one.

Do not promise citation. It is less predictable than ranking, and ranking already cannot be promised.
