# Skill: /localization-gaps — Localization Gap Analyzer

## Purpose
Identify content localization gaps by comparing top-performing pages across locales, finding where non-localized English pages are cannibalizing traffic from international users, and surfacing missing locale content.

## When to Trigger
- User asks about localization gaps or missing translations
- User wants to know which pages need localization
- User mentions "hreflang issues", "content gaps by country", "missing localized pages"
- User wants to audit their international content coverage

## Required Inputs
- **target**: The domain to analyze (e.g., `canva.com`)
- **countries**: List of country codes to compare (e.g., `de, fr, jp, br, es`)
- **date**: Analysis date

## Workflow

### Step 1: Pull Top Pages per Country
For each target country, use **Site Explorer - Top Pages**:
- Target: the domain
- Mode: `subdomains`
- Country: each country code
- Date: specified date
- Select: `url, traffic, keywords, top_keyword, top_keyword_volume`
- Order by: `traffic:desc`
- Limit: 30-50
- This gives you the highest-traffic pages per country

### Step 2: Identify Non-Localized Pages Getting Foreign Traffic
From the results in Step 1, flag any URLs that do NOT match the expected locale pattern.

Common locale URL patterns to check:
- Subdirectory: `/de/`, `/de_de/`, `/fr/`, `/ja_jp/`
- Subdomain: `de.example.com`, `fr.example.com`
- ccTLD: `example.de`, `example.fr`

If a page like `/en/ai-image-generator/` appears in the Germany results, that's an English page getting German traffic = localization gap.

### Step 3: Compare Locale Coverage
Build a matrix comparing which content exists across locales:

For each top-performing URL slug:
- Check if equivalent exists for each target locale
- Compare traffic between the localized version and the English version in that country

### Step 4: Pull Organic Keywords for Gap Pages
For specific gap pages found, use **Site Explorer - Organic Keywords**:
- Target: the specific non-localized URL
- Country: the foreign country where it's getting traffic
- Select: `keyword, position, volume, traffic`
- This reveals exactly which keywords foreign users are using to find the English page

### Step 5: Quantify the Gap
For each gap found, calculate:
- **Leaked traffic**: Traffic to English page from non-English country
- **Potential uplift**: If the localized version gets 2-3x the traffic of the English leak (typical), estimate the gain
- **Priority score**: Leaked traffic × potential multiplier × CPC (value-weighted)

## Output Format

### Localization Coverage Matrix

| Content/Page | EN (US) | DE | FR | JP | BR | ES |
|-------------|:-------:|:--:|:--:|:--:|:--:|:--:|
| AI Image Generator | ✅ 250K | ✅ 92K | ❌ | ✅ 45K | ⚠️ 12K (EN leak) | ✅ 38K |
| Logo Maker | ✅ 180K | ✅ 61K | ✅ 40K | ✅ 30K | ✅ 55K | ✅ 42K |
| Resume Templates | ✅ 320K | ✅ 106K | ⚠️ 8K (EN leak) | ❌ | ✅ 90K | ✅ 70K |

Legend: ✅ = Localized version exists | ❌ = No page exists | ⚠️ = English page getting foreign traffic

### Top Localization Gaps (Priority Order)

| Page | Country | English Page Traffic | Keywords Leaking | Est. Potential | Priority |
|------|---------|--------------------:|-----------------:|---------------:|----------|

### Leaked Keywords Detail
For each gap, show the actual keywords foreign users are searching:

| Keyword (Foreign) | Volume | Position | Traffic | Localized Equivalent Exists? |
|-------------------|-------:|---------:|-------:|-----|

### Recommendations
1. **Immediate localization priorities** — Ranked by leaked traffic × CPC value
2. **Hreflang audit flags** — Pages where both EN and locale versions exist but EN is still ranking in the foreign SERP
3. **Content creation opportunities** — Pages that don't exist in any locale yet but have foreign keyword demand
4. **Redirect recommendations** — Where to redirect English URLs for foreign users

## Example with Real Data (Canva.com — Germany)

**Top pages in Germany:**

| URL | Traffic (DE) | Keywords | Top Keyword |
|-----|------------:|---------:|-------------|
| /de_de/ | 1,511,670 | 4,063 | canva |
| /de_de/lebenslaeufe/vorlagen/ | 105,705 | 5,972 | lebenslauf vorlage |
| /de_de/ai-image-generator/ | 92,152 | 4,297 | ki bilder erstellen |
| /de_de/logos/ | 60,926 | 1,460 | logo erstellen |
| /ai-image-generator/ (English!) | 33,394 | 1,072 | ai image generator |
| /de_de/vorlagen/ | 47,431 | 11,945 | canva |
| /de_de/praesentationen/vorlagen/ | 15,826 | 3,686 | powerpoint vorlagen |

**Insight:** "The English `/ai-image-generator/` page is pulling 33K visits from Germany despite a localized `/de_de/ai-image-generator/` existing with 92K visits. This English leak suggests broken or missing hreflang tags. Fixing this alone could recover 20-30K visits. Also notable: `/de_de/praesentationen/vorlagen/` ranks for 'powerpoint vorlagen' — a competitor brand keyword opportunity."
