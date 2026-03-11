---
name: market-sizing-bottoms-up
description: Produce a bottoms-up market estimate with segment-level customer buckets, assumptions, and a cross-check against top-down sizing.
allowed-tools: Read, Grep, Glob, Edit, WebSearch, WebFetch
context: fork
---

# Skill: Market Sizing - Bottoms Up

## Purpose

Cross-check the market with a segment-by-segment bottoms-up model grounded in customer counts, adoption, and deal-size logic.

## Workspace I/O

- Read: `workspace/{deal-slug}/context/deal-context.json`
- Read: `workspace/{deal-slug}/sizing/top-down.json`
- Read: `workspace/{deal-slug}/sources.json` or a runner-provided temporary source registry
- Write: `workspace/{deal-slug}/sizing/bottoms-up.json`
- Update: the active source registry with every web source used

## What To Do

1. Define the target customer buckets explicitly.
2. Estimate customer counts, adoption assumptions, and ACV ranges by segment.
3. Build one visible calculation chain with segment headers, totals, and the final TAM, SAM, SOM rows.
4. Cross-check the output against the top-down result and explain the gap.

## Output Requirements

Write `sizing/bottoms-up.json` with:

- `tab_name: "Bottoms Up"`
- one `Calculation Chain` table
- section-header rows for each customer segment
- sections for `target_customer_buckets`, `cross_check`, and `assumptions_list`

## Constraints

- Treat customer counts and ACV assumptions as assumptions unless a source supports them.
- Keep totals visible and easy to audit.
- If top-down is sufficient and the analyst explicitly skips this step, do not fabricate a bottoms-up model.

## References

- `../../shared/workspace-spec.md`
- `../../shared/output-format-spec.md`
- `../../shared/source-credibility-guidelines.md`
- `../../shared/constraints.md`
- `../../shared/tab-contracts.md`
