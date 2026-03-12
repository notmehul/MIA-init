---
name: feature-comparison
description: Compare product capabilities, pricing, and business-model UX across the most relevant competitors and write the Feature Comparison workspace JSON.
allowed-tools: Read, Write, Grep, Glob, Edit, WebSearch, WebFetch
context: fork
---

# Skill: Feature Comparison

## Purpose

Build an L2 comparison across features, pricing, and business-model or UX choices for the most relevant comparable products.

## Workspace I/O

- Read: `workspace/{deal-slug}/context/deal-context.json`
- Read: `workspace/{deal-slug}/analysis/competitors.json`
- Read: `workspace/{deal-slug}/sources.json` or a runner-provided temporary source registry
- Write: `workspace/{deal-slug}/analysis/feature-comparison.json`
- Update: the active source registry with every web source used

## What To Do

1. Select only the comparables that matter for product benchmarking.
2. Build separate tables for the feature matrix, pricing, and business-model or UX differences.
3. Finish with a differentiation assessment that states what is actually distinct.

## Output Requirements

Write `analysis/feature-comparison.json` with:

- `tab_name: "Feature Comparison"`
- tables for `Feature Matrix`, `Pricing Comparison`, and `Business Model & UX`
- a `Differentiation Assessment` section

## Constraints

- Skip this skill when the market does not have product-comparable competitors.
- Keep feature claims grounded in official docs, pricing pages, or reputable reviews.
- Do not confuse marketing copy with real product capability.

### Tab Headers

| Features | Feature Description | Comp 1 | Comp 2 | ... | Comp 10 | Agent Notes |

Rename `Comp N` to actual competitor names. Include rows for: Business Model, Freemium or Paid, Brand Voice/Tone, UX/UI, and Pricing (Free Trial / Individual / Team / Enterprise).

## Common Rules

### JSON Envelope

```json
{
  "skill": "<skill-name>",
  "tab_name": "<Tab Name>",
  "summary": "<1-2 sentence summary>",
  "tables": [],
  "sections": [],
  "source_refs": []
}
```

### Table & Row Schema

Table: `{ "id", "label", "headers": [...], "rows": [] }`

Row: `{ "data": [...], "source_refs": ["src_NNN"], "type": "data"|"section_header"|"total"|"empty" }`

`data` length must match `headers`. `source_refs` must be valid IDs in `sources.json`. Total rows are rendered bold automatically.

### Sections

`{ "id", "label", "content": "<markdown text>" }` — use `"items": [...]` for bullet lists.

### sources.json Rules

Check if URL exists before adding. Reuse existing `src_NNN` if found. New ID = `src_` + (count of existing + 1).

Entry: `{ "url", "publisher", "title", "tier" (1-3), "date_accessed", "used_by_skills": ["skill-name"] }`

### Citation Format

`(Source) - <Publisher>` · `Calculated field` · `Through Primary Research` · `Assumption - <rationale>`

### Evidence & Anti-Speculation

- Every number traces to source, calculation, primary research, or labeled assumption.
- Show conflicting sources; note discrepancy in Agent Notes.
- No projections unless the source reports them. No speculative language without citation.
- Blank cells over placeholders. Agent Notes only for real analyst flags.

### Source Tiers

- **Tier 1**: Government filings (SEBI, ROC, SEC), annual reports, DRHPs, Big Four/MBB with disclosed methodology.
- **Tier 2**: Gartner, Forrester, Grand View, MarketsandMarkets, IMARC, Mordor, Allied; NASSCOM; Reuters, Bloomberg; World Bank, UN.
- **Tier 3** (flag in Agent Notes): Single-company reports, Reddit/Twitter sentiment, G2/Capterra reviews, company blogs.
- **Non-credible for numbers**: Statista, SEO blog posts, Wikipedia, AI summaries.
