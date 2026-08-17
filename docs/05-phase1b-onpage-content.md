# Phase 1b: on-page and content

The technical audit tells you whether a page can be indexed. This part tells you whether it deserves to rank once it is.

Machines cannot do most of this. A crawler can report that a title is missing. It cannot report that the page answers a question nobody asks, or that the one page a buyer needs does not exist.

## Map queries to pages

Take the queries the business actually cares about and ask, for each one, which single page is supposed to win it. Three outcomes:

**No page exists.** This is the most valuable finding in the whole audit and the one crawlers never produce. It is also the most expensive to act on, because it means writing something.

**Several pages compete.** Two or three pages covering the same intent split links and impressions between them. Consolidate into one and redirect the rest. Do not add a fourth.

**A page exists but targets the wrong intent.** Someone searching for a price finds a page about the company's philosophy. The fix is editing, not adding.

Build this as a table with one row per query and keep it in the repository. It becomes the reference for every later content decision. The playbook in [skills/seo-keyword-to-page](../skills/seo-keyword-to-page/SKILL.md) automates the tedious half.

## Read the results page before writing anything

Search the query yourself and look at what is already there. If the top ten are all comparison tables, the searcher wants a comparison table, and a beautifully written essay will lose to a worse-written table. If the top ten are all official government or vendor documentation, an outsider's blog post is not going to displace them, and that query should be dropped from the target set.

This takes five minutes per query and prevents weeks of writing in the wrong format.

## Titles and descriptions

The title has two jobs, telling a search engine what the page is about, and convincing a human to click. Write for the human, include the term the human typed, and put the distinguishing part first because the end gets truncated.

A workable pattern for a small site is `<specific page subject> | <organization>`. Note that Google rewrites titles when it detects a problem such as boilerplate repeated across the site ([Google, title links](https://developers.google.com/search/docs/appearance/title-link)), so a title that is 80 percent organization name invites a rewrite.

Meta descriptions do not affect ranking. They frequently become the snippet, so they affect clicks. Write one per page, describe what the reader gets, and let Google replace it when a query-specific extract would serve the reader better.

Generating both from a template is acceptable when there are hundreds of similar pages, and is a poor trade for the twenty pages that carry the business.

## Headings and page structure

One `h1` matching the page subject, `h2` sections that a reader could scan as a table of contents, no heading levels skipped for visual reasons. Style with CSS, not with heading tags.

If the page answers a specific question, let the answer appear early and in plain text. This helps a reader in a hurry, and it is also what gets extracted for snippets and for AI answers, which is discussed in [11](11-ai-search-visibility.md).

## Internal linking

Internal links are the part of link building that requires no outreach, no budget, and nobody else's permission. They are consistently underused.

Link from pages that have authority to pages that need it, using anchor text that describes the destination. When you publish something new, go back and link to it from the existing pages that mention the topic, because a new page with no inbound internal links is nearly invisible.

Contextual links inside body copy are worth more than another entry in the footer, and a footer containing every page on the site tells a crawler nothing about which pages matter.

## Thin and duplicated pages

The instinct to expand every short page is wrong. A short page that answers its question is fine. The problem is a page that exists for a keyword and says nothing.

For each thin page, choose one of four: merge it into a stronger page and redirect, expand it because the topic genuinely deserves a page, `noindex` it because it is useful to users but not to search, or delete it and return 410. Doing nothing is also a choice, and it is the default outcome when you decide to expand everything and then run out of time.

## Content brief format

Before writing anything, fill in five lines. If any line is blank, the page is not ready to be written.

1. Target query and the intent behind it
2. The reader, stated as a role and a situation
3. What the top three results currently provide
4. What this page will provide that they do not
5. The action the reader should be able to take at the end
