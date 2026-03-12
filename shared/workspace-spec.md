# MI v3 Workspace Specification

This document defines the workspace contract for all MI v3 skills.

## Directory Structure

When MI v3 starts a new deal, it creates:

```text
workspace/
  {deal-slug}/
    meta.json
    sources.json
    context/
      deal-context.json
    sizing/
      top-down.json
      bottoms-up.json
    analysis/
      value-chain.json
      trends.json
      competitors.json
      feature-comparison.json
      meta-review.json
    validation/
      whale-watch.json
      anti-feku.json
    output/
      {CompanyName}_Market_Intelligence.xlsx
```

## `meta.json`

Required fields:

```json
{
  "deal_slug": "ninenine-ai",
  "company_name": "NineNine AI",
  "analyst": "Mehul",
  "created_at": "2026-03-10T14:30:00Z",
  "level": "L2",
  "skills_requested": ["deal-context-builder", "market-sizing-top-down"],
  "skills_completed": [],
  "workspace_version": "3.0"
}
```

Rules:

- `deal_slug` is the workspace folder name.
- `skills_completed` is append-only.

## Skill Output Envelope

Every skill output file uses:

```json
{
  "skill": "market-sizing-top-down",
  "tab_name": "Top Down",
  "summary": "TAM for the global fraud detection market is approximately $32B (2025)...",
  "tables": [],
  "sections": [],
  "source_refs": ["src_001"]
}
```

Required: `skill`, `tab_name`, `summary`, `tables`.

Optional: `sections`, `source_refs`, and skill-specific fields (`open_questions`, `sizing_approach`, `value_chain_layers`, `company_position`).

## Table Schema

```json
{
  "id": "credible-analyst-numbers",
  "label": "Credible Analyst Numbers",
  "headers": ["Market Terminology", "Geography", "TAM (Year)", "CAGR", "Source", "Agent Notes"],
  "rows": []
}
```

Rules:

- `headers` must match `tab-contracts.md` for template tabs.
- The xlsx builder owns column widths and styling.

## Row Schema

```json
{
  "data": ["cell1", "cell2", "cell3", "cell4"],
  "source_refs": ["src_001"],
  "type": "data"
}
```

Allowed types: `data`, `section_header`, `total`, `empty`.

Rules:

- `data` length must match `headers`.
- `section_header` rows put the label in the first cell of `data`.
- `total` rows are rendered bold automatically.
- `source_refs` must only contain IDs present in `sources.json`.

## Section Schema

For non-tabular content:

```json
{
  "id": "gut-check",
  "label": "Gut Check",
  "content": "The broad fraud detection market is venture-scale..."
}
```

Use `content` for text or `items` for bullet lists.

## `sources.json`

```json
{
  "deal_slug": "ninenine-ai",
  "sources": {
    "src_001": {
      "url": "https://example.com/report",
      "publisher": "MarketsandMarkets",
      "title": "Fraud Detection Market Report 2025",
      "tier": 2,
      "date_accessed": "2026-03-10",
      "used_by_skills": ["market-sizing-top-down"]
    }
  }
}
```

Rules:

- Source IDs use `src_NNN` format. New ID = `src_` + (count of existing sources + 1).
- Before adding a source, check for an existing entry with the same URL.
- Append the current skill name to `used_by_skills` if not already present.

## Skill I/O Rules

Every skill must:

1. Read `meta.json`.
2. Read any prerequisite workspace JSON listed in its instructions.
3. Read `sources.json` before adding new citations.
4. Write exactly one primary output file unless the skill is a runner.
5. Update `sources.json` if it used any new web sources.
6. Keep `skills_completed` in `meta.json` accurate when the skill finishes.

Parallel groups may use temporary source registries such as `sources.trends.json` and merge them back into `sources.json` by URL after the group completes.
