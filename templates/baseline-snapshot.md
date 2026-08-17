# Baseline snapshot

Index file for the raw exports captured in Phase 0. Commit this next to the exports themselves.

- **Site:** https://example.com
- **Captured:** 2026-09-01
- **Captured by:**
- **Search Console property:** domain property / URL prefix, verified 2026-09-01
- **Field data source:** Search Console CWV report / web-vitals to own endpoint / GA4

## Files

| File | Contents | Captured |
| --- | --- | --- |
| `gsc-pages-2026-09-01.csv` | Index coverage export | 2026-09-01 |
| `gsc-queries-2026-09-01.csv` | Performance, last 3 months | 2026-09-01 |
| `crawl-2026-09-01.json` | Full crawl, facts only | 2026-09-01 |
| `raw-html/` | `curl` output for the top 10 pages | 2026-09-01 |
| `rendered-html/` | Headless browser DOM for the same 10 | 2026-09-01 |
| `robots.txt` | Verbatim | 2026-09-01 |
| `sitemaps/` | Every sitemap, verbatim | 2026-09-01 |
| `lighthouse/` | Full JSON, one run per template | 2026-09-01 |

## State at capture

| Metric | Value | Source |
| --- | --- | --- |
| Indexed pages | | GSC Pages |
| Pages excluded, by reason | | GSC Pages |
| URLs in sitemap | | sitemap |
| Total impressions, 28 days | | GSC Performance |
| Total clicks, 28 days | | GSC Performance |
| LCP, p75 field | | field source |
| CLS, p75 field | | field source |
| INP, p75 field | | field source |

## Access obtained

| Item | Status | Date | Note |
| --- | --- | --- | --- |
| Search Console | | | read / full |
| Analytics | | | |
| Repository | | | |
| Deploy pipeline | | | |
| Crawl permission | | | |

## Gaps

What could not be captured, why, and on what date the request was made. Written now, because nobody will remember in six weeks.

-

## Data before this date

State plainly what history exists and what does not. If the property was verified today, there is no comparison period, and every early report has to say so.
