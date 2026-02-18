# International Content — Ahrefs Blog Skills

Claude Code skills for creating and translating Ahrefs blog content in Spanish.

## Skills

### blog-pipeline-es

Full article creation pipeline from keyword to publish-ready article. 7 sub-skills:

1. **research-es** — Keyword research + competitor analysis via Ahrefs MCP
2. **ahrefs-mentions-es** — Brand Radar data for AI visibility angles
3. **outline-es** — Article outline with BLUF structure
4. **draft-es** — Section-by-section draft in Spanish
5. **verify-claims-es** — Fact-check stats + add citations
6. **format-for-publish-es** — WordPress shortcodes + .docx export
7. **preview-es** — HTML preview for copy-paste to WordPress

### blog-translate-es

Translation pipeline for existing EN articles. 6 sub-skills:

1. **fetch-source** — Fetch EN article + build link inventory
2. **keyword-check** — Compare EN vs ES keyword volumes via Ahrefs MCP
3. **translate** — Section-by-section translation with light localization
4. **adapt-links** — Enforce same-language link rule, update product URLs
5. **preview-es** — HTML preview
6. **format-for-publish-es** — WordPress shortcodes + .docx export

## Setup

Copy skills into your Claude Code project:

```bash
cp -r blog-pipeline-es /path/to/project/.claude/skills/
cp -r blog-translate-es /path/to/project/.claude/skills/
```

## Key Rules

- **Internal links**: Only link to articles in the same language (`/blog/es/` for Spanish). Never link to EN-only blog articles.
- **Product URLs**: Use `/es/` prefix (e.g., `ahrefs.com/es/site-audit`)
- **Style**: Tuteo informal, BLUF principle, Spanish number formatting (3.922 for thousands, 45,7% for decimals)
