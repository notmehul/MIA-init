# Biome MI (v3) Claude Code Plugin

This folder is the MI v3 Claude Code plugin.

## Load

From the repo root:

```bash
claude --plugin-dir ./skills/mi-v3
```

## Invoke

Skills are available as slash commands under the plugin namespace.

Primary entry points:

```text
/...:deal-context-builder
/...:mi-runner
```

## Validate

```bash
claude plugin validate ./skills/mi-v3
```

```bash
python3 scripts/build_mi_sheet.py workspace/<deal-slug>
```

## Layout

- `.claude-plugin/plugin.json`: plugin manifest
- `skills/*/SKILL.md`: skill definitions
- `shared/*`: workspace spec, constraints, source rules, output format

## What Changed From v2

- Skills write workspace JSON instead of paste-ready tables.
- `sources.json` preserves URLs and source metadata across all skills.
- `build_mi_sheet.py` turns workspace JSON into the final workbook.
- Forked skills use `context: fork` where isolation matters.