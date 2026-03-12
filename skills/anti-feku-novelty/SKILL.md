---
name: anti-feku-novelty
description: Pressure-test the company’s claims, risks, and novelty after the rest of the MI workspace has been built.
allowed-tools: Read, Write, Grep, Glob, Edit, WebSearch, WebFetch
context: fork
---

# Skill: Anti-Feku + Novelty

## Purpose

Run the final skepticism pass. Pressure-test the claims, surface the biggest risks, and assess whether the company is genuinely novel or just re-labeled category work.

## Workspace I/O

- Read: every JSON file available under `workspace/{deal-slug}`
- Read: `workspace/{deal-slug}/sources.json`
- Write: `workspace/{deal-slug}/validation/anti-feku.json`
- Update: the active source registry with any new web sources used

## What To Do

1. Read the entire workspace before making judgments.
2. Push back on unsupported founder claims.
3. Distinguish novelty in product, wedge, GTM, or market timing from plain execution risk.
4. End with a bottom line that the analyst can act on.

## Output Requirements

Write `validation/anti-feku.json` with:

- `tab_name: "MI: Anti-Feku"`
- tables for `Claim Pushback Table`, `Top Risks`, and `Novelty Score`
- a `Bottom Line` section

## Constraints

- Critique the evidence, not the founder.
- Every pushback claim needs a concrete basis in the workspace or in cited sources.
- Novelty is not the same as market attractiveness.

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
