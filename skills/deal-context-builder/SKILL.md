---
name: deal-context-builder
description: Build the deal workspace, initialize meta and source registry files, and write the Pre-Requisites output for MI v3.
allowed-tools: Read, Write, Grep, Glob, Edit, Bash, WebSearch, WebFetch
---

# Skill: Deal Context Builder

## Purpose

Start MI v3 for a deal. This skill creates the workspace, initializes `meta.json` and `sources.json`, and writes `context/deal-context.json`.

## Workspace I/O

- Read: deal folder materials, analyst prompt, existing workspace files if present
- Write: `workspace/{deal-slug}/meta.json`
- Write: `workspace/{deal-slug}/sources.json`
- Write: `workspace/{deal-slug}/context/deal-context.json`

## What To Do

1. Derive a stable `deal_slug` from the company name or analyst-provided slug.
2. Create the workspace directory tree if it does not exist.
3. Initialize `meta.json` with the analyst, timestamp, level, requested skills, empty `skills_completed`, and `workspace_version: "3.0"`.
4. Initialize `sources.json` if it does not exist.
5. Read the deal materials and answer the Pre-Requisites checklist.
6. Recommend a sizing approach and capture open questions that block later analysis.

## Output Requirements

Write `context/deal-context.json` using the JSON envelope below.

Required content:

- `tab_name: "Pre-Requisites"`
- one table with headers `S No. | Pre-Requisites | Answer | Source | Agent Notes`
- top-level `open_questions`
- top-level `sizing_approach`
- sections for sizing approach recommendation and open questions

## Constraints

- Keep unknown answers blank and explain the gap in `Agent Notes` only when it matters.
- Use the existing source format in visible cells and preserve URLs in `sources.json`.
- Do not infer pricing, traction, or valuation unless the materials justify it.

## Workspace Setup

Create this directory tree:

```
workspace/{deal-slug}/
  meta.json
  sources.json
  context/
  sizing/
  analysis/
  validation/
  output/
```

`meta.json`: `{ "deal_slug", "company_name", "analyst", "created_at" (ISO 8601), "level" ("L1"|"L2"), "skills_requested": [], "skills_completed": [], "workspace_version": "3.0" }`

`sources.json`: `{ "deal_slug", "sources": {} }`

### Tab Headers

| S No. | Pre-Requisites | Answer | Source | Agent Notes |

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
