---
name: trends-analyzer
description: Identify the market, regulatory, product, and behavior shifts that matter for the deal and write the MI: Trends workspace JSON.
allowed-tools: Read, Write, Grep, Glob, Edit, WebSearch, WebFetch
context: fork
---

# Skill: Trends Analyzer

## Purpose

Identify the structural trends that affect demand, product adoption, category timing, and risk for the company.

## Workspace I/O

- Read: `workspace/{deal-slug}/context/deal-context.json`
- Read: `workspace/{deal-slug}/sources.json` or a runner-provided temporary source registry
- Write: `workspace/{deal-slug}/analysis/trends.json`
- Update: the active source registry with every web source used

## What To Do

1. Find the few trends that materially change the investment view.
2. Classify each trend by direction, category, and time horizon.
3. Tie every trend back to the company’s actual product or buyer.
4. End with a short net assessment.

## Output Requirements

Write `analysis/trends.json` with:

- `tab_name: "MI: Trends"`
- one `Trends Table`
- a `Net Assessment` section

## Constraints

- Avoid generic category commentary that could apply to any startup.
- Use `Agent Notes` only when a trend is weakly evidenced, stale, or contradictory.

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
