---
name: generate-tables
description: Transform collected JSON data into TablePress-ready CSV files
argument-hint: [slug]
allowed-tools: Read, Write, Bash
---

# Generate Tables Sub-skill

Transform the raw JSON data from Step 1 into CSV files ready for TablePress import in WordPress.

## Input

Read from: `1-data/[slug].json`

## Output

Write CSVs to: `2-tables/[slug]/`

## Table Specifications

### tabla-1-chatgpt.csv

ChatGPT mentions and share of voice per brand, sorted by SOV descending.

```csv
Marca,Menciones ChatGPT,Share of Voice
Carrefour,3.500,"45,7%"
Mercadona,3.922,"40,3%"
```

**Column mapping** (adapt headers to target language — see language-config):
- Brand name
- Total mentions from `chatgpt.mentions`
- SOV from `chatgpt.sov` (formatted as percentage with local number format)

### tabla-2-ai-overviews.csv

Same structure but for AI Overviews data.

```csv
Marca,Menciones AI Overviews,Share of Voice
Mercadona,9.415,"49,9%"
Dia,8.257,"30,8%"
```

### tabla-3-cited-sources.csv

Top cited domains, sorted by responses descending.

```csv
Dominio citado,Respuestas,Volumen mensual
elespanol.com,2.105,"4,5M"
carrefour.es,1.824,"4,7M"
```

**Volume formatting:**
- < 1,000 → show exact number
- 1,000–999,999 → show as "X,XK" (e.g., "4,5K")
- ≥ 1,000,000 → show as "X,XM" (e.g., "4,5M")
- Use local number formatting (see language-config)

### tabla-4-comparison.csv

Cross-platform comparison table, sorted by total mentions descending.

```csv
Marca,SOV ChatGPT,SOV AI Overviews,ChatGPT (menciones),AI Overviews,Diferencia
Mercadona,"40,3%","49,9%",3.922,9.415,+140%
```

**Difference column**: Calculate `((AI Overviews mentions - ChatGPT mentions) / ChatGPT mentions) × 100`. Format as `+X%` or `-X%`.

### tabla-5-keywords.csv

Industry keyword metrics from Keywords Explorer.

```csv
Keyword,Volumen,KD,CPC (USD),Traffic Potential,AI Overview
mejores supermercados,5.400,35,$0.45,8.200,Sí
```

**AI Overview column**: Check if `serp_features` array contains `"ai_overview"` → "Sí"/"No" (or equivalent in target language).

### tabla-6-serp.csv (optional)

SERP overview for the top industry keyword.

```csv
Posición,URL,DR,Tráfico,Top Keyword
1,ejemplo.com/mejores-supermercados,85,12.500,mejores supermercados
```

Only generate this table if SERP data was collected in Step 1.

## Number Formatting by Language

| Country | Thousands sep | Decimal sep | Example |
|---------|--------------|-------------|---------|
| ES, MX | . | , | 3.922 / 45,7% |
| BR | . | , | 3.922 / 45,7% |
| KR | , | . | 3,922 / 45.7% |
| US, UK | , | . | 3,922 / 45.7% |
| FR | space | , | 3 922 / 45,7% |
| DE | . | , | 3.922 / 45,7% |

## Important Rules

1. **Sort by SOV descending** in tables 1 and 2
2. **Sort by total mentions descending** in table 4
3. **Sort by volume descending** in table 5
4. **Sort by position ascending** in table 6
5. **Quote fields with commas** — CSV fields containing commas MUST be quoted
6. **Use UTF-8 encoding** — important for Korean, Portuguese accents, etc.
7. **No trailing newline** at end of CSV file
