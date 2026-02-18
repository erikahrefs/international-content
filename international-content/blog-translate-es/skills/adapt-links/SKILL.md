---
name: adapt-links
description: Adapt all internal links in a translated article for the Spanish blog ecosystem
argument-hint: [translated-file]
allowed-tools: Read, Write, WebSearch, WebFetch
---

# Adapt Links Skill

Update all links in a translated article to work in the Spanish ecosystem. This is the critical step that ensures the article only links to content available in Spanish.

## Input

**Translated file path** — e.g., `./3-translated/investigacion-de-palabras-clave.md`

Also reads `./1-source/[slug].md` for the link inventory.

---

## REGLA CRÍTICA — Internal Links Only in Same Language

- **ONLY** link to blog articles that exist in Spanish (`ahrefs.com/blog/es/`)
- **NEVER** keep links to EN-only blog articles (`ahrefs.com/blog/[en-slug]/`)
- If no Spanish version exists → remove the link, keep the anchor text as plain text
- Product URLs in Spanish (`ahrefs.com/es/brand-radar`) → KEEP, these are fine
- External links (non-Ahrefs) → KEEP as-is

---

## Workflow

### Step 1: Build Link Inventory

From the translated file, extract every link:

```markdown
| # | Type | Anchor Text (ES) | Current URL | Action Needed |
|---|------|------------------|-------------|---------------|
| 1 | Blog internal | "guía de keyword research" | /blog/keyword-research/ | Check for ES |
| 2 | Product | "Site Explorer" | ahrefs.com/site-explorer | Update to /es/ |
| 3 | External | "John Mueller" | twitter.com/... | Keep |
```

### Step 2: Check Each Internal Blog Link

For each link to `ahrefs.com/blog/[slug]` (NOT `/blog/es/`):

**Method 1: Direct URL check**
Try WebFetch on `https://ahrefs.com/blog/es/[slug]/`
- If it returns content → ES version exists

**Method 2: Search for equivalent**
```
WebSearch: site:ahrefs.com/blog/es/ [topic keywords in Spanish]
```
- The ES version might have a different slug

**Method 3: Common slug patterns**
Some articles have predictable ES slugs:
- `keyword-research` → `investigacion-de-palabras-clave` or `keyword-research`
- `seo-basics` → `seo-basico` or `conceptos-basicos-seo`
- `backlink-checker` → `verificador-de-backlinks`

### Step 3: Apply Link Decisions

For each link, take one of these actions:

**A. ES version exists** → Replace URL
```markdown
# Before
[guía de keyword research](https://ahrefs.com/blog/keyword-research/)
# After
[guía de keyword research](https://ahrefs.com/blog/es/investigacion-de-palabras-clave/)
```

**B. No ES version exists** → Remove link, keep text
```markdown
# Before
Las [menciones vienen de terceros](https://ahrefs.com/blog/geo-generative-engine-optimization/)
# After
Las menciones vienen de terceros
```

**C. Product URL** → Update to /es/ version
```markdown
# Before
[Site Explorer](https://ahrefs.com/site-explorer)
# After
[Site Explorer](https://ahrefs.com/es/site-explorer)
```

Common product URL mappings:
| EN URL | ES URL |
|--------|--------|
| ahrefs.com/site-explorer | ahrefs.com/es/site-explorer |
| ahrefs.com/keywords-explorer | ahrefs.com/es/keywords-explorer |
| ahrefs.com/site-audit | ahrefs.com/es/site-audit |
| ahrefs.com/rank-tracker | ahrefs.com/es/rank-tracker |
| ahrefs.com/content-explorer | ahrefs.com/es/content-explorer |
| ahrefs.com/brand-radar | ahrefs.com/es/brand-radar |
| ahrefs.com/dashboard | ahrefs.com/es/dashboard |
| ahrefs.com/webmaster-tools | ahrefs.com/es/webmaster-tools |

**D. External link** → Keep unchanged

**E. Social links** → Update to ES accounts
| EN | ES |
|----|----|
| twitter.com/aaborysenko (or author) | twitter.com/AhrefsES |
| linkedin.com/company/ahrefs | linkedin.com/company/ahrefs-en-espanol/posts/?feedView=all |

### Step 4: Handle Further Reading

If the original article had a "Further reading" or recommended articles section:
- Only include articles that have ES versions
- If fewer than 2 articles have ES versions, search for related ES articles:
  ```
  WebSearch: site:ahrefs.com/blog/es/ [topic]
  ```
- Minimum 1 article, maximum 4

### Step 5: Generate Report

Create a link adaptation report showing all changes made.

---

## Output

Save to `./4-adapted/[es-slug].md`:

The full translated article with all links updated.

Add to the notes section:

```markdown
## Informe de adaptación de enlaces

**Total de enlaces en el artículo original**: [count]

### Enlaces internos del blog
| # | Anchor Text | URL Original (EN) | Acción | URL Final |
|---|------------|-------------------|--------|-----------|
| 1 | "keyword research" | /blog/keyword-research/ | → ES | /blog/es/investigacion-de-palabras-clave/ |
| 2 | "SEO basics" | /blog/seo-basics/ | Eliminado (sin versión ES) | — |

### URLs de producto
| # | Producto | URL Original | URL Final (/es/) |
|---|---------|-------------|-----------------|
| 1 | Site Explorer | /site-explorer | /es/site-explorer |

### Enlaces externos
| # | Anchor Text | URL | Acción |
|---|------------|-----|--------|
| 1 | "Google" | google.com/... | Sin cambios |

### Further reading
| # | Título | URL |
|---|--------|-----|
| 1 | [Título ES] | /blog/es/[slug]/ |

### Resumen
- Enlaces internos adaptados a ES: [count]
- Enlaces internos eliminados (sin ES): [count]
- URLs de producto actualizadas: [count]
- Enlaces externos sin cambios: [count]
```

---

## Quality Checklist

| Check | Requirement |
|-------|-------------|
| No EN blog links | Zero links to ahrefs.com/blog/[en-slug] remain |
| Product URLs | All product URLs use /es/ prefix |
| ES blog links | All internal blog links point to /blog/es/ |
| External links | External links preserved unchanged |
| Further reading | Only ES articles in further_reading |
| Social links | CTA uses Ahrefs ES accounts |
| Anchor text | Spanish anchor text, not English |
