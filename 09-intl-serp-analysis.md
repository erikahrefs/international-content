# Skill: /intl-serp-analysis — SERP Landscape Analysis by Country

## Purpose
Analyze the search engine results page (SERP) for specific keywords in different countries to understand the competitive landscape, SERP features present, content types that rank, and opportunities to capture positions in international markets.

## When to Trigger
- User asks "what does the SERP look like for [keyword] in [country]?"
- User wants to understand competitive positioning for a specific query in a market
- User mentions "SERP analysis", "search results analysis", "who ranks for X in Y country"
- User wants to plan content strategy based on what's currently winning in a SERP

## Required Inputs
- **keyword**: The search query to analyze (in the local language for best results)
- **country**: The country code (e.g., `fr`, `de`, `jp`, `br`)
- **Optional**: `date` for historical SERP, `top_positions` to limit results

## Workflow

### Step 1: Pull SERP Overview
Use **SERP Overview**:
- Keyword: the target keyword (use native language for non-English markets)
- Country: target country code
- Select: `url, title, position, backlinks, refdomains, traffic, keywords, domain_rating`
- Top positions: 10-20
- This returns the full first page of results with metrics for each

### Step 2: Keyword Metrics Context
Use **Keywords Explorer - Overview**:
- Keywords: the target keyword
- Country: target country
- Select: `keyword, volume, difficulty, cpc, traffic_potential, clicks, global_volume`
- This provides the overall keyword metrics to contextualize the SERP

### Step 3: Analyze Each SERP Competitor
For the top 3-5 ranking URLs, use **Site Explorer - Organic Keywords**:
- Target: each ranking URL (exact URL, not domain)
- Mode: `exact`
- Country: target country
- Select: `keyword, position, volume, traffic`
- Limit: 10
- This reveals what OTHER keywords each page ranks for

### Step 4: Check Your Current Position
Use **Site Explorer - Organic Keywords**:
- Target: your domain
- Country: target country
- Where: filter for the target keyword
- This shows if/where you currently rank and which URL is ranking

### Step 5: Cross-Country SERP Comparison (Optional)
Repeat Step 1 for 2-3 additional countries with the same keyword (or its translation):
- This reveals if the same sites dominate globally or if local players win in each market

## Analysis Framework

For each SERP result, evaluate:

1. **Domain Authority Gap** — Your DR vs. ranking pages' DR
2. **Content Type** — Blog post, tool page, listicle, video, product page?
3. **Backlink Requirement** — Median backlinks/refdomains of top 5 = minimum to compete
4. **Traffic Concentration** — Does #1 capture most traffic, or is it spread?
5. **SERP Features** — PAA boxes, featured snippets, videos, images, local packs
6. **Local vs. Global** — Results dominated by local-language sites or international English sites?
7. **Content Freshness** — Recent content or evergreen pages?

## Output Format

### SERP Analysis: "[keyword]" in [Country]

#### Keyword Metrics
- Search Volume: [number]
- Keyword Difficulty: [KD]
- CPC: [value]
- Traffic Potential: [number]
- Global Volume: [number]

#### Current SERP Results

| Pos | Title | Domain | DR | Backlinks | Ref Domains | Traffic | Content Type |
|-----|-------|--------|---:|----------:|------------:|--------:|-------------|

#### SERP Features Present
- [ ] Featured Snippet
- [ ] People Also Ask (count: X)
- [ ] Video carousel
- [ ] Image pack
- [ ] Knowledge panel
- [ ] Local pack
- [ ] Shopping results

#### Your Current Position
- Ranking URL: [url or "Not ranking"]
- Position: [number or N/A]
- Traffic from this keyword: [number]

#### Competitive Benchmarks
- Median DR of top 5: [number]
- Median Backlinks of top 5: [number]
- Median Ref Domains of top 5: [number]
- Content type winning: [type]

### Recommendations

1. **Can you compete?** — Yes/No/Maybe based on DR gap, backlink requirements, content type
2. **Recommended content format** — Match what's winning
3. **Target SERP features** — Which features you can capture (PAA, featured snippet)
4. **Required investment** — Estimated backlinks needed, content depth required
5. **Localization angle** — If English sites rank in non-English SERPs = opportunity for localized content

## Example with Real Data ("logiciel design graphique" — France)

**Keyword Metrics:** Volume 300 | KD 27 | CPC $0.60

| Pos | Title | Domain | DR | Traffic |
|-----|-------|--------|---:|-------:|
| 1 | Les meilleurs logiciels de graphisme en 2025 | ynov.com | 72 | 439 |
| 2 | Top 10 des logiciels de création graphique | lisaa.com | 62 | 418 |
| **3** | **Créez un graphique personnalisé en ligne** | **canva.com** | **93** | **6,635** |
| 4 | *People Also Ask (4 questions)* | — | — | — |
| 5 | Les 10 meilleurs logiciels de graphisme | graphiste.com | 71 | 96 |
| 6 | Applications de design graphique | adobe.com | 96 | 143 |
| 7 | Logiciel de design graphique et vectoriel | affinity.studio | 76 | 3,143 |
| 8 | 14 meilleurs logiciels gratuits | publuu.com | 85 | 156 |

**Insight:** "Canva ranks #3 but captures 6,635 visits — more than positions 1, 2, 5, 6, 7, 8 combined. The #1 and #2 results are French educational institutions (DR 72 and 62) with much lower authority than Canva (DR 93). Canva could overtake them with a dedicated French-language comparison/listicle page. 4 PAA questions appear at position 4 — FAQ content opportunity. The SERP is 90% French-language, confirming this keyword requires native French content."
