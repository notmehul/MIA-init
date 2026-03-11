---
name: anti-feku-novelty
description: Pressure-test the company’s claims, risks, and novelty after the rest of the MI workspace has been built.
allowed-tools: Read, Grep, Glob, Edit, WebSearch, WebFetch
context: fork
---

# Skill: Anti-Feku + Novelty

## Purpose

Run the final skepticism pass. Pressure-test the claims, surface the biggest risks, and assess whether the company is genuinely novel or just re-labeled category work.

## Workspace I/O

- Read: every JSON file available under `workspace/{deal-slug}`
- Read: `workspace/{deal-slug}/sources.json`
- Write: `workspace/{deal-slug}/validation/anti-feku.json`
- Update: the active source registry with any new web sources used

## What To Do

1. Read the entire workspace before making judgments.
2. Push back on unsupported founder claims.
3. Distinguish novelty in product, wedge, GTM, or market timing from plain execution risk.
4. End with a bottom line that the analyst can act on.

## Output Requirements

Write `validation/anti-feku.json` with:

- `tab_name: "MI: Anti-Feku"`
- tables for `Claim Pushback Table`, `Top Risks`, and `Novelty Score`
- a `Bottom Line` section

## Constraints

- Critique the evidence, not the founder.
- Every pushback claim needs a concrete basis in the workspace or in cited sources.
- Novelty is not the same as market attractiveness.

## References

- `../../shared/workspace-spec.md`
- `../../shared/output-format-spec.md`
- `../../shared/source-credibility-guidelines.md`
- `../../shared/constraints.md`
