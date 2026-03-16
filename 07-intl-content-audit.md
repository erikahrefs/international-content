# Skill: /intl-content-audit — International Content Performance Audit

## Purpose
Audit content performance across international markets by analyzing search volume trends, keyword history, traffic patterns, and page performance over time — identifying seasonal patterns, growth trajectories, and content that needs refreshing in specific locales.

## When to Trigger
- User asks about content performance in international markets
- User wants to track branded or non-branded search trends by country
- User mentions "content audit", "seasonal trends", "search demand trends"
- User wants to know how their content performs across different markets over time

## Required Inputs
- **target**: The domain to analyze (e.g., `canva.com`)
- **keywords**: Key branded and non-branded terms to track
- **countries**: Country codes to analyze (e.g., `br, de, jp, fr`)
- **date_range**: Start and end dates for trend analysis (recommend 12-24 months)

## Workflow

### Step 1: Branded Search Volume Trends
For each country, use **Keywords Explorer - Volume History**:
- Keyword: the brand name
- Country: each target country
- Date range: specified range
- This reveals brand awareness trends by market

### Step 2: Non-Branded Keyword Trends
For key non-branded terms, use **Keywords Explorer - Volume History**:
- Keyword: each category keyword (in the local language)
- Country: each target country
- Date range: specified range
- This shows market demand trends independent of brand

### Step 3: Organic Keywords History
Use **Site Explorer - Keywords History**:
- Target: the domain
- Country: each target country
- Date range: specified range
- Select: available position range metrics
- History grouping: `monthly`
- This shows how many keywords you rank for over time by position bucket

### Step 4: Top Pages Performance Over Time
Use **Site Explorer - Pages History**:
- Target: the domain
- Country: each target country (if supported)
- Date range: specified range
- History grouping: `monthly`

### Step 5: Total Search Volume History
Use **Site Explorer - Total Search Volume History**:
- Target: the domain
- Country: each target country
- Date range: specified range
- This shows the total search volume of all keywords you rank for

### Step 6: Current Top Pages Snapshot with Comparison
Use **Site Explorer - Top Pages**:
- Target: the domain (or locale-specific path)
- Country: each target country
- Date: most recent
- Date compared: 6 months ago
- Select: `url, traffic, keywords, top_keyword, top_keyword_volume`
- Limit: 30
- Shows which pages are growing vs. declining

## Analysis Framework

For each market, analyze:

1. **Brand Demand Trajectory** — Is branded search growing, flat, or declining?
2. **Seasonality Patterns** — Monthly peaks/troughs (map to local events, holidays, academic calendar)
3. **Ranking Progress** — Are you gaining or losing keyword positions?
4. **Content Freshness** — Pages that have lost traffic (need refresh)
5. **Emerging Topics** — Keywords with rising search volume in that market
6. **Market Maturity** — Where you are in the growth curve per country

## Output Format

### Brand Search Demand by Market

| Month | US | BR | DE | JP | FR |
|-------|---:|---:|---:|---:|---:|
| [monthly data] |

### Seasonality Calendar
For each market, note:
- Peak months and likely cause (back to school, business cycles, holidays)
- Dip months and recovery patterns
- Optimal content publishing windows

### Keyword Ranking Progress

| Country | KWs in Top 3 | KWs 4-10 | KWs 11-50 | Trend (6mo) |
|---------|-------------:|----------:|----------:|-------------|

### Content Performance Changes (Top Pages)

| Page | Country | Current Traffic | Traffic 6mo Ago | Change | Action |
|------|---------|---------------:|----------------:|-------:|--------|

Actions: 🟢 Growing | 🟡 Stable | 🔴 Declining — Refresh | 🆕 New

### Recommendations

1. **Content refresh priorities** — Pages losing traffic in specific markets
2. **Seasonal content calendar** — When to publish/promote for each market
3. **Growth markets** — Countries where keyword rankings are expanding fastest
4. **At-risk markets** — Countries where rankings or brand search are declining
5. **Content gap fillers** — Rising search trends you don't yet have content for

## Example with Real Data (Canva — "canva" brand search in Brazil)

| Month | Search Volume |
|-------|-------------:|
| Jan 2024 | 9,080,955 |
| Mar 2024 | 13,143,901 |
| Jun 2024 | 13,092,155 |
| Sep 2024 | 15,862,163 |
| Nov 2024 | 16,030,027 |
| Dec 2024 | 12,399,709 |
| Mar 2025 | **16,798,265** |

**Insight:** "Branded search for 'canva' in Brazil has grown 85% in 14 months (9M → 16.8M). There's a clear seasonal dip in Dec/Jan (Brazilian summer holidays) followed by rapid recovery. Content publishing should front-load Q1 to capture the post-holiday surge. Meanwhile, in Germany, branded search has plateaued at ~1.5M/month for 6 months — indicating market saturation for brand-aware users. German strategy should shift from brand awareness to non-branded keyword capture."
