---
name: competitor-landscape
description: Build the competitor landscape, grouped by category, and write the Competitor Analysis workspace JSON.
allowed-tools: Read, Write, Grep, Glob, Edit, WebSearch, WebFetch
context: fork
---

# Skill: Competitor Landscape

## Purpose

Map the relevant direct, indirect, global, local, and adjacent competitors in the format of the Biome competitor tab.

## Workspace I/O

- Read: `workspace/{deal-slug}/context/deal-context.json`
- Read: `workspace/{deal-slug}/analysis/value-chain.json` when available
- Read: `workspace/{deal-slug}/sources.json` or a runner-provided temporary source registry
- Write: `workspace/{deal-slug}/analysis/competitors.json`
- Update: the active source registry with every web source used

## What To Do

1. Identify the right competitor categories for the market.
2. Build the table with section headers for each category.
3. Capture traction, funding, and USP only when publicly supportable.
4. Summarize the funding landscape and the important market gaps.

## Output Requirements

Write `analysis/competitors.json` with:

- `tab_name: "Competitor Analysis"`
- one competitor table with category section headers
- sections for `funding_landscape` and `gap_analysis`

## Constraints

- Compare against status quo or service alternatives when they are real substitutes.
- Leave missing fields blank instead of hallucinating estimates.
- Flag thin or self-reported traction data in `Agent Notes`.

### Tab Headers

| No. | Company (Competitors) | Description of Product/Service | Founding Year | USP | Traction/Revenue | Valuation | Investors | Funding | Key Features | So what? | Agent Notes |

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
