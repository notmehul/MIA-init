---
name: whale-watch
description: Map potential customers, market concentration, and founder claim cross-checks, then write the MI: Whale Watch workspace JSON.
allowed-tools: Read, Grep, Glob, Edit, WebSearch, WebFetch
context: fork
---

# Skill: Whale Watch

## Purpose

Test whether the target market has enough credible customers, whether revenue is likely to concentrate, and whether the founder’s GTM story matches the market structure.

## Workspace I/O

- Read: `workspace/{deal-slug}/context/deal-context.json`
- Read: `workspace/{deal-slug}/analysis/value-chain.json`
- Read: `workspace/{deal-slug}/analysis/competitors.json`
- Read: `workspace/{deal-slug}/sources.json` or a runner-provided temporary source registry
- Write: `workspace/{deal-slug}/validation/whale-watch.json`
- Update: the active source registry with every web source used

## What To Do

1. Build a potential customer list grouped by tiers.
2. Estimate concentration risk and budget concentration.
3. Cross-check the founder’s target-customer narrative against the observable market.

## Output Requirements

Write `validation/whale-watch.json` with:

- `tab_name: "MI: Whale Watch"`
- a `Potential Customer List` table with tier headers
- a `Market Concentration` table
- a `Founder Claims Crosscheck` section

## Constraints

- Focus on real buyers, not abstract TAM buckets.
- Flag customer lists that rely too heavily on inference or weak proxies.

## References

- `../../shared/workspace-spec.md`
- `../../shared/output-format-spec.md`
- `../../shared/source-credibility-guidelines.md`
- `../../shared/constraints.md`
