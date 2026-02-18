---
name: preview
description: Generate an HTML preview of the brand visibility article for browser review
argument-hint: [slug]
allowed-tools: Read, Write, Bash
---

# Preview Sub-skill

Generate a styled HTML preview from the article HTML file.

## Input

`3-article/[slug].html` — WordPress-ready article with shortcodes

## Procedure

1. Read the article HTML
2. Read the CSV tables from `2-tables/[slug]/`
3. Convert WordPress shortcodes to styled HTML:
   - `[intro_text]...[/intro_text]` → `<div class="intro">...</div>`
   - `[intro_toc]` → Remove (TOC auto-generated in WordPress)
   - `[post_nav_link]...[/post_nav_link]` → Keep contents, strip shortcode
   - `[table id=X /]` → Render actual HTML `<table>` from corresponding CSV
   - `[sidenote]...[/sidenote]` → `<div class="sidenote">...</div>`
   - `[recommendation]...[/recommendation]` → `<div class="recommendation">...</div>`
   - `[blockquote]...[/blockquote]` → `<blockquote class="methodology">...</blockquote>`
   - `<!-- comments -->` → Remove
4. Wrap in full HTML document with styling

## HTML Template

```html
<!DOCTYPE html>
<html lang="[lang-code]">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>[Article title] — Vista Previa</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  /* Same Ahrefs blog styling as other preview skills */
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { font-family: 'Inter', sans-serif; color: #40464d; line-height: 1.7; background: #f7f8fa; }
  .preview-banner { background: #074ADA; color: white; text-align: center; padding: 10px; font-size: 13px; }
  .container { max-width: 720px; margin: 0 auto; padding: 40px 24px 80px; background: white; }
  h2 { font-size: 24px; margin-top: 48px; margin-bottom: 16px; color: #1a1a1a; }
  p { margin-bottom: 16px; font-size: 16px; }
  a { color: #074ADA; text-decoration: none; }
  table { width: 100%; border-collapse: collapse; margin: 24px 0; }
  th { background: #f7f8fa; font-weight: 600; text-align: left; padding: 10px 12px; border: 1px solid #e8e8e8; }
  td { padding: 10px 12px; border: 1px solid #e8e8e8; font-size: 14px; }
  tr:hover { background: #fafbfc; }
  .intro { font-size: 18px; line-height: 1.6; margin-bottom: 24px; }
  .sidenote { background: #f0f4ff; border-left: 3px solid #074ADA; padding: 16px 20px; margin: 24px 0; font-size: 14px; }
  .recommendation { background: #f0faf0; border-left: 3px solid #2ecc71; padding: 20px 24px; margin: 32px 0; }
  .recommendation h3 { font-size: 16px; font-weight: 600; margin-bottom: 12px; }
  blockquote.methodology { background: #f7f8fa; padding: 20px; margin: 32px 0; border-radius: 4px; font-size: 14px; color: #6b7280; }
  strong { color: #1a1a1a; }
  ol { padding-left: 24px; }
  li { margin-bottom: 12px; }
</style>
</head>
<body>
<div class="preview-banner">Vista Previa — Brand Visibility Listicle</div>
<div class="container">
  [CONVERTED CONTENT]
</div>
</body>
</html>
```

## Table Rendering

When converting `[table id=X /]` placeholders:

1. Read the corresponding CSV file
2. Generate an HTML `<table>` with `<thead>` and `<tbody>`
3. Right-align numeric columns (mentions, SOV, volume, KD, CPC, etc.)
4. Add CSS class `numeric` to right-aligned cells

## Output

`4-preview/[slug].html`
