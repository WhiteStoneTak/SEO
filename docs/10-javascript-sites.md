# JavaScript sites

Framework defaults produce a specific and recurring set of SEO failures. Recognizing them by their signature saves a day of investigation, and fixing them requires reading the router and the rendering configuration, which is where an external audit has to stop.

## The two-minute diagnosis

```bash
curl -sL https://example.com/ > raw.html
wc -c raw.html
grep -ci "<title" raw.html
grep -ci "<h1" raw.html
grep -ci "canonical" raw.html
```

Then load the same URL in a headless browser and compare. Four common outcomes:

| Raw response | Meaning |
| --- | --- |
| Full content, full head | Server rendered and fine. Look elsewhere |
| Full content, empty head | Content renders on the server but the head is never populated. The most common defect, and usually a one-file fix |
| Empty shell, content only after JS | Client-side rendering only. Indexing depends on the renderer running, which is a risk worth writing down |
| Different content raw versus rendered | Something is branching on user agent or on locale. Investigate before anything else |

## Failure 1: no metadata anywhere

The site renders its body on the server, and the `<head>` contains no `title`, no description, no canonical, and no `lang`. Every page is affected identically, which is the tell that it is one missing piece of configuration rather than an editorial oversight.

Google will still show a result. It generates the title link from headings, anchor text, and other sources when the `title` element is missing or unhelpful ([Google, title links](https://developers.google.com/search/docs/appearance/title-link)). The wording of every result for the site is then chosen by Google rather than by its owner.

The fix is in the framework's head management API, applied in the base layout so that all templates inherit it, with per-page overrides where they matter. Cost is small, reach is the whole site, which usually puts it at the top of the Phase 2 list.

## Failure 2: catch-all routes return 200 for everything

Request a URL that cannot exist. If it returns 200 with the homepage content, every typo, every stale external link, and every crawler probe becomes an indexable URL. Google reports these as soft 404s when it notices ([Google, HTTP status codes](https://developers.google.com/search/docs/crawling-indexing/http-network-errors)).

Fix in the routing layer so that unmatched paths return a real 404 status, not a 200 rendering a page that says "not found". Static hosts commonly have an SPA fallback setting that causes this; check the host configuration before assuming the bug is in the application code.

## Failure 3: language routing that crawlers do not survive

A frequent pattern: `/ja/` serves a meta refresh to `/`, and `/` reads `navigator.language` in JavaScript and redirects elsewhere for other locales.

A crawler generally identifies as `en-US`. Follow that path as a crawler and the Japanese content may never be reached, which is fatal for a business selling in Japanese.

Serve real content at a stable URL per language. Use server-side negotiation for the initial visit if you want convenience, never client-side redirection as the only path, and give every language version reciprocal `hreflang` annotations including a self-reference.

## Failure 4: navigation that is not links

Client-side navigation implemented with click handlers on `div` or `button` elements produces a site with no crawlable link graph. Use real `<a href>` elements and let the framework intercept the click. This also fixes middle-click, open-in-new-tab, and keyboard navigation, which are user-facing bugs that existed before anyone mentioned SEO.

## Failure 5: hydration changes the content

If the server renders one thing and the client replaces it with another, the indexed content is unpredictable. Any hydration mismatch warning in the console is an SEO issue as well as a rendering issue.

## Failure 6: robots.txt served by the catch-all

If `/robots.txt` does not exist as a real file, a catch-all route may answer it with HTML, sometimes appended to a CDN-managed body. Crawlers parse leniently, so this rarely causes visible damage, and it is still a file whose contents nobody chose. Fetch it and read the entire body rather than the first few lines.

## Ordering these fixes

Metadata and 404 status usually come first, since both are small, both are template level, and both affect every page. Language routing comes next when more than one language is a real business channel. Rendering strategy changes come last, because moving from client-side rendering to server-side rendering is an architectural project and the cheaper fixes often make it unnecessary.
