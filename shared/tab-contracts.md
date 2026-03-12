# Biome MI Template Tab Contracts
#
# Source of truth: `sources/templates/Biome_ Market Intelligence Template.pdf`
# (extracted via `pdftotext -layout`).
#
# Purpose: keep MI v3 outputs consistent with the Biome template across reruns.
#
# Important conventions:
# - Leave unknown data cells blank. Do not use "N/A", "-", or "--".
# - Add an `Agent Notes` column as the LAST column in every table and keep it blank
#   unless you need to flag something that requires analyst attention.
# - When a tab exists in the Biome template, match the template's column headers
#   exactly, then append `Agent Notes` (even if the template doesn't show it).
#
# MI-only tabs (e.g., `MI: Trends`) define their own headers in their SKILL.md files.

## Pre-Requisites (Template Tab)

Template (PDF page 1) is a checklist-style section, rendered as a table.

Recommended columns (match first two, append rest):

| S No. | Pre-Requisites | Answer | Source | Agent Notes |

Notes:
- Keep `S No.` stable and ordered as the template expects.
- Use `Source` values like `Deal folder`, `(Source) - <Doc Name>`, or `Through Primary Research`.

## Bottoms Up (Template Tab)

Template (PDF pages 4-5).

Primary calculation table columns (match exactly, append notes):

| Approach | Estimate | Source/ Assumptions/ Comments | Agent Notes |

Also include a short "Target Customer (s) Buckets" list above the table.

## Top Down (Template Tab)

Template (PDF page 6) shows example "Credible Analysts" numbers and geography splits.
The template is less strict than other tabs; MI v3 uses two tables:

1) Credible Analyst Numbers:

| Market Terminology | Geography | TAM (Year) | CAGR | Source | Agent Notes |

2) Calculation Chain:

| Parameter | Estimate | Source/ Assumptions/ Comments | Agent Notes |

Notes:
- Use `(Source) - <Publisher/Doc>` for sourced rows, and `Calculated field` for derived rows.
- Record the year for every numeric input.

## Competitor Analysis (Template Tab)

Template headers (PDF page 7).

Required columns (match exactly, append notes):

| No. | Company (Competitors) | Description of Product/Service | Founding Year | USP | Traction/Revenue | Valuation | Investors | Funding | Key Features | So what? | Agent Notes |

Notes:
- `No.` should be sequential within each section (if you use section headers).
- Put missing info as blank and flag in `Agent Notes` if it matters.

## Feature Comparison (Template Tab)

Template headers (PDF page 8).

Primary matrix columns (match exactly, append notes):

| Features | Feature Description | Comp 1 [1] | Comp 2 | ... | Comp 10 | Agent Notes |

Notes:
- In many sheets, the placeholder `Comp N` columns may be renamed to actual competitor names. This is OK as long as column order stays consistent.

Template expectations:
- The same matrix typically includes rows for: `Business Model`, `Freemium or Paid`,
  `Brand Voice/Tone`, `UX/UI`, and a `Pricing` block (Free Trial / Individual / Team / Enterprise).
- Prefer a single matrix (paste-friendly). If you output additional tables, keep the primary
  matrix present and column-compatible with the template.
