---
name: meta-review
description: Review external sentiment, claims-versus-reality gaps, and recurring product signals, then write the MI: Meta Review workspace JSON.
allowed-tools: Read, Grep, Glob, Edit, WebSearch, WebFetch
context: fork
---

# Skill: Meta Review

## Purpose

Analyze review platforms, discussion forums, and public product sentiment to understand recurring strengths, gaps, and customer pain points.

## Workspace I/O

- Read: `workspace/{deal-slug}/context/deal-context.json`
- Read: `workspace/{deal-slug}/analysis/competitors.json`
- Read: `workspace/{deal-slug}/sources.json` or a runner-provided temporary source registry
- Write: `workspace/{deal-slug}/analysis/meta-review.json`
- Update: the active source registry with every web source used

## What To Do

1. Review credible public feedback sources for the relevant competitors.
2. Summarize recurring patterns instead of cherry-picking isolated quotes.
3. Compare marketed claims against what users actually report.
4. Capture the strongest opportunity signals for the company.

## Output Requirements

Write `analysis/meta-review.json` with:

- `tab_name: "MI: Meta Review"`
- tables for `Competitor Review Summary` and `Claims vs Reality Matrix`
- an `Opportunity Signals` section

## Constraints

- Use review platforms for product feedback, not market-size numbers.
- Skip this skill when public review coverage is too thin to be useful.
- Flag low-signal or biased review sources.

## References

- `../../shared/workspace-spec.md`
- `../../shared/output-format-spec.md`
- `../../shared/source-credibility-guidelines.md`
- `../../shared/constraints.md`
