# Skill: /market-discovery — International Market Discovery

## Purpose
Analyze a domain's organic search performance across all countries to identify the best markets for expansion, localization investment, and resource allocation.

## When to Trigger
- User asks "where should we expand next?"
- User asks about international opportunities for a domain
- User wants to prioritize markets for localization
- User mentions "market discovery", "market analysis", "international expansion"

## Required Inputs
- **target**: The domain to analyze (e.g., `canva.com`)
- **date**: Analysis date in YYYY-MM-DD format (default: most recent available)

## Workflow

### Step 1: Get Domain Authority Baseline
Use the **Site Explorer - Domain Rating** endpoint:
- Target: the domain
- Date: specified date
- This gives you DR and global Ahrefs Rank as a baseline

### Step 2: Pull Metrics by Country
Use the **Site Explorer - Metrics by Country** endpoint:
- Target: the domain
- Mode: `subdomains` (IMPORTANT: always use subdomains for domain-level analysis)
- Date: specified date
- Select: `country, organic_traffic, organic_keywords, organic_cost, paid_traffic, paid_keywords, paid_cost`

### Step 3: Pull Overall Metrics
Use the **Site Explorer - Metrics** endpoint for top countries individually to get deeper data:
- Target: the domain
- Country: each top country code
- Date: specified date

### Step 4: Analyze & Recommend

For each country in the results, calculate and present:

1. **Traffic Volume** — Raw organic traffic
2. **Traffic Value** — Estimated cost if traffic were paid (organic_cost)
3. **Value per Visit** — Traffic Value ÷ Traffic Volume (monetization efficiency)
4. **Keyword Coverage** — Number of organic keywords ranked
5. **Keywords per 1K Traffic** — Keyword diversity ratio

#### Market Classification Framework:
- **Fortress Markets** (High traffic + High value): Already strong, maintain and defend
- **Growth Markets** (High traffic + Low value): Volume exists but monetization is low — optimize conversion
- **Premium Markets** (Low traffic + High value): Each visit is valuable — invest in content to grow volume
- **Opportunity Markets** (Low traffic + Low value): Early stage — evaluate if worth entering

## Output Format

Present results as:

### Domain Overview
- Domain: [domain]
- Domain Rating: [DR]
- Global Rank: [rank]

### Top Markets by Traffic

| Rank | Country | Traffic | Keywords | Traffic Value | Value/Visit | Classification |
|------|---------|--------:|---------:|--------------:|------------:|----------------|

### Recommendations
For each market classification, provide 2-3 actionable recommendations:
- Which markets to prioritize for localization
- Which markets have untapped potential (high keyword count but low traffic = ranking poorly)
- Which markets show paid traffic but low organic (competitor-heavy, needs SEO investment)

### Seasonal Note
Flag any markets where traffic may be seasonal (e.g., Southern Hemisphere has opposite academic/business cycles)

## Example with Real Data (Canva.com)

**Domain Rating:** 93 | **Ahrefs Rank:** #219

| Country | Traffic | Keywords | Traffic Value | Value/Visit | Classification |
|---------|--------:|---------:|--------------:|------------:|----------------|
| US | 37,232,899 | 3,216,412 | $1,758M | $47.22 | Fortress |
| India | 26,595,469 | 1,398,011 | $78M | $2.93 | Growth |
| Brazil | 24,889,653 | 1,102,737 | $69M | $2.77 | Growth |
| Mexico | 20,141,390 | 911,041 | $106M | $5.27 | Growth/Premium |
| Spain | 15,480,531 | 520,624 | $98M | $6.33 | Premium |
| Indonesia | 15,295,141 | 758,691 | $51M | $3.33 | Growth |

**Insight:** "Brazil has 25M organic visits but only $69M traffic value ($2.77/visit), while Mexico has 20M visits at $106M value ($5.27/visit). Mexico yields nearly 2x the value per visit — prioritize Mexico for paid+organic campaigns, Brazil for volume-based organic growth."
