# Pre-launch checklist

Run before a new site or a redesign goes live. Most of these cost minutes now and days later.

## Blocking, do not launch without these

- [ ] `robots.txt` does not carry the staging `Disallow: /`. This is the single most common launch failure
- [ ] No `noindex` left on public pages, in the markup and in the `X-Robots-Tag` header
- [ ] The staging environment is unreachable or authenticated, not merely disallowed in `robots.txt`
- [ ] A nonexistent URL returns 404 or 410, not 200
- [ ] One canonical host and protocol, with the others redirecting in a single hop
- [ ] Every old URL redirects to its specific successor with a 301, if this replaces an existing site
- [ ] Valid TLS on every hostname in use

## Indexability

- [ ] Sitemap exists, parses, contains only indexable 200 URLs, and is referenced from `robots.txt`
- [ ] Every indexable page is reachable by following `<a href>` links from the homepage
- [ ] Self-referencing canonical on every page, absolute, correct host and protocol
- [ ] Main content present in the raw response, or a decision recorded that JavaScript rendering is accepted

## Metadata

- [ ] Unique `title` on every page
- [ ] `meta description` on every page that matters
- [ ] Exactly one `h1` per page, matching the subject
- [ ] `html lang` set
- [ ] `hreflang` reciprocal including self-reference, if multilingual
- [ ] Open Graph and Twitter Card tags with a functioning image URL
- [ ] `Organization` structured data, validated

## Measurement

- [ ] Search Console property verified, preferably a domain property
- [ ] Sitemap submitted
- [ ] Field data collection live
- [ ] Baseline snapshot committed with a date

## Performance

- [ ] LCP, CLS, and TBT measured per template and recorded
- [ ] The LCP image is not lazy-loaded
- [ ] Images sized so they do not shift layout on load

## Policy decisions, recorded rather than inherited

- [ ] AI crawler rules in `robots.txt` reflect a decision by a named person on a known date
- [ ] Analytics choice reviewed against the site's privacy policy
- [ ] Cookie or consent banner does not block rendering of main content

## The day after launch

- [ ] Fetch `robots.txt` in production and read the entire body
- [ ] Request indexing for the homepage and two key pages
- [ ] Check Search Console for coverage errors
- [ ] Confirm field data is arriving
