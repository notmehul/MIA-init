---
name: value-chain-mapper
description: Map the company’s spend pool, current alternatives, and adjacent opportunity set, then write the MI: Value Chain workspace JSON.
allowed-tools: Read, Grep, Glob, Edit, WebSearch, WebFetch
context: fork
---

# Skill: Value Chain Mapper

## Purpose

Map where the company sits in the value chain, which spend pool it targets, how the problem is solved today, and what adjacent expansion paths are credible.

## Workspace I/O

- Read: `workspace/{deal-slug}/meta.json`
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

## References

- `../../shared/workspace-spec.md`
- `../../shared/output-format-spec.md`
- `../../shared/source-credibility-guidelines.md`
- `../../shared/constraints.md`
