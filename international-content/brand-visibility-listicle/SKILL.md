---
name: brand-visibility-listicle
description: Create data-driven brand visibility articles with tables (TablePress CSVs) using Brand Radar + Keywords Explorer + SERP Overview data from Ahrefs MCP. Configurable country and language.
argument-hint: [sector] [brands] [country-code]
allowed-tools: Read, Write, Bash, WebSearch, WebFetch, mcp__1a081627-4991-4907-9154-9bd405f0af14__brand-radar-mentions-overview, mcp__1a081627-4991-4907-9154-9bd405f0af14__brand-radar-sov-overview, mcp__1a081627-4991-4907-9154-9bd405f0af14__brand-radar-cited-domains, mcp__1a081627-4991-4907-9154-9bd405f0af14__brand-radar-cited-pages, mcp__1a081627-4991-4907-9154-9bd405f0af14__brand-radar-ai-responses, mcp__1a081627-4991-4907-9154-9bd405f0af14__brand-radar-impressions-overview, mcp__1a081627-4991-4907-9154-9bd405f0af14__keywords-explorer-overview, mcp__1a081627-4991-4907-9154-9bd405f0af14__keywords-explorer-matching-terms, mcp__1a081627-4991-4907-9154-9bd405f0af14__serp-overview, mcp__1a081627-4991-4907-9154-9bd405f0af14__doc
---

# Brand Visibility Listicle Pipeline

Create data-driven articles about brand visibility in AI (ChatGPT, AI Overviews) for any industry and country, with TablePress-ready CSV tables enriched with keyword and SERP data.

## Input Format

```
/brand-visibility-listicle [sector] [brand1, brand2, ...] [country-code]
```

**Examples:**
```
/brand-visibility-listicle supermercados "Mercadona, Carrefour, Lidl, Dia, Alcampo, Aldi" ES
/brand-visibility-listicle streaming "Netflix, HBO Max, Disney+, Amazon Prime, Movistar Plus+" ES
/brand-visibility-listicle e-commerce "Mercado Livre, Amazon, Magazine Luiza, Shopee, Casas Bahia" BR
/brand-visibility-listicle 이커머스 "쿠팡, 네이버쇼핑, 11번가, G마켓, SSG닷컴" KR
```

**Parameters:**
- `sector` — Industry name (in the target language)
- `brands` — Comma-separated brand list (first brand = main brand for API calls)
- `country-code` — ISO 3166-1 alpha-2: ES, BR, MX, KR, US, FR, DE, etc.

## Language Configuration

The article language is determined by the country code. See `reference/language-config.md` for the full mapping. The skill automatically uses the correct language, number formatting, Ahrefs product URLs, and social links.

## Pipeline Overview

| Step | Sub-skill | Output |
|------|-----------|--------|
| 1 | **collect-data** | `1-data/[slug].json` — Raw data from Brand Radar + Keywords Explorer + SERP |
| 2 | **generate-tables** | `2-tables/[slug]/tabla-*.csv` — TablePress-ready CSV files |
| 3 | **write-article** | `3-article/[slug].html` — WordPress-ready article with shortcodes |
| 4 | **preview** | `4-preview/[slug].html` — Browser preview for review |

## Step-by-Step Execution

### Step 1: Collect Data (`skills/collect-data/SKILL.md`)

Pull data from 3 sources via Ahrefs MCP:

**A. Brand Radar** (per brand × per data_source):
- `brand-radar-mentions-overview` → total mentions per brand
- `brand-radar-sov-overview` → share of voice per brand
- Data sources: `chatgpt` and `google_ai_overviews`
- Filter by `country`

**B. Brand Radar Cited Domains:**
- `brand-radar-cited-domains` → top domains cited in AI responses for the sector
- Use `market` parameter with sector name

**C. Keywords Explorer:**
- `keywords-explorer-overview` → volume, KD, CPC, traffic_potential for 5-10 industry keywords
- `keywords-explorer-matching-terms` → discover related keywords with high volume

**D. SERP Overview (optional, for top 2-3 keywords):**
- `serp-overview` → who ranks #1-10 for key industry search terms

### Step 2: Generate Tables (`skills/generate-tables/SKILL.md`)

Create 4-6 CSV files for TablePress import:

| Table | Columns | Source |
|-------|---------|--------|
| tabla-1-chatgpt.csv | Brand, Mentions ChatGPT, Share of Voice | Brand Radar (chatgpt) |
| tabla-2-ai-overviews.csv | Brand, Mentions AI Overviews, Share of Voice | Brand Radar (google_ai_overviews) |
| tabla-3-cited-sources.csv | Cited Domain, Responses, Monthly Volume | Brand Radar cited-domains |
| tabla-4-comparison.csv | Brand, SOV ChatGPT, SOV AI Overviews, Mentions ChatGPT, Mentions AIO, Difference | Computed from tables 1+2 |
| tabla-5-keywords.csv | Keyword, Volume, KD, CPC, Traffic Potential, Has AI Overview | Keywords Explorer |
| tabla-6-serp.csv | Position, URL, Domain, DR, Traffic, Top Keyword | SERP Overview |

### Step 3: Write Article (`skills/write-article/SKILL.md`)

Generate the article HTML with WordPress shortcodes. Uses the reference article structure from existing Brand Radar articles.

### Step 4: Preview (`skills/preview/SKILL.md`)

Generate an HTML preview for browser review before WordPress upload.

## Resume Support

```
/brand-visibility-listicle --from=2 [slug]
```

Resume from any step. Earlier steps must have their output files present.

## Output Directory

All output goes to: `./brand-visibility-listicle/[slug]/`

```
brand-visibility-listicle/
└── [slug]/
    ├── 1-data/
    │   └── [slug].json
    ├── 2-tables/
    │   ├── tabla-1-chatgpt.csv
    │   ├── tabla-2-ai-overviews.csv
    │   ├── tabla-3-cited-sources.csv
    │   ├── tabla-4-comparison.csv
    │   ├── tabla-5-keywords.csv
    │   └── tabla-6-serp.csv
    ├── 3-article/
    │   └── [slug].html
    └── 4-preview/
        └── [slug].html
```
