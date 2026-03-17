# Skill: /intl-tech-audit — International Technical SEO Audit

## Purpose
Audit the technical SEO health of a website's international implementation — analyzing internal linking across locales, hreflang consistency, locale URL structure, and crawl issues specific to multi-language/multi-region sites.

## When to Trigger
- User asks about technical SEO for international sites
- User mentions "hreflang", "internal linking by locale", "international site structure"
- User wants to audit their multi-language site setup
- User asks about crawl issues on localized pages

## Required Inputs
- **target**: The domain to analyze (e.g., `canva.com`)
- **project_id**: Site Audit project ID (if available, for crawl-level data)
- **locales**: List of locale paths/subdomains to compare (e.g., `/de_de/, /fr_fr/, /ja_jp/, /pt_br/`)

## Workflow

### Step 1: Internal Anchor Text Analysis
Use **Site Explorer - Linked Anchors Internal**:
- Target: the domain
- Mode: `subdomains`
- Select: `anchor, links_from_target, linked_pages, dofollow_links`
- Order by: `links_from_target:desc`
- Limit: 50
- Look for anchor text in different languages — reveals locale navigation structure

### Step 2: Internal Link Distribution by Locale
For each locale path, use **Site Explorer - Pages by Internal Links**:
- Target: `domain.com/de_de/` (each locale)
- Mode: `prefix`
- Select: `url, links_to_page, internal_links_count`
- Order by: `links_to_page:desc`
- Limit: 20
- Compare internal link counts across locales to find underlinked locales

### Step 3: Crawl Issues (if Site Audit project exists)
Use **Site Audit - Issues**:
- Project ID: the project
- Look for issues related to:
  - Hreflang errors
  - Duplicate content across locales
  - Missing hreflang return tags
  - Orphan pages in locale subdirectories
  - Redirect chains involving locale switches

### Step 4: Page Explorer for Locale Pages
Use **Site Audit - Page Explorer**:
- Project ID: the project
- Filter for locale-specific URL patterns
- Select relevant technical metrics
- Look for HTTP status codes, canonical issues, indexability

### Step 5: Page Content Check (Spot Check)
Use **Site Audit - Page Content**:
- For key pages across locales, check:
  - Title tags (are they localized?)
  - Meta descriptions (translated or English?)
  - H1 tags (matching locale?)
  - Hreflang declarations present?

### Step 6: External Anchor Text Analysis
Use **Site Explorer - Linked Anchors External**:
- Target: the domain
- Mode: `subdomains`
- Select: `anchor, dofollow_links, linked_pages`
- Order by: `dofollow_links:desc`
- Limit: 30
- Check if external sites link using localized anchor text

### Step 7: Linked Domains (Outbound)
Use **Site Explorer - Linked Domains**:
- Target: locale-specific paths
- This reveals if different locales link out to different external resources

## Analysis Framework

Check for these common international technical SEO issues:

1. **Internal Link Equity Distribution** — Are all locales getting proportional internal links?
2. **Anchor Text Localization** — Are internal anchors translated or still in English?
3. **Orphan Locale Pages** — Pages in locale directories with zero or very few internal links
4. **Hreflang Completeness** — Do all pages have proper hreflang annotations?
5. **Canonical Conflicts** — Self-referencing canonicals per locale vs. cross-locale canonicals
6. **Crawl Budget Waste** — Locale pages returning errors, redirect chains, or soft 404s
7. **Content Parity** — Locales with significantly fewer indexed pages

## Output Format

### International Architecture Overview

| Locale | URL Pattern | Pages Indexed | Avg Internal Links/Page | Top Anchor Language |
|--------|------------|-------------:|----------------------:|---------------------|

### Internal Link Equity Distribution

| Anchor Text | Language | Links | Pages Linked | Locales Using |
|-------------|----------|------:|-----------:|---------------|

### Technical Issues by Locale

| Issue Type | EN | DE | FR | JP | BR | ES |
|-----------|---:|---:|---:|---:|---:|---:|
| Hreflang errors | | | | | | |
| Orphan pages | | | | | | |
| Redirect chains | | | | | | |
| Missing canonicals | | | | | | |
| Duplicate content | | | | | | |

### Internal Link Gap Analysis

| Locale | Pages with < 5 Internal Links | % of Locale | vs. EN Average |
|--------|-----------------------------:|-----------:|---------------|

### Recommendations (Priority Order)

1. **Critical fixes** — Hreflang errors, broken locale pages, canonical conflicts
2. **Internal linking improvements** — Underlinked locales needing navigation updates
3. **Anchor text localization** — English anchors pointing to non-English pages
4. **Crawl budget optimization** — Reducing error pages, redirect chains in locale directories
5. **Content parity** — Locales missing significant numbers of pages vs. English version
6. **Architecture improvements** — Structural changes to improve locale discoverability

## Example with Real Data (Canva.com — Internal Anchors)

| Anchor Text | Language | Links | Pages Linked |
|-------------|----------|------:|-----------:|
| *(empty/image)* | N/A | 949,888 | 699,698 |
| Logos | English | 500,220 | 66 |
| Docs | English | 487,452 | 30 |
| Flyers | English | 384,266 | 27 |
| Case studies | English | 326,504 | 11 |
| CV | English | 311,863 | 37 |
| Historias de éxito | Spanish | 285,600 | 9 |
| 活用事例 | Japanese | 277,203 | 6 |
| Marketing | English | 277,359 | 96 |

**Insight:** "Canva's top internal anchor texts are English ('Logos' 500K links, 'Docs' 487K links). Localized anchors like 'Historias de éxito' (ES, 285K) and '活用事例' (JP, 277K) are 40% lower — showing uneven internal link equity distribution. Additionally, 950K internal links use empty/image-based anchors — missed opportunities for localized anchor text. Recommendation: Ensure global navigation distributes equal internal links to all locales."
