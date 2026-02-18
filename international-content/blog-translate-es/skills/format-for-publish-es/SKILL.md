---
name: format-for-publish-es
description: Format a translated Spanish article with WordPress shortcodes and export to .docx
argument-hint: [adapted-file]
allowed-tools: Read, Write, Bash
---

# Format for Publish Skill (Español — Translation Pipeline)

Transform a translated and link-adapted article into a WordPress-ready document with Ahrefs shortcodes, and export to .docx.

## Input

**Adapted file path** — e.g., `./4-adapted/[es-slug].md`

---

## WordPress Shortcodes Reference

| Shortcode | Purpose | When to Use |
|-----------|---------|-------------|
| `[intro_text][/intro_text]` | Wraps intro paragraph | First paragraph after title |
| `[intro_toc]` | Auto-generates TOC | After intro, before first H2 |
| `[post_nav_link]` | Section nav anchor | Wraps each H2 heading |
| `[recommendation title="Consejo"][/recommendation]` | Tip callout box | Actionable tips, tool recommendations |
| `[sidenote][/sidenote]` | Side note | Tangential but useful info |
| `[further_reading][/further_reading]` | Related articles | End of article, 2-4 related ES posts |

### post_nav_link syntax
```
[post_nav_link link_text="Título de la sección" section="titulo-de-la-seccion"]

## Título de la sección

[/post_nav_link]
```

**Slug transliteration:** á→a, é→e, í→i, ó→o, ú→u, ñ→n, ü→u. No ¿ or ¡ in slugs.

### recommendation titles (Spanish)
"Consejo", "Consejo pro", "Importante", "Nota", "No te pierdas..."

### further_reading
```
[further_reading]

- [Título del artículo](https://ahrefs.com/blog/es/slug/)

[/further_reading]
```

**REGLA CRÍTICA:** Only include articles from `ahrefs.com/blog/es/`. Never include EN-only articles.

---

## Workflow

### Phase 1: Read and Analyze

1. Read the adapted file
2. Identify elements needing shortcodes:
   - Intro paragraph
   - All H2 headings
   - Tips/recommendations (look for patterns like "Consejo:", "Tip:", actionable suggestions)
   - Expert quotes
   - Image placeholders

### Phase 2: Apply Shortcodes

1. Wrap first paragraph in `[intro_text]...[/intro_text]`
2. Add `[intro_toc]` after intro section
3. Wrap each H2 with `[post_nav_link]...[/post_nav_link]`
4. Convert tips to `[recommendation]`
5. Convert sidenotes to `[sidenote]`
6. Add `[further_reading]` at end (ES articles only)

### Phase 3: Cleanup

1. Remove metadata header
2. Remove translation notes section
3. Remove HTML comments
4. Ensure proper spacing around shortcodes
5. Verify CTA links to Ahrefs ES social:
   - LinkedIn: https://www.linkedin.com/company/ahrefs-en-espanol/posts/?feedView=all
   - X: https://twitter.com/AhrefsES

### Phase 4: Export to .docx

```bash
pandoc input.md -o output.docx --from markdown --to docx
```

---

## Output

1. **Formatted markdown**: `./6-publish/[es-slug].md`
2. **Word document**: `./6-publish/[es-slug].docx`
