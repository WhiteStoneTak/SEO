# Phase 1: technical audit

Estimated time: one to three hours for a site of a few hundred pages, plus reading time.

Collect facts. Do not rank them yet, and do not start fixing the first thing you find. Ranking happens in [Phase 2](06-phase2-prioritization.md), and the order changes once you can see everything.

Two rules for this phase. Separate extraction from judgement, so that adding a new check later does not require recrawling. And never record a finding without both a reason it matters and a concrete way to fix it, because a finding the reader cannot act on is noise.

## Before you crawl

Crawling costs the target server real resources. Only crawl sites you are authorized to crawl, respect `robots.txt`, and rate limit. A 250ms delay between requests is a reasonable default for a small site.

If the client's `robots.txt` blocks the agent you are using, either use a different tool that identifies itself honestly under an allowed agent, or get written permission first. Do not quietly ignore the file.

## Layer 1: reachability and status

| Check | How | Why it matters |
| --- | --- | --- |
| Canonical host and protocol | Request all four of `http/https` x `www/apex` and follow redirects | Multiple reachable hosts split signals and duplicate the whole site |
| Redirect chains | Count hops to the final URL | Each hop is latency, and long chains eventually stop being followed |
| Nonexistent URL returns 404 or 410 | `curl -I https://example.com/definitely-not-a-page-xyz` | A 2xx response with error-like content is reported as a soft 404 ([Google, HTTP status codes](https://developers.google.com/search/docs/crawling-indexing/http-network-errors)). Common on SPAs, see [10](10-javascript-sites.md) |
| Server errors under normal load | Watch status codes across the crawl | 5xx during a crawl means the same during a Googlebot visit |
| `robots.txt` is valid and served as text | Fetch it and read the whole body | A catch-all route can append HTML to it, which is not what anyone intended |
| Sitemap exists, parses, and matches reality | Fetch every sitemap, diff against the crawl | URLs in the sitemap that 404, and indexable pages missing from the sitemap, are both defects |

Diffing the sitemap against the crawl in both directions is the single highest-yield check in this section, and most audits only do one direction.

## Layer 2: index control

Anything in this section that is wrong outranks everything else in the audit. A page carrying an accidental `noindex` is not competing badly, it is absent.

| Check | What to look for |
| --- | --- |
| `noindex` on pages meant to be public | `<meta name="robots">` and the `X-Robots-Tag` response header. Check both, since the header is invisible in view-source |
| `Disallow` on pages meant to be crawled | Note that a disallowed page can still be indexed from external links, without a snippet |
| Self-referencing canonical present and correct | Absolute URL, matching protocol and host, one per page |
| Canonicals pointing somewhere unintended | Whole sites have been canonicalized to the homepage by one bad template |
| Staging or preview hosts reachable and indexed | Search for the hostname. Fix with authentication, not with `robots.txt` |
| Parameter and tracking URLs generating duplicates | `?utm_*`, session ids, sort and filter parameters |

## Layer 3: what the page tells the search engine

Google generates the title link in results from several sources, including the `title` element, the visible main heading, other headings, `og:title`, and anchor text pointing at the page, and it rewrites titles when it detects a problem ([Google, title links](https://developers.google.com/search/docs/appearance/title-link)). A missing `title` element does not produce a blank result. It produces a result whose wording you did not choose.

| Check | Note |
| --- | --- |
| `title` present, unique, describes the page | Duplicates across templates are the usual failure |
| `meta description` present and specific | Not a ranking factor, but it is the snippet, and the snippet decides the click |
| Exactly one `h1`, and it matches the page subject | Multiple `h1` elements are valid HTML and still usually indicate a template problem |
| `html lang` set correctly | Missing entirely on many framework starters |
| `hreflang` reciprocal across every language version | Non-reciprocal annotations get ignored. Include a self-reference |
| Open Graph and Twitter Card tags | Controls how the page looks when shared, which is adjacent to SEO rather than part of it |
| Structured data valid | Validate with the [Rich Results Test](https://search.google.com/test/rich-results) and the [Schema Markup Validator](https://validator.schema.org/). Start with `Organization` and `BreadcrumbList` |

## Layer 4: rendering

Fetch the raw HTML with `curl` and compare it to the rendered DOM from a headless browser. If the main content only exists in the rendered version, the site depends on JavaScript execution for indexing, which is a risk to write down, not automatically a defect.

```bash
curl -sL https://example.com/ | wc -c
curl -sL https://example.com/ | grep -c "<h1"
```

If that returns a page of a few hundred bytes with no headings, everything in Layer 3 is invisible in the raw response, and [10-javascript-sites](10-javascript-sites.md) applies.

## Layer 5: internal link structure

Treat the crawl as a graph and look at it that way.

- Orphan pages, indexable but not linked from anywhere. Every orphan is either a linking bug or a page that should not exist
- Click depth from the homepage. Anything past four hops is hard to justify on a small site
- Pages with exactly one inbound internal link, which is fragile
- Navigation implemented as buttons or JavaScript handlers instead of `<a href>`, which produces links that are not links
- Anchor text that says "here" or "read more" everywhere

## Layer 6: performance

Run Lighthouse per template rather than per page, since pages sharing a template share their performance profile. Store the full JSON so you can diff later.

Read the metrics, not the score. LCP, CLS, and INP are the Core Web Vitals; the composite Lighthouse number is a weighted average that hides which one is bad.

## Output of this phase

One findings file, one row per finding, using [templates/findings.md](../templates/findings.md). Each row carries the affected URLs, the evidence, why it matters, how to fix it, and an implementation cost estimate. No priority column yet.
