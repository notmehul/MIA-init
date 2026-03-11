---
name: market-sizing-top-down
description: Produce a top-down TAM, SAM, and SOM estimate with a visible calculation chain and workbook-ready JSON output.
allowed-tools: Read, Grep, Glob, Edit, WebSearch, WebFetch
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

Use row type `total` or `bold: true` for TAM, SAM, and SOM rows.

## Constraints

- Every number must have a source, be explicitly calculated, or be marked as an assumption with rationale.
- Do not create projections unless the source itself reports them.
- Do not hide weak assumptions. Flag them in `Agent Notes`.

## References

- `../../shared/workspace-spec.md`
- `../../shared/output-format-spec.md`
- `../../shared/source-credibility-guidelines.md`
- `../../shared/constraints.md`
- `../../shared/tab-contracts.md`
