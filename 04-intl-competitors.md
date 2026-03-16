# Skill: /intl-competitors — Competitor International Benchmarking

## Purpose
Identify and analyze organic search competitors in specific international markets, revealing local competitors that don't appear in your home market and benchmarking your international SEO performance against them.

## When to Trigger
- User asks "who are our competitors in [country]?"
- User wants competitive analysis for a specific international market
- User mentions "international competitors", "local competitors", "competitive benchmarking"
- User wants to understand competitive landscape before entering a market

## Required Inputs
- **target**: The domain to analyze (e.g., `canva.com`)
- **countries**: One or more country codes (e.g., `de, fr, jp`)
- **date**: Analysis date

## Workflow

### Step 1: Pull Organic Competitors per Country
For each country, use **Site Explorer - Organic Competitors**:
- Target: the domain
- Mode: `subdomains`
- Country: each country code
- Date: specified date
- Select: `domain, common_keywords, keywords_unique_to_target, organic_traffic, organic_keywords, keywords_unique_to_competitor`
- Order by: `common_keywords:desc`
- Limit: 20

### Step 2: Get Competitor Domain Ratings
For the top 5-10 competitors per country, use **Site Explorer - Domain Rating**:
- Target: each competitor domain
- Date: specified date
- This adds authority context to the competitive landscape

### Step 3: Get Competitor Metrics in That Country
For the most interesting competitors (especially local/unknown ones), use **Site Explorer - Metrics**:
- Target: competitor domain
- Country: the specific country
- Date: specified date
- This shows their country-specific traffic, keywords, and value

### Step 4: Identify Content Overlap
For key competitors, use **Site Explorer - Top Pages**:
- Target: competitor domain
- Country: the specific country
- Date: specified date
- Select: `url, traffic, keywords, top_keyword, top_keyword_volume`
- Limit: 15
- This reveals WHAT content they're winning with in that market

### Step 5: Classify Competitors

Categorize each competitor as:

1. **Global Giants** — Also compete with you in your home market (e.g., adobe.com)
2. **Local Champions** — Strong in this specific country but not a global competitor (e.g., vistaprint.de in Germany)
3. **Category Specialists** — Compete on a subset of your keywords in a niche (e.g., pdf24.org for PDF keywords)
4. **Rising Threats** — Lower traffic but growing keyword overlap
5. **Unexpected Competitors** — Domains you wouldn't expect (educational, government, different industry)

## Output Format

### Competitive Landscape: [Country Name]

#### Your Position
- Organic Traffic ([country]): [number]
- Organic Keywords ([country]): [number]
- Traffic Value ([country]): [value]

#### Top Competitors

| Competitor | Type | Common KWs | Their Traffic | Their KWs | DR | Unique KWs (Theirs) |
|-----------|------|----------:|-------------:|----------:|---:|-------------------:|

### Competitor Deep Dives

For the top 3 most interesting competitors:

#### [Competitor Name] — [Type]
- **Why they matter**: [1-2 sentences]
- **Their top content in this market**:

| URL | Traffic | Keywords | Top Keyword |
|-----|--------:|---------:|-------------|

- **Keywords they rank for that you don't**: [list top opportunities]
- **Your advantage**: [what you have that they don't]

### Strategic Recommendations

1. **Content gaps to fill** — Topics where competitors dominate and you have no content
2. **Local competitors to study** — Their localization approach, local partnerships, local content
3. **Defensive priorities** — Where competitors are encroaching on your strongest keywords
4. **Link building targets** — Referring domains linking to competitors but not to you

## Example with Real Data (Canva.com — Germany)

| Competitor | Common KWs | Their Traffic | Their KWs | Type |
|-----------|----------:|-------------:|----------:|------|
| adobe.com | 133,927 | 3,397,441 | 453,468 | Global Giant |
| fotor.com | 23,576 | 81,241 | 9,835 | Global Competitor |
| capcut.com | 20,768 | 238,539 | 10,579 | Category Specialist |
| wix.com | 17,117 | 259,081 | 29,055 | Global Giant |
| pixlr.com | 15,853 | 81,724 | 6,420 | Category Specialist |
| vistaprint.de | 14,783 | 202,020 | 18,486 | Local Champion |
| pdf24.org | 14,286 | 1,203,158 | 22,548 | Category Specialist |

**Insight:** "In Germany, Adobe shares 134K keywords with Canva — massive overlap but expected. The surprise is **pdf24.org** — a local German tool with 1.2M traffic and 14K common keywords, dominating PDF-related queries. Canva's PDF features compete directly but aren't well-optimized for German search terms. Also, **vistaprint.de** (a German-specific domain) captures 'visitenkarten erstellen' (business card design) traffic that Canva could own. Recommendation: Create dedicated German-language landing pages for PDF and business card use cases."
