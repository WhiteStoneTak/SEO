# CI gates

An external audit ends when the report is delivered. The site keeps shipping. Six weeks later a refactor drops the head component from one layout, nobody notices, and the fix that took an afternoon is gone.

Catching that requires being inside the pipeline, which is why this chapter exists and why no agency deliverable contains it.

## Level 1: assert the tags in a test

The cheapest useful gate. For one representative page per template, render it and assert that the expected tags are present and non-empty.

```js
// pseudo-code, adapt to the project's test runner
const html = await renderPage("/");
assert(/<title>[^<]+<\/title>/.test(html));
assert(/<meta name="description" content="[^"]+"/.test(html));
assert(/<link rel="canonical" href="https:\/\/[^"]+"/.test(html));
assert(/<html[^>]+lang="/.test(html));
```

Runs in seconds, needs no network, and catches the regression that actually happens. Add one assertion per finding you fixed, and the test file becomes a record of what the site is supposed to guarantee.

## Level 2: validate structured data

Structured data breaks silently, because a page with invalid JSON-LD looks identical to a page with valid JSON-LD. Parse every JSON-LD block during the build and fail on parse errors, missing `@type`, or missing required properties for the types you rely on.

For TypeScript projects, [`schema-dts`](https://github.com/google/schema-dts) makes malformed structured data a type error, which moves the check from CI to the editor.

## Level 3: performance budgets

[Lighthouse CI](https://github.com/GoogleChrome/lighthouse-ci) runs Lighthouse against a preview deployment and fails the build when a metric crosses a budget.

Set budgets on the individual metrics, LCP, CLS, and TBT, not on the composite score, since the composite can stay flat while LCP doubles. Set the initial budget at the current value plus a small margin so the gate blocks regressions rather than demanding a project. Tighten it after each improvement.

Lab numbers are noisy on shared CI runners. Run three times and take the median, or accept intermittent failures and the loss of trust that follows.

## Level 4: crawl the preview deployment

For sites where a routing change can break many URLs at once, crawl the preview build and fail on new 404s, new redirect chains, orphaned pages, or a drop in the number of indexable URLs.

This is the most expensive gate to maintain and the only one that catches a whole class of URL-level regressions before release. Add it after a release has already broken URLs once, not before.

## Do not gate on things you cannot control

Rankings, impressions, and third-party scores are not build outputs and must never fail a build. Gate only on properties the repository determines: markup present, structured data valid, budgets met, URLs resolving.

## Make failure legible

A gate that fails with a stack trace teaches the team to disable the gate. Fail with the URL, the missing thing, the reason it matters in one line, and a link to the finding it came from.

```
FAIL /pricing
  missing: <link rel="canonical">
  why: duplicate URLs consolidate to the wrong page without it
  finding: seo-03
```
