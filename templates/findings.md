# Findings

Output of Phase 1. Facts and reasoning, no priority column. Prioritization happens separately in `docs/06-phase2-prioritization.md`.

- **Site:** https://example.com
- **Audited:** 2026-09-01
- **Crawl scope:** 84 URLs from https://example.com/, depth 5, same origin only
- **Not covered:** subdomains, anything behind login, PDFs

## Summary

| ID | Finding | Affected | Severity | Cost |
| --- | --- | --- | --- | --- |
| seo-01 | | | | |
| seo-02 | | | | |

Severity: critical, high, medium, low. Cost: S, M, L.

## seo-01: short title of the finding

**Observed.** The exact evidence. Command output, URL, byte count, header, or markup. Someone else must be able to reproduce this from what is written here.

```
$ curl -sI https://example.com/definitely-not-a-real-page-xyz123 | head -1
HTTP/2 200
```

**Affected.** 84 of 84 indexable URLs.

**Why it matters.** One sentence. If it cannot be written in one sentence, the finding is not understood yet.

**How to fix.** Specific enough to open the right file. Name the layer: router, layout, host configuration, CMS template.

**Cost.** S, with the reason for the estimate.

**Severity.** high, with the reason.

**Uncertain.** Anything not yet verified, and what would settle it.

## seo-02: ...

## Observations that are not findings

Facts worth recording that are not defects. A client-side rendered site, an AI crawler block that may be intentional, a language routing scheme that works but is fragile. These belong in the record without being counted as problems.

-

## Checks not run

Which checks were skipped and why. Silence here reads as a clean result.

-
