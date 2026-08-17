# Principles

Five rules that decide what to do when the situation is ambiguous. Everything else in this repository follows from them.

## 1. Measurement comes before the fix

Search Console data starts accumulating on the day the property is verified, and not one day earlier. A site that has run for three years without a verified property has three years of history that can never be recovered.

So the first task of any engagement is verification, not repair. If the client cannot grant access yet, write down that constraint with the date, then decide whether to proceed knowing that the work will be unprovable.

The temptation to fix the obvious problem first is strong, especially when the obvious problem is embarrassing. Resist it for as long as it takes to verify the property, which is usually under an hour.

## 2. A composite score is not a deliverable

Domain Authority, Domain Rating, and the hundred-point grades produced by online SEO checkers are vendor estimates. No search engine publishes such a number, and none of them consumes one. Most of these scores also rise when you fill in a meta description, which makes them trivially easy to move without changing anything a user or a crawler experiences.

Deliver an ordered list of work with the reasoning attached. If a client insists on a single number, agree on one that maps to their business, such as impressions for a defined query set, and state its limitations in the same sentence.

Core Web Vitals are a different case, because Google states that they are used by its ranking systems. Google also states that good scores do not guarantee top rankings and that there is no single page experience signal ([Google, page experience](https://developers.google.com/search/docs/appearance/page-experience)). Report them as a real signal of unknown weight, and do not sell speed as the headline result.

## 3. Change one thing at a time, except for hygiene

Shipping a title rewrite, a canonical fix, and 40 new internal links on the same afternoon means you will never know which one moved the numbers. If you intend to claim a result, isolate the change.

This has a cost, and the cost is not always worth paying. Obvious defects with no upside to leaving them in place, such as an accidental `noindex`, a broken canonical, a soft 404, or invalid structured data, are hygiene. Batch hygiene into one commit, ship it, and do not attempt to measure it individually. Reserve isolation for changes that are genuinely a bet.

## 4. Record what did not work

Every engagement produces changes that moved nothing. Writing them down costs you a paragraph and buys you the only kind of credibility that cannot be manufactured, because a vendor whose case studies contain no failures has either never tested anything or is not telling you about it.

The experiment log in [templates/experiment-log.md](../templates/experiment-log.md) has a verdict column with three values: improved, no change, worse. Fill it in honestly, including for your own idea.

## 5. Present the material, not the causal claim

"Our optimization tripled organic traffic" is almost always unfalsifiable. Seasonality, a competitor's outage, an algorithm update, and a paid campaign running in parallel are all live alternative explanations, and a single before-and-after chart cannot separate them.

Present the commit, the deploy date, the pre-registered threshold, the observation window, and the graph. Name the confounders you know about. Let the reader reach their own conclusion. Anyone with repository access can verify every element of that, which is what makes it worth more than a claim.
