---
name: collect-data
description: Pull Brand Radar, Keywords Explorer, and SERP Overview data for a sector/brand/country combination
argument-hint: [sector] [brands] [country-code]
allowed-tools: Write, Bash, mcp__1a081627-4991-4907-9154-9bd405f0af14__brand-radar-mentions-overview, mcp__1a081627-4991-4907-9154-9bd405f0af14__brand-radar-sov-overview, mcp__1a081627-4991-4907-9154-9bd405f0af14__brand-radar-cited-domains, mcp__1a081627-4991-4907-9154-9bd405f0af14__brand-radar-ai-responses, mcp__1a081627-4991-4907-9154-9bd405f0af14__keywords-explorer-overview, mcp__1a081627-4991-4907-9154-9bd405f0af14__keywords-explorer-matching-terms, mcp__1a081627-4991-4907-9154-9bd405f0af14__serp-overview, mcp__1a081627-4991-4907-9154-9bd405f0af14__doc
---

# Collect Data Sub-skill

Pull all data from Ahrefs MCP for a brand visibility article.

## Input

- **sector**: Industry name (e.g., "supermercados", "streaming", "e-commerce")
- **brands**: Comma-separated brand list
- **country**: ISO country code (ES, BR, MX, KR, etc.)

## Procedure

### A. Brand Radar — ChatGPT Data

For each brand, pull mentions and SOV from ChatGPT:

```
brand-radar-mentions-overview:
  select: "brand,total"
  data_source: "chatgpt"
  brand: "[first-brand]"
  competitors: "[remaining-brands]"
  country: "[country-code]"

brand-radar-sov-overview:
  select: "brand,share_of_voice"
  data_source: "chatgpt"
  brand: "[first-brand]"
  competitors: "[remaining-brands]"
  country: "[country-code]"
```

### B. Brand Radar — AI Overviews Data

Same calls but with `data_source: "google_ai_overviews"`.

### C. Brand Radar — Cited Domains

Pull the top domains cited in AI responses related to this sector:

```
brand-radar-cited-domains:
  select: "domain,responses,volume"
  data_source: "chatgpt"
  brand: "[first-brand]"
  competitors: "[remaining-brands]"
  country: "[country-code]"
  limit: 10
```

### D. Keywords Explorer — Industry Keywords

1. First, determine 5-10 relevant industry keywords. Examples for "supermercados" in ES:
   - "mejores supermercados", "supermercados online", "comparativa supermercados", etc.

2. Pull overview metrics:

```
keywords-explorer-overview:
  select: "keyword,volume,difficulty,cpc,traffic_potential,serp_features"
  keywords: "[keyword1],[keyword2],..."
  country: "[country-code]"
```

3. Optionally, discover more keywords:

```
keywords-explorer-matching-terms:
  select: "keyword,volume,difficulty,traffic_potential"
  keywords: "[sector-keyword]"
  country: "[country-code]"
  limit: 20
  order_by: "volume:desc"
```

### E. SERP Overview — Top 2-3 Keywords

For the 2-3 highest-volume industry keywords, pull SERP data:

```
serp-overview:
  select: "position,url,title,domain_rating,traffic,top_keyword"
  keyword: "[keyword]"
  country: "[country-code]"
  top_positions: 10
```

## Output

Save all collected data as JSON to: `1-data/[slug].json`

```json
{
  "meta": {
    "sector": "supermercados",
    "brands": ["Mercadona", "Carrefour", "Lidl", "Dia", "Alcampo", "Aldi"],
    "country": "ES",
    "date": "2026-02-18"
  },
  "chatgpt": {
    "mentions": [ {"brand": "...", "total": 1234}, ... ],
    "sov": [ {"brand": "...", "share_of_voice": 0.457}, ... ]
  },
  "ai_overviews": {
    "mentions": [ {"brand": "...", "total": 1234}, ... ],
    "sov": [ {"brand": "...", "share_of_voice": 0.457}, ... ]
  },
  "cited_domains": [
    {"domain": "...", "responses": 1234, "volume": 5678}, ...
  ],
  "keywords": [
    {"keyword": "...", "volume": 1234, "difficulty": 45, "cpc": 50, "traffic_potential": 5678, "serp_features": [...]}, ...
  ],
  "serp": {
    "[keyword]": [
      {"position": 1, "url": "...", "title": "...", "domain_rating": 80, "traffic": 5000, "top_keyword": "..."}, ...
    ]
  }
}
```

## Important Notes

- Always use `doc` tool first if unsure about a parameter
- The first brand in the list goes in `brand`, the rest go in `competitors`
- For cited domains, use the `market` parameter with the sector name if results are too broad
- If a Brand Radar call returns empty data, try without the `country` filter (some markets have limited data)
- For Keywords Explorer, generate keyword ideas in the LOCAL LANGUAGE of the target country
