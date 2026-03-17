# Skill: /intl-backlinks — International Link Building Intelligence

## Purpose
Analyze a domain's backlink profile with an international lens — identifying referring domains by country/language, finding broken backlinks to reclaim, discovering link building opportunities in target markets, and benchmarking link authority across locales.

## When to Trigger
- User asks about international link building opportunities
- User wants to analyze backlinks by country or language
- User mentions "broken backlinks", "link reclamation", "international link building"
- User wants to find referring domains in specific markets

## Required Inputs
- **target**: The domain to analyze (e.g., `canva.com`)
- **Optional**: specific locale subdirectories to compare (e.g., `/de_de/`, `/fr_fr/`, `/ja_jp/`)

## Workflow

### Step 1: Get Overall Backlink Stats
Use **Site Explorer - Backlinks Stats**:
- Target: the domain
- Mode: `subdomains`
- This gives total backlinks, referring domains, dofollow ratio

### Step 2: Pull Top Referring Domains
Use **Site Explorer - Referring Domains**:
- Target: the domain
- Mode: `subdomains`
- Select: `domain, domain_rating, links_to_target, dofollow_links, first_seen, last_seen`
- Order by: `domain_rating:desc`
- Limit: 30

### Step 3: Find Broken Backlinks
Use **Site Explorer - Broken Backlinks**:
- Target: the domain
- Mode: `subdomains`
- Select: `url_from, url_to, domain_rating_source, anchor, first_seen, http_code`
- Order by: `domain_rating_source:desc`
- Limit: 30
- Focus on high-DR sources linking to broken pages

### Step 4: Analyze Locale-Specific Backlinks
For each target locale subdirectory, use **Site Explorer - Referring Domains**:
- Target: `domain.com/de_de/` (or the locale pattern)
- Mode: `prefix`
- Select: `domain, domain_rating, links_to_target, first_seen`
- Order by: `domain_rating:desc`
- Limit: 20
- This reveals which domains link to each locale specifically

### Step 5: Referring Domains History
Use **Site Explorer - Refdomains History**:
- Target: the domain
- Date range: last 12 months
- This shows if international link building is growing or declining

### Step 6: Anchor Text Analysis
Use **Site Explorer - Anchors**:
- Target: the domain
- Mode: `subdomains`
- Select: `anchor, dofollow_links, linked_pages`
- Order by: `dofollow_links:desc`
- Limit: 30
- Look for anchors in different languages — indicates international editorial links

### Step 7: Classify and Recommend

Analyze referring domains to identify:

1. **Global Authority Links** — DR 80+ domains linking across multiple locales
2. **Locale-Specific Links** — Domains that only link to one locale (e.g., German news sites linking to /de_de/)
3. **Broken Link Recovery** — High-DR broken backlinks that can be reclaimed via 301 redirects
4. **Localized Anchor Patterns** — Anchor text in different languages indicating organic international coverage
5. **Link Gaps by Locale** — Locales with significantly fewer referring domains

## Output Format

### Backlink Overview
- Total Backlinks: [number]
- Referring Domains: [number]
- Dofollow Ratio: [percentage]

### Top Referring Domains (Global)

| Domain | DR | Links | Dofollow | First Seen | Language/Region |
|--------|---:|------:|---------:|------------|-----------------|

### Backlinks by Locale

| Locale | Referring Domains | Total Backlinks | Avg DR | Top Referring Domain |
|--------|------------------:|--------------:|-------:|---------------------|

### Broken Backlinks to Reclaim (Priority)

| Source Domain | DR | Broken URL | Anchor Text | Recommended Redirect |
|--------------|---:|-----------|-------------|---------------------|

### International Anchor Text Distribution

| Language | Top Anchors | Total Links | % of Total |
|----------|------------|------------:|-----------:|

### Link Building Recommendations

1. **Immediate reclamation** — Broken links from DR 80+ sites, with redirect targets
2. **Locale link gap priorities** — Which locales need more link building effort
3. **Outreach targets** — High-DR domains linking to competitors but not to you in each market
4. **Content for links** — Topics that naturally attract links in each market

## Example with Real Data (Canva.com)

**Top referring domains:**

| Domain | DR | Links to Canva | First Seen |
|--------|---:|---------------:|-----------:|
| youtube.com | 99 | 29,725 | Apr 2015 |
| google.com | 99 | 2,159 | Apr 2014 |
| linkedin.com | 99 | 65 | Oct 2014 |
| apple.com | 97 | 1,308 | Nov 2014 |
| wikipedia.org | 97 | 216 | Aug 2015 |
| tiktok.com | 97 | 110 | Sep 2021 |
| shopify.com | 96 | 4,020 | Nov 2015 |
| pinterest.com | 96 | 2,063 | Dec 2014 |
| github.com | 96 | 733 | May 2020 |
| europa.eu | 96 | 12 | Dec 2023 |

**Broken backlinks from DR 99 sites (reclaimable):**
- youtube.com → `/p/templates/EAE..` (deleted template page)
- youtube.com → `/brand/brand-tem..` (deleted brand page)
- youtube.com → `/zh_tw/help/keyboard-shortcuts/` (deleted localized help page)

**Insight:** "Canva has broken backlinks from YouTube (DR 99) pointing to deleted template pages and a zh_tw localized help page. Redirecting these broken URLs to live equivalents would recover link equity from the highest-DR site on the internet. The europa.eu link (DR 96, first seen Dec 2023) is a recent acquisition — indicating Canva is gaining government/institutional authority."
