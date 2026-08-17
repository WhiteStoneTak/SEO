# Data layer: own it instead of renting it

Facts in this document were checked on 2026-08-17. Pricing and product terms change, so verify before quoting them to anyone.

Two kinds of SEO data cannot be derived from the site itself. Search volume requires someone with access to search logs or ad auction data. Backlinks require an independent crawl of the web. Everything else in this repository is reproducible from the site plus Search Console.

The usual answer is a Semrush or Ahrefs subscription, which is a fixed monthly cost whether you run one audit or a hundred, and which locks the client's data inside a dashboard they lose access to when the engagement ends.

## OpenSEO plus DataForSEO

[OpenSEO](https://github.com/every-app/open-seo) is an MIT-licensed application covering keyword research, rank tracking, competitor analysis, backlinks, site audits, and AI visibility. It ships no data of its own. You supply a [DataForSEO](https://dataforseo.com/) API key and pay that vendor per request.

The hosted service at openseo.so adds a 28 percent margin on every DataForSEO request. Self-hosting removes that margin, which is the entire reason to self-host.

DataForSEO accounts include one dollar of credit for testing, and the minimum top-up is 50 dollars. Per-endpoint prices differ and have been revised, so read the [pricing page](https://dataforseo.com/pricing) before committing to a volume.

### Running it locally

```bash
git clone https://github.com/every-app/open-seo
cd open-seo
cp .env.example .env
# set DATAFORSEO_API_KEY in .env
docker compose up -d
```

It listens on port 3001 by default.

One thing to get right: Docker mode runs with `AUTH_MODE=local_noauth`, meaning no authentication at all. Keep it on localhost or behind your own authenticated proxy. Putting it on a public hostname exposes your DataForSEO balance to anyone who finds it.

The project sends anonymized usage telemetry. Set `OPENSEO_TELEMETRY_DISABLED=1` or `DO_NOT_TRACK=1` in `.env` to turn it off, which is worth doing before client work under a confidentiality agreement.

It also documents connecting Google Search Console and Google Analytics, so first-party and third-party data end up in one place.

### Through an agent

OpenSEO exposes an MCP server, so an agent can query keyword, rank, and backlink data directly rather than through a browser. Setup is documented at [openseo.so/docs/mcp](https://openseo.so/docs/mcp).

That is what makes the playbooks in [skills/](../skills/) into something other than reading material. An agent can pull volumes for a query set, cross-reference them against the pages that exist in the repository, and produce the query-to-page map from [05](05-phase1b-onpage-content.md) without a human copying numbers between tabs.

## Cost control

Per-request billing punishes carelessness differently than a subscription does. A subscription makes an accidental thousand-keyword pull free and invisible. Per-request billing makes it a line item.

Decide the query set before pulling anything, prefer the slower queue when the answer is not needed in the next five minutes, and pull rank tracking on a schedule that matches how often you will actually read it. Weekly is enough for most small sites.

## What this still does not give you

Backlink coverage depends on DataForSEO's crawl, which is not the same as Ahrefs' crawl. For a competitive link analysis where completeness matters, the incumbent index is still the better product. For checking whether a specific site has an obvious link problem, this is sufficient.

Search volumes from any source are modeled estimates, rounded and averaged over months. Treat them as an ordering of relative demand, never as a forecast of traffic.

## Handing data to the client

Because you self-host, exports belong to the client. Give them the CSV and the JSON alongside the report. It costs nothing, it survives the end of the engagement, and it is the opposite of the arrangement where the analysis evaporates when the subscription lapses.
