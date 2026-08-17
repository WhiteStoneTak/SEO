# Site migration checklist

A replatform or domain change is where accumulated search visibility is most often destroyed, and the damage is usually discovered weeks later when the traffic graph has already dropped.

Treat the URL map as a deliverable of the migration project, not as a task for launch week.

## Before the migration

- [ ] Export the full list of current indexable URLs, from the crawl, the sitemap, and Search Console together. Each source contains URLs the others miss
- [ ] Export Search Console performance for the longest period available, so a comparison exists afterwards
- [ ] Rank the current URLs by clicks and impressions. Pages carrying traffic get individual attention; the tail can be handled by pattern
- [ ] Export the current backlink profile. Externally linked URLs must not break, since those links cannot be reissued
- [ ] Record the current index coverage count, which is the number to watch after cutover

## The URL map

- [ ] One row per old URL with its new URL, produced before the build is finished
- [ ] Each row maps to the closest equivalent page. Redirecting everything to the homepage is treated as a soft 404
- [ ] Where no successor exists, decide 410 deliberately and record the reason
- [ ] Redirects are 301, one hop, no chains
- [ ] Externally linked URLs are individually verified, not pattern-matched
- [ ] The map is committed to the repository, not kept in a spreadsheet that disappears

## Preserve on the new platform

- [ ] Titles and meta descriptions carried over, unless deliberately rewritten as a separate change
- [ ] Structured data reimplemented and revalidated
- [ ] Canonicals correct for the new URL structure
- [ ] `hreflang` rebuilt, if multilingual
- [ ] Images retained at reachable URLs, since image search traffic is lost silently

## Cutover day

- [ ] `robots.txt` on the new platform is the production version, not the staging one
- [ ] Sitemap regenerated with the new URLs and submitted
- [ ] Old sitemap left available briefly, so old URLs get recrawled and their redirects discovered
- [ ] Spot-check 20 redirects in production with `curl`, chosen from the highest-traffic rows
- [ ] Confirm a nonexistent URL returns 404
- [ ] Analytics and field data collection confirmed working on the new platform

## After

- [ ] Search Console change of address submitted, for a domain change
- [ ] Both properties kept verified during the transition
- [ ] Index coverage watched daily for the first two weeks. A drop that does not recover is the signal to investigate the map
- [ ] Crawl the new site for redirect chains introduced by the migration
- [ ] Compare impressions against the pre-migration export at 4 and 12 weeks

## Expect a dip

A temporary decline after a migration is normal while URLs are recrawled and reassessed. That expectation is not a reason to skip the checks above, and stating it in advance is what keeps a normal dip from being read as a disaster.

Agree beforehand on how large a dip and how long a recovery would count as a problem, and write the number down. Deciding that afterwards produces an argument instead of a decision.
