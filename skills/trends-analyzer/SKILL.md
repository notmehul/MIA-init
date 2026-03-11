---
name: trends-analyzer
description: Identify the market, regulatory, product, and behavior shifts that matter for the deal and write the MI: Trends workspace JSON.
allowed-tools: Read, Grep, Glob, Edit, WebSearch, WebFetch
context: fork
---

# Skill: Trends Analyzer

## Purpose

Identify the structural trends that affect demand, product adoption, category timing, and risk for the company.

## Workspace I/O

- Read: `workspace/{deal-slug}/context/deal-context.json`
- Read: `workspace/{deal-slug}/sources.json` or a runner-provided temporary source registry
- Write: `workspace/{deal-slug}/analysis/trends.json`
- Update: the active source registry with every web source used

## What To Do

1. Find the few trends that materially change the investment view.
2. Classify each trend by direction, category, and time horizon.
3. Tie every trend back to the company’s actual product or buyer.
4. End with a short net assessment.

## Output Requirements

Write `analysis/trends.json` with:

- `tab_name: "MI: Trends"`
- one `Trends Table`
- a `Net Assessment` section

## Constraints

- Avoid generic category commentary that could apply to any startup.
- Use `Agent Notes` only when a trend is weakly evidenced, stale, or contradictory.

## References

- `../../shared/workspace-spec.md`
- `../../shared/output-format-spec.md`
- `../../shared/source-credibility-guidelines.md`
- `../../shared/constraints.md`
