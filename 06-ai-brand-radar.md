# Skill: /ai-brand-radar — AI Visibility by Market

## Purpose
Monitor and analyze how a brand and its competitors appear in AI-generated responses (ChatGPT, Claude, Perplexity, etc.) — tracking mentions, share of voice, cited sources, and sentiment across different markets and languages.

## When to Trigger
- User asks about AI visibility, AI search presence, or "how do we show up in ChatGPT?"
- User wants to track brand mentions in LLM responses
- User mentions "AI brand monitoring", "LLM visibility", "AI share of voice"
- User wants to compare their AI presence against competitors

## Required Inputs
- **brand**: The brand to track (e.g., `canva`)
- **competitors**: Comma-separated competitor brands (e.g., `figma, adobe express, visme`)
- **data_source**: The AI platform to analyze (`chatgpt`, `claude`, `perplexity`, `gemini`)
- **Optional**: `country`, `market` for regional filtering

## Workflow

### Step 1: Get Mentions Overview
Use **Brand Radar - Mentions Overview**:
- Brand: target brand
- Competitors: competitor brands
- Data source: specified AI platform
- Select: `total, brand, only_target_brand, only_competitors_brands, target_and_competitors_brands`
- Optional: filter by country/market for international analysis

### Step 2: Get Impressions Overview
Use **Brand Radar - Impressions Overview**:
- Same parameters as above
- Select available impression metrics
- This shows how often the brand appears in AI responses overall

### Step 3: Get Share of Voice Overview
Use **Brand Radar - SOV Overview**:
- Same parameters
- This gives percentage share of voice across all tracked queries

### Step 4: Get Mentions History (Trend)
Use **Brand Radar - Mentions History**:
- Same brand/competitors
- This shows if AI visibility is growing or declining over time

### Step 5: Get Cited Domains
Use **Brand Radar - Cited Domains**:
- This reveals which domains the AI cites when mentioning your brand
- Critical for understanding what sources feed AI responses

### Step 6: Get Cited Pages
Use **Brand Radar - Cited Pages**:
- This shows specific pages the AI references
- Helps identify which content drives AI visibility

### Step 7: Get AI Responses (Samples)
Use **Brand Radar - AI Responses**:
- Pull actual AI response samples where your brand is mentioned
- Analyze tone, context, and how you're positioned relative to competitors

### Step 8: Analyze by Market
Repeat Steps 1-3 with different country/market filters to compare AI visibility across regions.

## Analysis Framework

Calculate and present:

1. **Share of Voice (SOV)** — Your mentions ÷ total mentions for the category
2. **Solo Mention Rate** — % of times mentioned alone (not alongside competitors) — indicates being the "default recommendation"
3. **Co-mention Partners** — Which competitors you're most often mentioned alongside
4. **Citation Authority** — Which of your pages are most cited by AI
5. **Market Variation** — How SOV differs across countries/languages
6. **Trend Direction** — Is AI visibility growing or declining?

## Output Format

### AI Visibility Dashboard: [Brand]
- Platform: [ChatGPT/Claude/etc.]
- Analysis Period: [dates]

### Share of Voice

| Brand | Total Mentions | Solo Mentions | Co-mentions | SOV % |
|-------|---------------:|--------------:|------------:|------:|

### AI Visibility by Market

| Market/Country | Your SOV | Top Competitor SOV | Gap |
|---------------|--------:|-----------------:|----:|

### Most Cited Pages (Your Brand)

| Page URL | Times Cited | Context |
|----------|-------------|---------|

### Trend (Last 6 Months)
- [Monthly SOV trend data]
- Direction: Growing / Stable / Declining

### Recommendations

1. **Content to create/optimize** — Topics where competitors are cited but you aren't
2. **Pages to strengthen** — Your most-cited pages that need updating to maintain position
3. **Market priorities** — Countries where AI visibility lags behind organic visibility
4. **Competitive threats** — Competitors gaining AI SOV faster than you
5. **AI-specific content strategy** — Content formats AI models prefer to cite

## Example with Real Data (Canva vs Competitors in ChatGPT)

| Brand | Total Mentions | Solo Mentions | Co-mentions | SOV % |
|-------|---------------:|--------------:|------------:|------:|
| **Canva** | **20,083** | **14,247** | **5,836** | **88.1%** |
| Adobe Express | 6,582 | 1,655 | 4,927 | 24.3% |
| Figma | 1,966 | 991 | 975 | 7.5% |
| Visme | 1,281 | 130 | 1,151 | 4.4% |

**Insight:** "Canva dominates ChatGPT responses with 88% share of voice. When mentioned, Canva appears alone in 71% of cases — it's the default recommendation. Adobe Express appears but almost always alongside Canva (75% co-mention rate). Visme is almost never recommended alone (only 130 solo mentions vs 1,151 co-mentions). This is a massive competitive moat in the AI discovery channel."
