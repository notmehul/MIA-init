---
name: competitor-landscape
description: Build the competitor landscape, grouped by category, and write the Competitor Analysis workspace JSON.
allowed-tools: Read, Grep, Glob, Edit, WebSearch, WebFetch
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

## References

- `../../shared/workspace-spec.md`
- `../../shared/output-format-spec.md`
- `../../shared/source-credibility-guidelines.md`
- `../../shared/constraints.md`
- `../../shared/tab-contracts.md`
