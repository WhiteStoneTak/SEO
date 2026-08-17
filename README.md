# seo

A working method for doing SEO when you have commit access to the site.

Most SEO documentation is written for people who can only advise. This one assumes you can open the repository, change a template, and ship it. That changes what is worth doing, in what order, and how you report the result.

The repository contains prose, checklists, templates, and agent playbooks. It contains no crawler, no CLI, and no scoring engine. Everything here is reproducible with public tools: Search Console, Lighthouse, `curl`, and [OpenSEO](https://github.com/every-app/open-seo) for keyword, rank, and backlink data.

## Who this is for

- Engineers who inherited a site that ranks badly and want a defensible order of work
- Consultants who can edit the code and want to prove which change caused which result
- Anyone using a coding agent (Claude Code, Codex, and similar) to run an audit, since the [`skills/`](skills/) directory is written for exactly that

Assumed site size is tens to a few hundred pages. Large e-commerce catalogs, news publishers, and multi-location local SEO have their own constraints that this method does not cover.

## Start here

| If you are | Read |
| --- | --- |
| Starting an engagement | [01-principles](docs/01-principles.md), then [03-phase0-baseline](docs/03-phase0-baseline.md) |
| Auditing an unfamiliar site | [04-phase1-technical-audit](docs/04-phase1-technical-audit.md) |
| Holding a list of problems and no order | [06-phase2-prioritization](docs/06-phase2-prioritization.md) |
| Asked to prove a change worked | [08-phase4-measurement](docs/08-phase4-measurement.md) |
| Told the site is a SPA and nothing indexes | [10-javascript-sites](docs/10-javascript-sites.md) |
| Asked about ChatGPT and AI Overviews | [11-ai-search-visibility](docs/11-ai-search-visibility.md) |

## The five phases

Phase 0 sets up measurement. Nothing gets fixed before this, because a fix shipped without a baseline can never be evaluated afterwards. Phase 1 collects facts about the current state without judging them. Phase 2 turns facts into an ordered list of work. Phase 3 ships the work, one change per commit. Phase 4 waits out the observation window and records what happened, including the changes that did nothing.

Phase 2 is a deliberate stopping point. A diagnosis with a priced, ordered work list is a complete deliverable on its own.

## Contents

**Method**

- [01-principles](docs/01-principles.md)
- [02-scope-and-limits](docs/02-scope-and-limits.md)
- [03-phase0-baseline](docs/03-phase0-baseline.md)
- [04-phase1-technical-audit](docs/04-phase1-technical-audit.md)
- [05-phase1b-onpage-content](docs/05-phase1b-onpage-content.md)
- [06-phase2-prioritization](docs/06-phase2-prioritization.md)
- [07-phase3-implementation](docs/07-phase3-implementation.md)
- [08-phase4-measurement](docs/08-phase4-measurement.md)

**Beyond the standard engagement**

- [09-data-layer](docs/09-data-layer.md) run your own keyword, rank, and backlink stack instead of renting one
- [10-javascript-sites](docs/10-javascript-sites.md) failure modes specific to SPA and hybrid rendering
- [11-ai-search-visibility](docs/11-ai-search-visibility.md) AI answers, citation, and crawler policy as a business decision
- [12-ci-gates](docs/12-ci-gates.md) stop the fix from silently reverting three releases later
- [13-antipatterns](docs/13-antipatterns.md) what gets sold and does not work

**Reusable material**

- [skills/](skills/) five agent playbooks in `SKILL.md` format
- [templates/](templates/) baseline snapshot, findings, experiment log, client report
- [checklists/](checklists/) pre-launch and site migration
- [ja/](ja/) Japanese edition, plus notes on the Japanese-language market

## Using the skills with a coding agent

Copy any playbook into your agent's skill directory. For Claude Code:

```bash
cp -r skills/seo-technical-audit ~/.claude/skills/
```

The playbooks assume the agent can read the repository, run shell commands, and fetch URLs. They are also readable as plain documentation if you would rather do the work by hand.

## What this method does not promise

Rankings cannot be guaranteed by anyone. Traffic and conversion numbers cannot be guaranteed either. This repository does not cover link acquisition outreach, and it will not tell you how to survive a core update, because nobody outside Google knows that in advance.

The observation windows given in [08-phase4-measurement](docs/08-phase4-measurement.md) are working assumptions from practice, not figures published by any search engine. Calibrate them against your own data and correct them.

## License

MIT. See [LICENSE](LICENSE).
