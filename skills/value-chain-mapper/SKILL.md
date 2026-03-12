---
name: value-chain-mapper
description: Map the company’s spend pool, current alternatives, and adjacent opportunity set, then write the MI: Value Chain workspace JSON.
allowed-tools: Read, Write, Grep, Glob, Edit, WebSearch, WebFetch
context: fork
---

# Skill: Value Chain Mapper

## Purpose

Map where the company sits in the value chain, which spend pool it targets, how the problem is solved today, and what adjacent expansion paths are credible.

## Workspace I/O

- Read: `workspace/{deal-slug}/context/deal-context.json`
- Read: `workspace/{deal-slug}/sources.json` or a runner-provided temporary source registry
- Write: `workspace/{deal-slug}/analysis/value-chain.json`
- Update: the active source registry with every web source used

## What To Do

1. Identify the buyer, budget owner, spend pool, and current workflow.
2. Break the market into value-chain layers and mark the company’s position.
3. List current alternatives, including in-house work, consultants, and status quo.
4. Identify adjacent opportunities only when the expansion logic is believable.

## Output Requirements

Write `analysis/value-chain.json` with:

- `tab_name: "MI: Value Chain"`
- tables for `Spend Pool Detail`, `Current Alternatives`, and `Adjacent Opportunities`
- sections for `value_chain_map` and `summary`
- top-level `value_chain_layers`
- top-level `company_position`

## Constraints

- Compare against the real alternative, not just software competitors.
- Keep expansion paths specific and tied to buyer, workflow, or spend-pool adjacency.
- Flag weak assumptions in `Agent Notes`.

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
