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
- `workspace_version` must be `"3.0"`.
- `skills_completed` is append-only.

## Common Skill JSON Envelope

Every skill output file uses this envelope:

```json
{
  "schema_version": "3.0",
  "skill": "market-sizing-top-down",
  "tab_name": "Top Down",
  "generated_at": "2026-03-10T15:00:00Z",
  "summary": "TAM for the global fraud detection market is approximately $32B (2025)...",
  "tables": [],
  "sections": [],
  "source_refs": ["src_001"]
}
```

Required top-level fields:

- `schema_version`
- `skill`
- `tab_name`
- `generated_at`
- `summary`
- `tables`

Optional top-level fields:

- `sections`
- `source_refs`
- skill-specific fields such as `open_questions`, `sizing_approach`, `value_chain_layers`, `company_position`

The `tab_name` should follow the MI naming rules even if the xlsx builder later normalizes invalid Excel characters.

## Table Schema

Each item in `tables` follows:

```json
{
  "id": "credible-analyst-numbers",
  "label": "Credible Analyst Numbers",
  "type": "data",
  "headers": ["Market Terminology", "Geography", "TAM (Year)", "CAGR", "Source", "Agent Notes"],
  "column_widths": [40, 18, 15, 12, 40, 35],
  "rows": []
}
```

Rules:

- `headers` must match `tab-contracts.md` for template tabs.
- `column_widths` should match the number of headers.
- `type` is informational. The xlsx builder uses row-level `type` for styling.

## Row Schema

Each item in `tables[].rows` follows:

```json
{
  "data": ["cell1", "cell2", "cell3", "cell4"],
  "source_refs": ["src_001"],
  "bold": false,
  "type": "data"
}
```

Allowed row types:

- `data`
- `section_header`
- `total`
- `empty`

Rules:

- `data` rows must have the same number of cells as `headers`.
- `section_header` rows should put the section label in `text`, or in the first cell of `data`.
- `total` rows should set `bold: true`.
- `source_refs` must only contain IDs present in `sources.json`.

## Section Schema

`sections` is for non-tabular content:

```json
{
  "id": "gut-check",
  "label": "Gut Check",
  "type": "summary_block",
  "text": "The broad fraud detection market is venture-scale..."
}
```

Common section types:

- `summary_block`
- `bullet_list`
- `open_questions`

Rules:

- Use `text` for paragraph content.
- Use `items` for bullet-like lists.

## `sources.json`

The shared source registry follows:

```json
{
  "schema_version": "3.0",
  "deal_slug": "ninenine-ai",
  "sources": {
    "src_001": {
      "id": "src_001",
      "url": "https://example.com/report",
      "publisher": "MarketsandMarkets",
      "title": "Fraud Detection Market Report 2025",
      "tier": 2,
      "source_type": "research_report",
      "date_accessed": "2026-03-10",
      "publication_date": "2025",
      "used_by": [
        {
          "skill": "market-sizing-top-down",
          "table": "credible-analyst-numbers",
          "row_index": 0
        }
      ]
    }
  },
  "next_id": 2
}
```

Rules:

- Source IDs must use the `src_NNN` format.
- Before adding a source, check for an existing entry with the same URL.
- `next_id` always points to the next unused numeric ID.
- `used_by` tracks every row that cites the source.

## Skill I/O Rules

Every skill must:

1. Read `meta.json`.
2. Read any prerequisite workspace JSON listed in its instructions.
3. Read `sources.json` before adding new citations.
4. Write exactly one primary output file unless the skill is a runner.
5. Update `sources.json` if it used any new web sources.
6. Keep `skills_completed` in `meta.json` accurate when the skill finishes.

Parallel groups may use temporary source registries such as `sources.trends.json` and merge them back into `sources.json` by URL after the group completes.
