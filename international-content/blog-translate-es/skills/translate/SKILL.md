---
name: translate
description: Translate an EN Ahrefs blog article to Spanish with light localization
argument-hint: [source-file]
allowed-tools: Read, Write
---

# Translate Skill

Translate an Ahrefs EN blog article into Spanish, applying light localization and following Ahrefs ES blog style conventions.

## Input

- **Source file**: `./1-source/[slug].md`
- **Keyword check file**: `./2-keyword-check/[slug].md` (for chosen keyword + slug)

---

## Translation Principles

### What This Is NOT
This is **not** a literal word-for-word translation. It's a **professional localization** that reads as if it were originally written in Spanish. The article should feel native to a Spanish reader.

### What This IS
- Faithful to the original meaning and structure
- Adapted to Spanish reading patterns and style
- Localized where obvious (currencies, domains, examples)
- Following Ahrefs ES blog conventions

---

## Style Guide (Spanish)

### Voice and Tone
- **Tuteo informal** but professional ("tú" not "usted")
- **Español neutro** with a light Spanish-from-Spain tendency
- Casual tone — starting sentences with "Pero..." or "Y lo más interesante:" is valid
- Direct, not formal or academic
- No swearing

### Sentence and Paragraph Structure
- **One thought per sentence**
- **Max 3 lines per paragraph**
- **No filler** — cut "En este artículo vamos a ver..."
- **Simple language** — "vimos" not "constatamos"

### Number Formatting
- Thousands separator: period → 3.922
- Decimal separator: comma → 45,7%
- No space before %: 45,7% (not 45,7 %)
- Currency: swap USD to EUR where the amount is illustrative (not a specific data point)

### Technical Terms — Keep in English
SEO, SEM, CPC, SERP, keyword, backlink, share of voice, AI Overviews, ChatGPT, Domain Rating, traffic potential, keyword difficulty, CTR, CMS, URL, HTML, CSS, JavaScript, API, anchor text, nofollow, dofollow, robots.txt, sitemap, crawl, index, canonical, redirect, 301, 404, hreflang, schema markup, Core Web Vitals, E-E-A-T

### Technical Terms — Translate
mentions → menciones, visibility → visibilidad, ranking → posicionamiento, search engine → motor de búsqueda, link building → construcción de enlaces (or keep "link building"), bounce rate → tasa de rebote, organic traffic → tráfico orgánico, search volume → volumen de búsqueda

---

## Light Localization Rules

### DO Localize
- **Currencies**: If the original says "$50/month" as a general example → "50 $/mes" or "50 €/mes" depending on context
- **Domains**: If "example.com" → keep. If "bestplumber-nyc.com" → swap for a Spanish equivalent like "fontanero-madrid.com"
- **Cultural references**: "Black Friday sales" → keep (universal). "Super Bowl" → consider if relevant to audience
- **Local brands/examples**: If an example uses a US-only brand and the point is illustrative, consider swapping for a known equivalent
- **Date formats**: "March 2025" → "marzo de 2025"
- **Measurement**: miles → km, Fahrenheit → Celsius (if they appear)

### DO NOT Localize
- **Specific data points** — If the EN article says "Pinterest has 450M users", keep the exact number
- **Brand names** — Never change Ahrefs, Google, ChatGPT, etc.
- **Study results** — Keep exact figures from cited studies
- **Screenshots** — Keep [SCREENSHOT] placeholders as-is (screenshots will be retaken separately)
- **Formulas/code** — Keep technical content unchanged

---

## Translation Workflow

### Phase 0: Load Context

1. Read the source file (`./1-source/[slug].md`)
2. Read the keyword check file (`./2-keyword-check/[slug].md`)
3. Extract: chosen ES keyword, ES slug, article structure

If `./reference/style-reference-es.md` exists, read it and extract a Style Card (~200 words) for voice calibration.

### Phase 1: Translate Section by Section

For each H2 section:

1. **Read the EN section** completely
2. **Translate** following style guide above
3. **Apply light localization** where applicable
4. **Preserve link placeholders** — keep all `[text](url)` links intact, translating only the anchor text
5. **Mark links for adaptation** — internal blog links will be updated in Step 4 (adapt-links)
6. **Write the ES section** to the output file

**Critical**: Translate the anchor text of links but keep the URL unchanged. The adapt-links step will handle URL updates.

Example:
```
EN: Check our [keyword research guide](https://ahrefs.com/blog/keyword-research/) for details.
ES: Consulta nuestra [guía de keyword research](https://ahrefs.com/blog/keyword-research/) para más detalles.
```

### Phase 2: Introduction

Translate the introduction:
- Adapt the PAS formula to Spanish
- Keep it under 100 words
- Make sure the hook works in Spanish (some EN hooks rely on English wordplay)

### Phase 3: Conclusion

Translate the conclusion:
- Replace Twitter/social CTA with Ahrefs ES accounts:
  - LinkedIn: https://www.linkedin.com/company/ahrefs-en-espanol/posts/?feedView=all
  - X: https://twitter.com/AhrefsES

### Phase 4: Review Pass

Read the full translated article and check:
- Does it read naturally in Spanish? (not "translationese")
- Are technical terms consistently handled?
- Are numbers in Spanish format?
- Are all links preserved with translated anchor text?
- Is the title optimized for the chosen ES keyword?

---

## Output

Save to `./3-translated/[es-slug].md`:

```markdown
# [Translated Title]

**Keyword objetivo**: [chosen ES keyword]
**Keyword EN original**: [original EN keyword]
**Artículo fuente**: [EN URL]
**Conteo de palabras**: ~[count]
**Status**: Traducido (enlaces pendientes de adaptar)

---

[Full translated article in markdown]

---

## Notas de traducción

**Localizaciones aplicadas:**
- [List of localization changes made]

**Elementos sin traducir (intencional):**
- [Terms/phrases kept in English and why]

**Pendiente:**
- [ ] Adaptación de enlaces internos (Step 4)
- [ ] Verificar screenshots necesarios
```

---

## Quality Checklist

| Check | Requirement |
|-------|-------------|
| Natural | Reads as native Spanish, no "translationese" |
| Voice | Tuteo + first person plural consistent |
| Numbers | Spanish format (3.922 / 45,7%) |
| Terms | Technical terms in English per style guide |
| Links | All links preserved with translated anchor text |
| Structure | Same H2/H3 hierarchy as original |
| Length | Within ±15% of original word count |
| Intro | Under 100 words, PAS formula |
| Conclusion | CTA to Ahrefs ES social accounts |
| Keyword | Chosen ES keyword used naturally in title + first 100 words |
