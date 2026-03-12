---
name: market-sizing-top-down
description: Produce a top-down TAM, SAM, and SOM estimate with a visible calculation chain and workbook-ready JSON output.
allowed-tools: Read, Write, Grep, Glob, Edit, WebSearch, WebFetch
context: fork
---

# Skill: Market Sizing - Top Down

## Purpose

Build the top-down market sizing view using credible secondary research and a traceable calculation chain.

## Workspace I/O

- Read: `workspace/{deal-slug}/context/deal-context.json`
- Read: `workspace/{deal-slug}/analysis/value-chain.json` when available
- Read: `workspace/{deal-slug}/sources.json` or a runner-provided temporary source registry
- Write: `workspace/{deal-slug}/sizing/top-down.json`
- Update: the active source registry with every web source used

## What To Do

1. Define the market terminology for this specific deal.
2. Find credible analyst or primary numbers for the broad market.
3. Build a step-by-step chain from the broad market to TAM, SAM, and SOM.
4. Cross-check conflicting sources and state the discrepancy.
5. Add a short gut check on venture scale and realism.

## Output Requirements

Write `sizing/top-down.json` with:

- `tab_name: "Top Down"`
- a `Credible Analyst Numbers` table
- a `Calculation Chain` table
- a `Gut Check` section

Use row type `total` for TAM, SAM, and SOM rows.

## Constraints

- Every number must have a source, be explicitly calculated, or be marked as an assumption with rationale.
- Do not create projections unless the source itself reports them.
- Do not hide weak assumptions. Flag them in `Agent Notes`.

### Tab Headers

Table 1 — Credible Analyst Numbers:

| Market Terminology | Geography | TAM (Year) | CAGR | Source | Agent Notes |

Table 2 — Calculation Chain:

| Parameter | Estimate | Source/ Assumptions/ Comments | Agent Notes |

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
