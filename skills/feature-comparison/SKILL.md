---
name: feature-comparison
description: Compare product capabilities, pricing, and business-model UX across the most relevant competitors and write the Feature Comparison workspace JSON.
allowed-tools: Read, Grep, Glob, Edit, WebSearch, WebFetch
context: fork
---

# Skill: Feature Comparison

## Purpose

Build an L2 comparison across features, pricing, and business-model or UX choices for the most relevant comparable products.

## Workspace I/O

- Read: `workspace/{deal-slug}/context/deal-context.json`
- Read: `workspace/{deal-slug}/analysis/competitors.json`
- Read: `workspace/{deal-slug}/sources.json` or a runner-provided temporary source registry
- Write: `workspace/{deal-slug}/analysis/feature-comparison.json`
- Update: the active source registry with every web source used

## What To Do

1. Select only the comparables that matter for product benchmarking.
2. Build separate tables for the feature matrix, pricing, and business-model or UX differences.
3. Finish with a differentiation assessment that states what is actually distinct.

## Output Requirements

Write `analysis/feature-comparison.json` with:

- `tab_name: "Feature Comparison"`
- tables for `Feature Matrix`, `Pricing Comparison`, and `Business Model & UX`
- a `Differentiation Assessment` section

## Constraints

- Skip this skill when the market does not have product-comparable competitors.
- Keep feature claims grounded in official docs, pricing pages, or reputable reviews.
- Do not confuse marketing copy with real product capability.

## References

- `../../shared/workspace-spec.md`
- `../../shared/output-format-spec.md`
- `../../shared/source-credibility-guidelines.md`
- `../../shared/constraints.md`
- `../../shared/tab-contracts.md`
