---
name: seo-technical-audit
description: Run a technical SEO audit of a website and produce a findings file with evidence, reasoning, and fix instructions. Use when asked to audit a site's SEO, diagnose why pages are not indexed or not ranking, or check a site before launch. Collects facts only and does not fix anything.
---

# Technical SEO audit

Produce a findings file. Do not fix anything in this run, and do not rank the findings yet.

## Before starting

Confirm the user is authorized to crawl the target. If they are not, stop and say so.

Fetch and read `robots.txt` in full before any other request. Respect it. Space requests at least 250ms apart. Keep total requests proportionate to the site: a few dozen for a spot check, a full crawl only when the user asked for one.

Ask for the target URL and the set of queries the business cares about, if not given. Proceed without the query set if the user does not have one, and note it as a gap.

## Step 1: reachability

```bash
for u in http://example.com https://example.com http://www.example.com https://www.example.com; do
  echo "== $u"; curl -sIL -o /dev/null -w "%{http_code} %{url_effective}\n" "$u"
done
curl -sI https://example.com/definitely-not-a-real-page-xyz123 | head -1
curl -s https://example.com/robots.txt
```

Record: which hosts respond, the redirect target and hop count, the status for a nonexistent path, and the full body of `robots.txt`.

A 200 for the nonexistent path is a soft 404 and is a finding.

## Step 2: sitemaps

Fetch every sitemap referenced in `robots.txt`, plus `/sitemap.xml` and `/sitemap_index.xml`. Parse them and record the URL count.

Diff in both directions: sitemap URLs that do not return 200, and crawled indexable URLs missing from the sitemap. Both directions are findings.

## Step 3: per-page extraction

For each page in scope, record from the raw response: status, final URL after redirects, byte size, `title`, `meta description`, `meta robots`, the `X-Robots-Tag` header, canonical, `html lang`, `hreflang` set, `h1` count and text, Open Graph tags, JSON-LD blocks, and internal links.

Check the response header separately from the HTML, since `X-Robots-Tag` is invisible in the markup.

Store this as raw facts with no judgement attached, so that adding a check later does not require refetching.

## Step 4: rendering check

Compare the raw response to the rendered DOM for two or three representative pages.

```bash
curl -sL https://example.com/ | grep -ci "<h1"
```

If the body is present but the head is empty, that is the metadata failure in `docs/10-javascript-sites.md`. If the body is also absent, note that indexing depends on JavaScript execution.

## Step 5: link graph

From the collected internal links, compute: orphan pages, click depth from the homepage, pages with a single inbound internal link, and navigation implemented without `<a href>`.

## Step 6: performance

Run Lighthouse once per template, not once per page. Keep the full JSON. Report LCP, CLS, and TBT individually and ignore the composite score.

## Step 7: write the findings file

One row per finding, using `templates/findings.md`. Every row needs all of these, and a row missing any of them is not ready:

- What was observed, with the exact evidence, such as the command output or the URL and byte count
- Which URLs are affected, and how many
- Why it matters, in one sentence
- How to fix it, specific enough to open the right file
- Implementation cost as S, M, or L
- Severity as critical, high, medium, or low

No priority column. Prioritization is a separate step with different inputs.

## Rules

State the crawl scope and where it was cut off, in the file itself.

Report facts that are not yet defects as observations, not as problems. A site that renders client-side is a risk to note, not automatically a fault.

If a check could not be run, write down which one and why. Do not silently skip it.
