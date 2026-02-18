---
name: fetch-source
description: Fetch and extract content from an Ahrefs EN blog article for translation
argument-hint: [url-or-slug]
allowed-tools: Read, Write, WebFetch, WebSearch
---

# Fetch Source Skill

Extract the full content of an existing Ahrefs EN blog article and save it in a structured format ready for translation.

## Input

**URL or slug** of the EN article:
- Full URL: `https://ahrefs.com/blog/keyword-research/`
- Slug only: `keyword-research` → resolved to `https://ahrefs.com/blog/keyword-research/`

---

## Workflow

### Step 1: Fetch the Article

Use WebFetch to get the article content:

```
WebFetch: https://ahrefs.com/blog/[slug]/
Prompt: Extract the full article content including: title (H1), all headings (H2-H4) with their hierarchy, all body text preserving paragraph structure, all hyperlinks with their anchor text and URLs, any callouts/tips/sidenotes, image alt text descriptions, the author name, and the publication/update date. Return as clean markdown.
```

If WebFetch returns a 403 or fails:
1. Try WebSearch: `site:ahrefs.com/blog/[slug]` to confirm the article exists
2. Ask the user to paste the article content directly

### Step 2: Extract Structure

From the fetched content, identify and tag:

**Metadata:**
- Title (H1)
- Author
- Published/Updated date
- Target keyword (from the title + H1 + first paragraph)

**Content elements:**
- All H2/H3/H4 headings in order
- Body text under each heading
- Lists (bulleted and numbered)
- Tables
- Blockquotes / expert quotes

**Links inventory:**
Create a full link inventory:

```markdown
## Link Inventory

### Internal Blog Links
| # | Anchor Text | URL | ES Version? |
|---|------------|-----|-------------|
| 1 | "keyword research" | /blog/keyword-research/ | TBD |
| 2 | "backlink checker" | /blog/backlink-checker/ | TBD |

### Product Links
| # | Product | URL |
|---|---------|-----|
| 1 | Site Explorer | https://ahrefs.com/site-explorer |
| 2 | Keywords Explorer | https://ahrefs.com/keywords-explorer |

### External Links
| # | Anchor Text | URL |
|---|------------|-----|
| 1 | "John Mueller" | https://twitter.com/... |
```

**Visual placeholders:**
- `[SCREENSHOT: description of what the screenshot shows]`
- `[IMAGE: description]`
- `[ILLUSTRATION: description]`

### Step 3: Check for Existing ES Version

Search if this article already has a Spanish translation:

```
WebSearch: site:ahrefs.com/blog/es/ [main topic keywords in Spanish]
```

Also try the direct URL pattern: `https://ahrefs.com/blog/es/[slug]/`

If an ES version exists:
- Note it in the output
- Include the ES URL
- Flag for user: "An existing Spanish version was found. This translation will be a new/updated version."

---

## Output

Save to `./1-source/[slug].md`:

```markdown
# Source Article: [Title]

**EN URL**: https://ahrefs.com/blog/[slug]/
**Author**: [name]
**Date**: [published/updated]
**Inferred keyword**: [keyword from title]
**Existing ES version**: [URL or "None found"]

---

## Article Content

[Full article content in markdown, preserving all headings, paragraphs, lists, tables, links, and visual placeholders]

---

## Link Inventory

### Internal Blog Links (ahrefs.com/blog/)
| # | Anchor Text | URL |
|---|------------|-----|
[table]

### Product Links (ahrefs.com tools)
| # | Product | URL |
|---|---------|-----|
[table]

### External Links
| # | Anchor Text | URL |
|---|------------|-----|
[table]

---

## Visual Placeholders
- [SCREENSHOT: ...]
- [IMAGE: ...]

---

## Notes
- Word count: [approximate]
- Number of H2 sections: [count]
- Number of internal links: [count]
- Number of product mentions: [count]
```
