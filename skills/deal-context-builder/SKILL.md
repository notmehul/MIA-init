---
name: deal-context-builder
description: Build the deal workspace, initialize meta and source registry files, and write the Pre-Requisites output for MI v3.
allowed-tools: Read, Grep, Glob, Edit, WebSearch, WebFetch
---

# Skill: Deal Context Builder

## Purpose

Start MI v3 for a deal. This skill creates the workspace, initializes `meta.json` and `sources.json`, and writes `context/deal-context.json`.

## Workspace I/O

- Read: deal folder materials, analyst prompt, existing workspace files if present
- Write: `workspace/{deal-slug}/meta.json`
- Write: `workspace/{deal-slug}/sources.json`
- Write: `workspace/{deal-slug}/context/deal-context.json`

## What To Do

1. Derive a stable `deal_slug` from the company name or analyst-provided slug.
2. Create the workspace directory tree if it does not exist.
3. Initialize `meta.json` with the analyst, timestamp, level, requested skills, empty `skills_completed`, and `workspace_version: "3.0"`.
4. Initialize `sources.json` if it does not exist.
5. Read the deal materials and answer the Pre-Requisites checklist.
6. Recommend a sizing approach and capture open questions that block later analysis.

## Output Requirements

Write `context/deal-context.json` using the common envelope from `../../shared/workspace-spec.md`.

Required content:

- `tab_name: "Pre-Requisites"`
- one table with headers `S No. | Pre-Requisites | Answer | Source | Agent Notes`
- top-level `open_questions`
- top-level `sizing_approach`
- sections for sizing approach recommendation and open questions

## Constraints

- Keep unknown answers blank and explain the gap in `Agent Notes` only when it matters.
- Use the existing source format in visible cells and preserve URLs in `sources.json`.
- Do not infer pricing, traction, or valuation unless the materials justify it.

## References

- `../../shared/workspace-spec.md`
- `../../shared/output-format-spec.md`
- `../../shared/source-credibility-guidelines.md`
- `../../shared/constraints.md`
- `../../shared/tab-contracts.md`
