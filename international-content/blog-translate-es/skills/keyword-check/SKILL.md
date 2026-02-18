---
name: keyword-check
description: Compare EN keyword vs Spanish alternatives using Ahrefs MCP to pick the best target keyword
argument-hint: [source-file]
allowed-tools: Read, Write, WebSearch, mcp__1a081627-4991-4907-9154-9bd405f0af14__keywords-explorer-overview, mcp__1a081627-4991-4907-9154-9bd405f0af14__keywords-explorer-matching-terms, mcp__1a081627-4991-4907-9154-9bd405f0af14__keywords-explorer-volume-by-country, mcp__1a081627-4991-4907-9154-9bd405f0af14__doc
---

# Keyword Check Skill

Compare the original English keyword with Spanish translation candidates to find the best target keyword for the Spanish article. Uses Ahrefs MCP for real data.

## Input

**Source file path** — Path to the fetched source (e.g., `./1-source/keyword-research.md`)

---

## Workflow

### Step 1: Identify the EN Keyword

Read the source file and extract:
- The inferred keyword from the title/H1
- Any secondary keywords visible in the article

### Step 2: Check EN Keyword Volume in Spain

The original English term might actually rank in Spain (many SEO terms do).

Call `keywords-explorer-overview` with:
- `keywords`: the EN keyword
- `country`: `es`
- `select`: `keyword,volume,difficulty,traffic_potential,cpc,parent_topic`

### Step 3: Generate Spanish Candidates

Based on the EN keyword, generate 3-5 Spanish translation candidates. Consider:

1. **Direct translation** — e.g., "keyword research" → "investigación de palabras clave"
2. **Common local term** — what Spanish SEOs actually say (e.g., "búsqueda de keywords")
3. **Hybrid** — mix of EN + ES (e.g., "keyword research en español")
4. **Alternate phrasing** — e.g., "cómo buscar palabras clave"
5. **Related concept** — e.g., "herramientas de keywords"

### Step 4: Check Spanish Candidates in Ahrefs

For each candidate, call `keywords-explorer-overview` with:
- `keywords`: the Spanish candidate
- `country`: `es`
- `select`: `keyword,volume,difficulty,traffic_potential,cpc,parent_topic`

Also run `keywords-explorer-matching-terms` for the top 2 candidates:
- `keywords`: candidate
- `country`: `es`
- `select`: `keyword,volume,difficulty,traffic_potential,parent_topic`
- `limit`: 10
- `order_by`: `volume:desc`

This reveals related long-tail terms that might be better targets.

### Step 5: Check Volume by Country (Optional)

If the article targets LATAM markets too, check top candidates across countries:

Call `keywords-explorer-volume-by-country` for the top 2 candidates.

This shows whether the keyword works globally or is Spain-specific.

### Step 6: Present Comparison

Present the data to the user in a clear table:

```markdown
## Keyword Comparison: [EN slug]

### EN Keyword in Spain
| Keyword | Volume (ES) | KD | TP | CPC |
|---------|------------|-----|-----|-----|
| [en keyword] | [vol] | [kd] | [tp] | [cpc] |

### Spanish Candidates
| # | Keyword (ES) | Volume (ES) | KD | TP | CPC | Parent Topic |
|---|-------------|------------|-----|-----|-----|-------------|
| 1 | [candidate 1] | [vol] | [kd] | [tp] | [cpc] | [parent] |
| 2 | [candidate 2] | [vol] | [kd] | [tp] | [cpc] | [parent] |
| 3 | [candidate 3] | [vol] | [kd] | [tp] | [cpc] | [parent] |

### Related Terms (top matches)
| Keyword | Volume | KD | TP | Parent Topic |
|---------|--------|-----|-----|-------------|
| [term] | [vol] | [kd] | [tp] | [parent] |

### Recommendation
[Brief analysis: which keyword has the best combination of volume, difficulty, and relevance]

**Pick a keyword to proceed with, or suggest a different one.**
```

### Step 7: Wait for User Decision

**IMPORTANT**: This step PAUSES the pipeline. The user must choose:
- One of the candidates
- The original EN keyword (if it has good volume in Spain)
- A custom keyword they suggest

Record their choice in the output file.

---

## Output

Save to `./2-keyword-check/[slug].md`:

```markdown
# Keyword Check: [EN article title]

**EN URL**: [url]
**EN keyword**: [keyword]
**Chosen ES keyword**: [user's choice]
**ES slug**: [transliterated slug]

---

## Data

[Full comparison tables from Step 6]

---

## Decision
- User chose: "[keyword]"
- Reason: [volume/difficulty/relevance]
- ES slug for article: [slug-es]
```

---

## Slug Generation Rules

When generating the Spanish slug from the chosen keyword:
- Lowercase
- Hyphens instead of spaces
- Transliterate: á→a, é→e, í→i, ó→o, ú→u, ñ→n, ü→u
- No special characters (¿, ¡, etc.)
- Max 5-6 words
- Example: "investigación de palabras clave" → `investigacion-de-palabras-clave`
- Example: "qué es el SEO" → `que-es-el-seo`
