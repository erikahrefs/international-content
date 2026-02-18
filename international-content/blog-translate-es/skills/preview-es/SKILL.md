---
name: preview-es
description: Generate an Ahrefs-styled HTML preview of a translated Spanish article
argument-hint: [adapted-file]
allowed-tools: Read, Write, Bash
---

# Preview Skill (Español — Translation Pipeline)

Generate an HTML preview of the translated article with Ahrefs blog styling.

## Input

**Adapted file path** — e.g., `./4-adapted/[es-slug].md`

---

## Workflow

1. Read the adapted markdown file
2. Strip any metadata header (everything before the first `---` separator after the frontmatter)
3. Convert markdown to HTML using Python:

```python
import markdown
md = markdown.Markdown(extensions=['tables', 'fenced_code'])
html = md.convert(content)
```

If `markdown` is not installed: `pip install markdown --break-system-packages`

4. Wrap in the Ahrefs preview template with:
   - `lang="es"` on `<html>`
   - `charset="UTF-8"` for ñ, á, ¿, ¡
   - Inter font family
   - Ahrefs color scheme (#074ADA links, #40464d text)
   - Preview banner: "Vista Previa — Traducción Blog de Ahrefs ES"

---

## Output

Save to `./5-preview/[es-slug].html`

The preview should be viewable in any browser and give a realistic sense of how the article will look on the blog.
