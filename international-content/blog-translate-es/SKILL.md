---
name: blog-translate-es
description: Translate existing Ahrefs EN blog articles to Spanish, with keyword research and light localization
argument-hint: [url-or-slug]
allowed-tools: Read, Write, Edit, Skill
---

# Blog Translation Pipeline (EN → ES)

Translate an existing article from ahrefs.com/blog/ into Spanish for ahrefs.com/blog/es/, with keyword validation, light localization, and publish-ready formatting.

## How It Differs from blog-pipeline-es

| | blog-pipeline-es | blog-translate-es |
|---|---|---|
| **Starts from** | Keyword → original article | Existing EN article |
| **Research** | Full keyword + competitor analysis | Keyword check: EN vs ES term volume |
| **Outline** | Created from scratch | Inherited from source article |
| **Draft** | Written from scratch | Translated + lightly localized |
| **Ahrefs mentions** | Annotated from scratch | Adapted from EN (URLs → /es/) |

---

## Input

**Option A: Full URL**
```
/blog-translate-es https://ahrefs.com/blog/keyword-research/
```

**Option B: Slug only**
```
/blog-translate-es keyword-research
```

**Option C: Resume from a step**
```
/blog-translate-es --from=translate keyword-research
```

---

## Pipeline Steps

| Step | Skill | Input | Output Folder |
|------|-------|-------|---------------|
| 1 | `fetch-source` | EN article URL/slug | `1-source/` |
| 2 | `keyword-check` | source file | `2-keyword-check/` |
| 3 | `translate` | source + keyword decision | `3-translated/` |
| 4 | `adapt-links` | translated draft | `4-adapted/` |
| 5 | `preview-es` | adapted draft | `5-preview/` |
| 6 | `format-for-publish-es` | adapted draft | `6-publish/` |

---

## Step Details

### Step 1: Fetch Source
Extract the full content of the EN article.

```
/fetch-source https://ahrefs.com/blog/keyword-research/
```

**What it does:**
- Fetch the EN article via WebFetch
- Extract: title, headings structure, body text, all links, images/screenshots
- Identify internal links (to other Ahrefs blog articles)
- Identify Ahrefs product mentions and their URLs
- Save structured source file

**Output:** `./1-source/[slug].md`

---

### Step 2: Keyword Check
Compare the EN keyword with Spanish alternatives using Ahrefs MCP.

```
/keyword-check ./1-source/[slug].md
```

**What it does:**
- Identify the target keyword from the EN article (title + H1)
- Get volume/KD for the EN keyword in Spain (`country=es`)
- Generate 3-5 Spanish translation candidates
- Get volume/KD for each candidate in Spain
- Check if a Spanish article already exists for this topic
- Present comparison table for user decision

**Output:** `./2-keyword-check/[slug].md` with recommendation

**IMPORTANT:** This step pauses for user input — the user picks the target keyword.

---

### Step 3: Translate
Translate the article with light localization.

```
/translate ./1-source/[slug].md
```

**What it does:**
- Translate the full article section by section
- Apply Ahrefs ES blog style (tuteo, casual, BLUF)
- Light localization:
  - Swap currencies to EUR where applicable
  - Replace US-centric examples with Spanish/European ones where obvious
  - Adapt cultural references
  - Keep technical terms in English (SEO, SERP, CPC, etc.)
- Preserve all link placeholders for Step 4
- Format numbers in Spanish style (3.922 for thousands, 45,7% for decimals)

**Output:** `./3-translated/[slug-es].md`

---

### Step 4: Adapt Links
Update all links for the Spanish ecosystem.

```
/adapt-links ./3-translated/[slug-es].md
```

**What it does:**
- For each internal blog link (`ahrefs.com/blog/X`):
  - Check if `/blog/es/X` exists (via WebFetch or WebSearch)
  - If ES version exists → replace with ES URL
  - If NO ES version → remove link, keep text
- For product URLs → update to /es/ versions
- For external links → keep as-is
- For further_reading → only include articles with ES versions
- Generate link adaptation report

**Output:** `./4-adapted/[slug-es].md`

---

### Step 5: Preview
Generate HTML preview.

```
/preview-es ./4-adapted/[slug-es].md
```

**Output:** `./5-preview/[slug-es].html`

---

### Step 6: Format for Publish
Apply WordPress shortcodes and export to .docx.

```
/format-for-publish-es ./4-adapted/[slug-es].md
```

**Output:**
- `./6-publish/[slug-es].md` (with shortcodes)
- `./6-publish/[slug-es].docx` (Word document)

---

## Workflow Execution

When running the full pipeline:

1. **Parse input** — URL or slug
2. **Extract EN slug** (e.g., `keyword-research`)
3. **Run Step 1** → Fetch source article
4. **Run Step 2** → Keyword check (PAUSE for user decision)
5. **Run Step 3** → Translate with chosen keyword
6. **Run Step 4** → Adapt links
7. **Run Step 5** → Preview
8. **Run Step 6** → Format + export
9. **Report completion** with all file locations

---

## Resume from Step

```
/blog-translate-es --from=translate keyword-research
```

Valid `--from` values:
- `fetch-source` (Step 1 — default)
- `keyword-check` (Step 2)
- `translate` (Step 3)
- `adapt-links` (Step 4)
- `preview` (Step 5)
- `format-for-publish` (Step 6)

---

## Output Summary

After a complete pipeline run:

```
## Translation Complete: [EN slug] → [ES slug]

| Step | Output |
|------|--------|
| 1. Source | ./1-source/[en-slug].md |
| 2. Keyword | ./2-keyword-check/[en-slug].md |
| 3. Translated | ./3-translated/[es-slug].md |
| 4. Adapted | ./4-adapted/[es-slug].md |
| 5. Preview | ./5-preview/[es-slug].html |
| 6. Publish | ./6-publish/[es-slug].md, .docx |

Ready for WordPress upload: ./6-publish/[es-slug].docx
```

---

## Working Directory

This pipeline works inside `blog-translate-es/` in the workspace folder.
All output directories are created automatically.

---

## Error Handling

- **Source article not accessible**: Try WebSearch fallback, ask user to paste content
- **Keyword check finds existing ES article**: Warn user, offer to continue as an update
- **Step fails**: Stop pipeline, report error, preserve completed outputs
