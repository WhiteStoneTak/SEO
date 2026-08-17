# Phase 0: baseline

Estimated time: two to four hours, most of it waiting for access.

Nothing gets fixed in this phase. The goal is that on the day you do start fixing things, a dated record of the previous state already exists.

## Verify Search Console first

Search Console is the only first-party source for queries, impressions, clicks, position, and index coverage. It is free, and its data begins on the day of verification. Delay costs history permanently.

Verification methods, in order of preference:

| Method | Use when | Note |
| --- | --- | --- |
| DNS TXT record | You control DNS | Verifies the whole domain including subdomains and both protocols |
| HTML file upload | You control the deploy | Breaks if the build strips unknown files from the output directory |
| HTML meta tag | You control the template | Easy to lose during a redesign |
| Google Analytics / Tag Manager | Already installed with the right permissions | Ties SEO access to analytics access, which complicates handover |

Prefer the domain property over the URL prefix property. A URL prefix property treats `https://example.com` and `https://www.example.com` as separate entities, and you will eventually look at the wrong one.

Ask for read access rather than ownership if the client is nervous. Read access is enough for everything in this method.

## Set up field data collection

Lighthouse produces lab data, measured once on a simulated device. Field data is what real users experienced. The two disagree regularly, and field data wins.

Options, pick one:

- The Core Web Vitals report in Search Console, sourced from the Chrome UX Report. Free, no code, but only covers URLs with enough Chrome traffic, so small sites often see nothing.
- The [`web-vitals`](https://github.com/GoogleChrome/web-vitals) library sending to your own endpoint. Works at any traffic level, no third-party involved, which matters when the client has a strict privacy policy.
- GA4, if it is already installed and the client accepts it.

INP cannot be measured in a lab, because it requires real interaction. If you only have Lighthouse, treat Total Blocking Time as a proxy and say so in the report.

## Freeze the baseline as dated files

Write files, commit them, and date them. Screenshots invite the suspicion that they were edited later, and a number quoted in a slide has no provenance.

Minimum contents of the snapshot:

| Item | How to capture |
| --- | --- |
| Index coverage | Search Console Pages report, exported to CSV |
| Query performance | Search Console Performance, 3 months if available, exported to CSV |
| Full crawl of the current state | Any crawler you trust, saved as JSON or CSV |
| Rendered HTML of the top 10 pages | `curl` for the raw response, plus a headless browser for the rendered DOM |
| `robots.txt` and every sitemap | Fetch and store verbatim |
| Lighthouse run for a representative page per template | Store the full JSON, not the score |
| Current field data | Whichever source you chose above |

Use [templates/baseline-snapshot.md](../templates/baseline-snapshot.md) as the index file that sits next to the raw exports.

## Record what you could not get

Access requests get partially granted, and six weeks later nobody remembers which parts. Write the gaps down on the day, with the date and the reason. This paragraph is also what protects the engagement when someone later asks why a number is missing.

Common gaps: analytics access refused on privacy grounds, staging environment unavailable, deploy pipeline owned by an external contractor, historical data lost in a replatform.

## Exit criteria

Move to Phase 1 when the property is verified, one field data source is collecting, the snapshot files are committed with a date, and the access gaps are written down. Not before.
