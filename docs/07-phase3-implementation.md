# Phase 3: implementation

This is where having the repository stops being a convenience and starts being the method.

## One change, one commit

Each item from the bets bucket becomes exactly one commit and one pull request. Put the finding id in the subject line so that the commit, the finding, and the experiment log row can be joined months later by anyone, including a search in the git history.

```
seo-03: emit self-referencing canonical on all page templates

Every page rendered without a canonical link. Adds an absolute
self-referencing canonical in the base layout.

Affected: 72 indexable pages
Finding: seo-03
Deploy target: 2026-09-01
```

Hygiene items ship together as one commit that lists what it contains. They are not measured individually, so splitting them buys nothing and costs review time.

## Do not touch anything else

The strongest reason to keep SEO commits narrow is that the moment one contains an unrelated refactor, the deploy date stops meaning anything and the experiment is dead. The second reason is that reviewers approve small diffs and stall on large ones.

If you find an unrelated bug while implementing, write it down and keep going.

## Prefer the template over the page

Adding a title to one page is an hour of work with almost no effect. Adding titles to the layout that renders every page is roughly the same hour with a hundred times the reach. Whenever a finding lists many affected URLs, look for the single file that renders them all.

Where framework conventions exist, use them rather than injecting tags manually, since manual injection tends to survive until the next framework upgrade and no further.

## Redirects

Every URL change needs a 301 from the old URL, and the old URL must not be left returning 200 with different content. Redirect to the specific equivalent page, not to the homepage, because a redirect to the homepage is treated as a soft 404 and also annoys the human who followed the link.

Keep redirects in one file that a human can read. Check for chains after adding any, since a redirect added today onto a redirect added last year is the usual way chains appear.

## Deletion

Deleting a page is a legitimate SEO action and is often the correct one. Return 410 for pages deleted intentionally with no successor, use 301 when a successor exists, and remove the URL from the sitemap in the same commit.

## Record the deploy date

Commit date and deploy date are not the same, and the deploy date is the one that matters for measurement. Record it in the experiment log at the moment of deploy, not from memory a month later.

If the deploy schedule is out of your hands, ask for the date rather than assuming it, and write down that you asked.

## Verify in production before starting the clock

After the deploy, confirm the change is actually live in the raw response, not just in the local build.

```bash
curl -sL https://example.com/ | grep -i "<link rel=\"canonical\""
```

Then request indexing for a representative URL through the URL Inspection tool in Search Console. This does not guarantee anything, and it does remove the "was it even crawled" question from the later analysis.

The observation window starts at the verified deploy, not at the merge.
