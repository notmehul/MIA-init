# MI v3 Output Format Specification

These conventions apply to all MI v3 skills.

## Primary Output Target

MI v3 writes structured JSON into the deal workspace. The final analyst deliverable is an xlsx workbook assembled by `build_mi_sheet.py`.

## Output Model

Each skill produces:

1. One workspace JSON file using the envelope from `workspace-spec.md`
2. Source references that point into `sources.json`

## Tables

Rules:

- For template tabs, headers must match `tab-contracts.md`.
- If a table includes `Agent Notes`, it must be the last column.
- Numbers must include units unless the header already implies them.
- Keep unknown data cells blank.
- Use row types to signal section headers, totals, or blank spacers.

## Source Cells

In row data, keep the human-readable source text in the relevant source column:

- `(Source) - <Publisher/Document>`
- `Calculated field`
- `Through Primary Research`
- `Assumption - <rationale>`

The hyperlink comes from `source_refs`, not from the visible cell text.

## Agent Notes

`Agent Notes` stays mostly empty. Use it only when:

- a source is weak or biased
- a number is stale
- two sources conflict
- a material inference was required
- the analyst must verify something before trusting the row

## Tab Naming

Use the Biome template tab names where they exist:

- `Pre-Requisites`
- `Top Down`
- `Bottoms Up`
- `Competitor Analysis`
- `Feature Comparison`

Use `MI: ...` for MI-only tabs:

- `MI: Value Chain`
- `MI: Trends`
- `MI: Meta Review`
- `MI: Whale Watch`
- `MI: Anti-Feku`

## Determinism

- Sort rows using explicit, skill-specific ordering rules.
- Prefer the most credible source first when multiple sources support the same metric.
- Keep section ordering stable across reruns.
