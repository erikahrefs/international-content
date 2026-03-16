# Skill: /intl-keywords — International Keyword Research

## Purpose
Discover keyword opportunities in specific international markets using native-language terms, comparing volume, difficulty, and CPC across countries to find the best content opportunities for localization.

## When to Trigger
- User asks for keyword research in a specific country or language
- User wants to find localized keyword opportunities
- User mentions "international keywords", "local keywords", "keyword translation"
- User wants to compare keyword demand across markets

## Required Inputs
- **keywords**: Seed keywords in the target language (comma-separated)
- **country**: ISO country code (e.g., `es` for Spain, `de` for Germany, `br` for Brazil, `jp` for Japan)
- **Optional**: `limit` (default 20), comparison country codes

## Workflow

### Step 1: Get Matching Terms (Native Language)
Use **Keywords Explorer - Matching Terms**:
- Keywords: seed keywords in the LOCAL language
- Country: target country code
- Select: `keyword, volume, difficulty, cpc, global_volume, traffic_potential`
- Order by: `volume:desc`
- Limit: 20-30

### Step 2: Get Related Terms
Use **Keywords Explorer - Related Terms**:
- Keywords: same seed keywords
- Country: target country code
- Select: `keyword, volume, difficulty, cpc, traffic_potential`
- Order by: `volume:desc`
- This surfaces "also rank for" and "also talk about" terms the user may not have considered

### Step 3: Get Search Suggestions
Use **Keywords Explorer - Search Suggestions**:
- Keywords: same seed keywords
- Country: target country code
- Select: `keyword, volume, difficulty, cpc`
- These are autocomplete-style suggestions real users type

### Step 4: Cross-Country Volume Comparison
For the top 5-10 keywords found, use **Keywords Explorer - Volume by Country**:
- Keyword: each top keyword
- This shows where else in the world that keyword has demand

### Step 5: Volume Trend Check
For the top 3-5 keywords, use **Keywords Explorer - Volume History**:
- Keyword: each keyword
- Country: target country
- Date range: last 12 months
- Identify trending up vs. declining keywords

### Step 6: Analyze & Categorize

Categorize keywords into:

1. **Quick Wins** — High volume + Low difficulty (KD < 30) + Reasonable CPC
2. **Strategic Targets** — High volume + Medium difficulty (KD 30-60) — need strong content
3. **Long-tail Gold** — Lower volume but very low difficulty (KD < 10) — easy to rank
4. **Expensive but Worth It** — High CPC keywords indicating commercial intent
5. **Trending** — Keywords with increasing search volume over last 6 months
6. **Cross-Market** — Keywords with significant volume in multiple countries (localization leverage)

## Output Format

### Market: [Country Name] ([country code])

#### Quick Wins (KD < 30, Volume > 500)
| Keyword | Volume | KD | CPC | Global Volume | Trend |
|---------|-------:|---:|----:|--------------:|-------|

#### Strategic Targets (KD 30-60)
| Keyword | Volume | KD | CPC | Traffic Potential | Trend |
|---------|-------:|---:|----:|------------------:|-------|

#### Long-tail Opportunities (KD < 10)
| Keyword | Volume | KD | CPC | Notes |
|---------|-------:|---:|----:|-------|

#### Cross-Market Keywords
| Keyword | [Country A] Vol | [Country B] Vol | [Country C] Vol | Global |
|---------|----------------:|----------------:|----------------:|-------:|

### Content Recommendations
- Map each keyword cluster to a content type (blog post, landing page, tool page, template page)
- Note which keywords indicate different search intent per market
- Flag keywords where the English equivalent also has volume (mixed-language opportunity)

## Example with Real Data (Spain — "diseño grafico" cluster)

| Keyword (ES) | Volume | KD | CPC | Global Volume | Category |
|--------------|-------:|---:|----:|--------------:|----------|
| diseño grafico | 8,800 | 26 | $0.60 | 117,000 | Quick Win |
| diseño grafico carrera | 600 | 1 | $1.10 | 13,000 | Long-tail Gold |
| diseño grafico online | 350 | 16 | $1.70 | 1,500 | Quick Win |
| ia diseño grafico | 300 | 39 | $0.30 | 900 | Strategic/Trending |
| curso diseño grafico | 600 | 53 | $1.60 | 2,600 | Strategic Target |
| agencia diseño grafico | 300 | 0 | $0.80 | 800 | Long-tail Gold |

**Cross-market comparison (Germany — same concepts, English terms):**

| Keyword (DE) | Volume | KD | CPC | Traffic Potential |
|--------------|-------:|---:|----:|------------------:|
| canva | 1,540,000 | 11 | $0.06 | 1,490,000 |
| logo maker | 12,000 | 28 | $0.20 | 7,500 |
| graphic design | 4,900 | 22 | $0.90 | 2,200 |
| poster maker | 400 | 33 | $0.80 | 3,400 |

**Insight:** "In Spain, 'ia diseño grafico' (AI graphic design) has 300 monthly searches at KD 39 — a rising trend tied to AI adoption. The English equivalent is barely searched in Spain (< 50/mo), confirming users search in Spanish. In Germany however, 'logo maker' (English, 12K volume) outperforms the German 'Logo erstellen' — indicating Germans often search design terms in English. Localization strategy: Spanish-first for Spain, bilingual for Germany."
