---
name: market-sizing-bottoms-up
description: Produce a bottoms-up market estimate with segment-level customer buckets, assumptions, and a cross-check against top-down sizing.
allowed-tools: Read, Write, Grep, Glob, Edit, WebSearch, WebFetch
context: fork
---

# Skill: Market Sizing - Bottoms Up

## Purpose

Cross-check the market with a segment-by-segment bottoms-up model grounded in customer counts, adoption, and deal-size logic.

## Workspace I/O

- Read: `workspace/{deal-slug}/context/deal-context.json`
- Read: `workspace/{deal-slug}/sizing/top-down.json`
- Read: `workspace/{deal-slug}/sources.json` or a runner-provided temporary source registry
- Write: `workspace/{deal-slug}/sizing/bottoms-up.json`
- Update: the active source registry with every web source used

## What To Do

1. Define the target customer buckets explicitly.
2. Estimate customer counts, adoption assumptions, and ACV ranges by segment.
3. Build one visible calculation chain with segment headers, totals, and the final TAM, SAM, SOM rows.
4. Cross-check the output against the top-down result and explain the gap.

## Output Requirements

Write `sizing/bottoms-up.json` with:

- `tab_name: "Bottoms Up"`
- one `Calculation Chain` table
- section-header rows for each customer segment
- sections for `target_customer_buckets`, `cross_check`, and `assumptions_list`

## Constraints

- Treat customer counts and ACV assumptions as assumptions unless a source supports them.
- Keep totals visible and easy to audit.
- If top-down is sufficient and the analyst explicitly skips this step, do not fabricate a bottoms-up model.

### Tab Headers

| Approach | Estimate | Source/ Assumptions/ Comments | Agent Notes |

Include a "Target Customer(s) Buckets" list above the table.

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
