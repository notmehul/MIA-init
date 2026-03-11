---
name: mi-runner
description: Orchestrate MI v3 through workspace initialization, phased skill execution, source-registry-safe parallel groups, and incremental workbook builds.
disable-model-invocation: true
allowed-tools: Read, Grep, Glob, Edit, Bash
---

# Skill: MI Runner

## Purpose

Run MI v3 as a phased workspace workflow. The deliverable is the workbook produced from workspace JSON, not a pasted table stream.

## Phase Plan

### Phase 1: Understand

1. Run `deal-context-builder` in the main context.
2. Run `value-chain-mapper` unless the analyst explicitly skips it.
3. Run `python3 scripts/build_mi_sheet.py workspace/{deal-slug}`.

### Phase 2: Size

4. Run `market-sizing-top-down`.
5. Run `market-sizing-bottoms-up` unless the analyst explicitly says top-down is sufficient.
6. Rebuild the workbook.

### Phase 3: Analyze

7. Run `trends-analyzer` and `competitor-landscape`.
8. After competitors complete, run `feature-comparison` and `meta-review` for L2 when relevant.
9. Rebuild the workbook.

### Phase 4: Validate

10. Run `whale-watch` when the customer universe needs validation.
11. Run `anti-feku-novelty`.
12. Rebuild the final workbook.

## Runner Rules

- Treat the workspace as the system of record.
- Only run a skill once its required workspace inputs exist.
- Respect each skill’s declared `context: fork`.
- After every completed skill, update `meta.json`.
- When running a parallel group, do not let multiple skills write the main `sources.json` at the same time.
  - Give each parallel skill a temporary registry path such as `sources.trends.json`.
  - Merge those registries back into `sources.json` by URL, merge `used_by`, and recalculate `next_id`.
- Skip missing or analyst-rejected phases cleanly.

## Completion Summary

At the end, report:

- skills completed
- skills skipped and why
- the workbook path
- all warnings aggregated from `Agent Notes`
- all open questions from `deal-context.json`

## References

- `../../shared/workspace-spec.md`
- `../../shared/output-format-spec.md`
- `../../shared/source-credibility-guidelines.md`
- `../../shared/constraints.md`
