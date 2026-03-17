# Skill: /market-entry — Market Entry Readiness Report

## Purpose
Generate a comprehensive market entry readiness assessment for a specific country — combining keyword ownership analysis, competitor strength, brand search patterns, content readiness, and link authority to determine whether to enter, expand, or defend a market.

## When to Trigger
- User asks "should we enter the [country] market?"
- User wants a comprehensive market assessment for a specific country
- User mentions "market entry", "market readiness", "go-to-market SEO"
- User needs a business case for localization investment in a new market

## Required Inputs
- **target**: The domain to analyze (e.g., `canva.com`)
- **country**: The target market country code (e.g., `jp`, `de`, `br`)
- **date**: Analysis date
- **Optional**: competitor domains to benchmark against

## Workflow

### Step 1: Current Market Position
Use **Site Explorer - Metrics**:
- Target: the domain
- Country: target country
- Date: specified date
- Get: organic traffic, organic keywords, traffic value, paid traffic

Use **Site Explorer - Metrics by Country**:
- Target: the domain
- Date: specified date
- Get the target country's row for comparison against all other countries

### Step 2: Keyword Ownership Depth
Use **Site Explorer - Organic Keywords**:
- Target: the domain
- Mode: `subdomains`
- Country: target country
- Date: specified date
- Select: `keyword, position, volume, traffic, url, best_position_url`
- Order by: `traffic:desc`
- Limit: 30
- Analyze: How many #1 positions? How many page 1? Keyword diversity?

### Step 3: Brand Search Analysis
Use **Keywords Explorer - Volume by Country**:
- Keyword: the brand name
- Check the target country's branded search volume

Use **Keywords Explorer - Volume History**:
- Keyword: brand name
- Country: target country
- Date range: last 12-24 months
- Is brand awareness growing in this market?

Also check for local script variations (e.g., Japan: katakana, hiragana):
- Run additional Volume by Country queries for each script variation

### Step 4: Competitive Landscape
Use **Site Explorer - Organic Competitors**:
- Target: the domain
- Country: target country
- Date: specified date
- Select: `domain, common_keywords, organic_traffic, organic_keywords`
- Order by: `common_keywords:desc`
- Limit: 15

### Step 5: Content Readiness
Use **Site Explorer - Top Pages**:
- Target: the domain (and locale-specific path if exists)
- Country: target country
- Date: specified date
- Select: `url, traffic, keywords, top_keyword, top_keyword_volume`
- Order by: `traffic:desc`
- Limit: 30
- Assess: Do localized pages exist? What % of traffic goes to localized vs. English pages?

### Step 6: Link Authority in Market
Use **Site Explorer - Referring Domains**:
- Target: locale-specific path (e.g., `/ja_jp/`)
- Mode: `prefix`
- Select: `domain, domain_rating, links_to_target`
- Order by: `domain_rating:desc`
- Limit: 15

### Step 7: Domain Rating Trend
Use **Site Explorer - Domain Rating History**:
- Target: the domain
- Date range: last 12 months
- Is overall authority growing?

### Step 8: Market Demand Assessment
Use **Keywords Explorer - Matching Terms**:
- Keywords: core category terms in LOCAL language
- Country: target country
- Select: `keyword, volume, difficulty, cpc, traffic_potential`
- Order by: `volume:desc`
- Limit: 20

## Scoring Framework

Rate each dimension 1-5 and calculate an overall readiness score:

| Dimension | Weight | Score (1-5) | Criteria |
|-----------|--------|-------------|----------|
| **Brand Awareness** | 20% | | Branded search volume > 100K = 5, > 50K = 4, > 10K = 3, > 1K = 2, < 1K = 1 |
| **Keyword Ownership** | 20% | | % of target keywords in top 10: >60% = 5, >40% = 4, >20% = 3, >10% = 2, <10% = 1 |
| **Content Readiness** | 15% | | Full locale = 5, Partial = 3, None = 1 |
| **Competitive Intensity** | 15% | | Few strong local competitors = 5, Many strong = 1 |
| **Link Authority** | 15% | | Local referring domains: >5K = 5, >1K = 4, >500 = 3, >100 = 2, <100 = 1 |
| **Market Size** | 15% | | Total addressable search volume for category keywords |

**Overall Score**: Weighted average
- **4.0-5.0**: Fortress Market — Defend and expand
- **3.0-3.9**: Growth Market — Invest aggressively
- **2.0-2.9**: Opportunity Market — Strategic entry with focused content
- **1.0-1.9**: Exploration Market — Test with minimal investment first

## Output Format

### Market Entry Report: [Country Name]

#### Executive Summary
[2-3 sentence verdict on market readiness]

#### Readiness Scorecard

| Dimension | Score | Evidence |
|-----------|------:|---------|
| Brand Awareness | X/5 | [key metric] |
| Keyword Ownership | X/5 | [key metric] |
| Content Readiness | X/5 | [key metric] |
| Competitive Intensity | X/5 | [key metric] |
| Link Authority | X/5 | [key metric] |
| Market Size | X/5 | [key metric] |
| **Overall** | **X.X/5** | **[Classification]** |

#### Brand Search Demand
- Brand volume in [country]: [number]
- Local script variations: [if applicable]
- Trend: [Growing/Stable/Declining] ([% change over period])

#### Keyword Position Summary

| Keyword | Position | Volume | Traffic | URL |
|---------|--------:|-------:|-------:|-----|

#### Content Localization Status
- Locale path: [e.g., /ja_jp/ or N/A]
- Localized pages: [number]
- % of traffic to localized pages: [%]
- % of traffic to English pages: [%] (= localization gap)

#### Competitive Landscape

| Competitor | Type | Common KWs | Their Traffic | Threat Level |
|-----------|------|----------:|-------------:|-------------|

#### Market Demand (Top Category Keywords)

| Keyword (Local Language) | Volume | KD | CPC | Traffic Potential |
|-------------------------|-------:|---:|----:|------------------:|

### Strategic Recommendation

**Verdict**: [Enter / Expand / Defend / Wait]

**Immediate actions** (next 30 days):
1. [action]
2. [action]

**Short-term** (30-90 days):
1. [action]
2. [action]

**Long-term** (90-180 days):
1. [action]
2. [action]

**Estimated investment**: [Low / Medium / High]
**Expected timeline to ROI**: [months]

## Example with Real Data (Canva.com — Japan)

**Readiness Score: 4.7/5 — Fortress Market**

Top keywords owned:

| Keyword | Position | Volume | Traffic | URL |
|---------|--------:|-------:|-------:|-----|
| canva | 1 | 1,480,000 | 1,571,490 | /ja_jp/ |
| キャンバ (katakana) | 1 | 920,000 | 927,787 | /ja_jp/ |
| きゃんば (hiragana) | 1 | 72,000 | 75,139 | /ja_jp/ |
| ai 画像生成 | 1 | 91,000 | 33,037 | /ja_jp/ai-image-generator/ |
| 画像生成 ai | 1 | 72,000 | 29,720 | /ja_jp/ai-image-generator/ |
| canva ログイン | 1 | 42,000 | 32,714 | /ja_jp/login/ |
| canva 使い方 | 1 | 21,000 | 22,959 | /ja_jp/learn/how-to/ |
| aiイラスト | 1 | 58,000 | 21,189 | /ja_jp/features/ai-illust-generate/ |

**Insight:** "Japan is a Fortress Market (4.7/5). Canva owns #1 for ALL top queries including brand searches in three scripts — Latin (1.48M), katakana (920K), and hiragana (72K) — totaling 2.5M+ branded searches/month. AI image generation pages rank #1 for both 'ai 画像生成' and '画像生成 ai' (word order variants). Recommendation: DEFEND. Shift from localization to non-branded keyword expansion — target 'ポスター作成', 'プレゼンテーションテンプレート' to capture more top-of-funnel."
