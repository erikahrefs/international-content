---
name: write-article
description: Generate a WordPress-ready article with shortcodes from the table data and JSON source
argument-hint: [slug]
allowed-tools: Read, Write, Bash
---

# Write Article Sub-skill

Generate a complete WordPress-ready article in the target language with Ahrefs shortcodes and TablePress references.

## Input

- `1-data/[slug].json` — Raw data
- `2-tables/[slug]/tabla-*.csv` — Generated table CSVs
- `reference/language-config.md` — Language-specific settings

## Output

`3-article/[slug].html` — Full article HTML with WordPress shortcodes

## Article Structure Template

Follow the exact structure from the reference articles. The article has these sections:

### 1. Title Comment + Intro

```html
<!-- TÍTULO: [Title in local language] -->
[intro_text]Lead paragraph with the most surprising data point. Bold key stats. Hook the reader with a counter-intuitive finding.[/intro_text]

Methodology paragraph: "Los datos provienen de <a href="https://ahrefs.com/[lang]/brand-radar">Brand Radar de Ahrefs</a>..."
```

**Title formula**: "¿Qué [brand-type] es más visible en la IA en [country-name]?" (adapt to language)

**Intro formula**: Take the most surprising finding from the data and lead with it. Example patterns:
- "[Brand A] is the biggest in [sector]. But when you ask ChatGPT, [Brand B] beats it in share of voice."
- "You'd expect [Brand A] to dominate. The data tells a different story."

### 2. ChatGPT Section

```html
[post_nav_link link_text="ChatGPT" section="chatgpt"]
<h2><strong>ChatGPT: [Key finding headline]</strong></h2>
[/post_nav_link]

[table id=CHATGPT /]
<!-- TablePress: importar tabla-1-chatgpt.csv -->

[2-3 analysis paragraphs with bold key stats]

[sidenote]Explanation of share of voice metric with link to https://ahrefs.com/blog/share-of-voice/[/sidenote]
```

### 3. AI Overviews Section

```html
[post_nav_link link_text="AI Overviews" section="ai-overviews"]
<h2><strong>AI Overviews: [Key finding headline]</strong></h2>
[/post_nav_link]

[table id=AI_OVERVIEWS /]
<!-- TablePress: importar tabla-2-ai-overviews.csv -->

[2-3 analysis paragraphs highlighting differences vs ChatGPT]
```

### 4. Cited Sources Section

```html
[post_nav_link link_text="[Cited sources label]" section="fuentes"]
<h2><strong>[Which sources does ChatGPT cite about this sector?]</strong></h2>
[/post_nav_link]

[table id=FUENTES /]
<!-- TablePress: importar tabla-3-cited-sources.csv -->

[Analysis: which brand domains appear? media vs brand sites? YouTube/Reddit presence?]
```

### 5. Cross-platform Comparison

```html
[post_nav_link link_text="[Comparison label]" section="comparativa"]
<h2><strong>ChatGPT vs AI Overviews: [headline]</strong></h2>
[/post_nav_link]

[table id=COMPARATIVA /]
<!-- TablePress: importar tabla-4-comparison.csv -->

[Analysis of biggest differences between platforms]
```

### 6. Industry Keywords Section (NEW — enrichment)

```html
[post_nav_link link_text="[Keywords label]" section="keywords"]
<h2><strong>[What do people search for about this sector?]</strong></h2>
[/post_nav_link]

[table id=KEYWORDS /]
<!-- TablePress: importar tabla-5-keywords.csv -->

[Analysis: which keywords have AI Overviews? Search volume insights? KD opportunities?]
```

### 7. SERP Analysis Section (NEW — enrichment, optional)

```html
[post_nav_link link_text="SERP" section="serp"]
<h2><strong>[Who ranks for "[top keyword]"?]</strong></h2>
[/post_nav_link]

[table id=SERP /]
<!-- TablePress: importar tabla-6-serp.csv -->

[Analysis: do the AI-visible brands also dominate organic search? Any mismatches?]
```

### 8. Actionable Takeaways

```html
[recommendation title="[What can brands in this sector learn?]"]
<ol>
  <li><strong>[Brand insight 1]:</strong> [Explanation with data]</li>
  <li><strong>[Brand insight 2]:</strong> [Explanation with data]</li>
  <li><strong>[Brand insight 3]:</strong> [Explanation with data]</li>
  <li><strong>[Brand insight 4]:</strong> [Explanation with data]</li>
</ol>
[/recommendation]
```

### 9. Conclusion + Methodology

```html
<h2><strong>[Conclusion]</strong></h2>

[1-2 paragraph conclusion with the key message]

Links to Brand Radar product page and visibility measurement guide (in target language).

[blockquote]
<strong>[Methodology label]:</strong> [Standard methodology text explaining Brand Radar, data sources, date, country filter, how mentions and SOV are calculated.]
[/blockquote]
```

## Writing Guidelines

### Tone
- Data-driven, analytical, but accessible
- Lead every section with the most interesting finding
- Bold ALL key numbers and percentages
- Use comparisons between brands to create narrative tension
- Explain WHY (hypothesize reasons for the data patterns)

### Analysis Patterns
For each table, follow this pattern:
1. **State the headline finding** (most surprising/interesting data point)
2. **Explain context** (why this matters, what you'd expect)
3. **Compare brands** (which brands over/underperform vs expectations)
4. **Hypothesize** (what might explain the pattern: content strategy, PR, YouTube presence, etc.)

### Links to Include
- Brand Radar product page: `https://ahrefs.com/[lang]/brand-radar`
- Share of voice explainer: `https://ahrefs.com/blog/share-of-voice/`
- AI visibility measurement guide (language-dependent — check if ES version exists)
- SERP features evolution: link only if ES/local version exists
- Digital PR: link only if local version exists

### CRITICAL: Internal Link Language Rule
- Only link to blog articles in the same language as the article
- For ES articles → only /blog/es/ links
- For BR articles → only /blog/pt/ links (if they exist)
- For KR articles → only /blog/ko/ links (if they exist)
- Product URLs always use /[lang]/ prefix
- If no local version of a blog article exists, DO NOT link — keep text as plain text
