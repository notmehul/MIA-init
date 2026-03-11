# MI v3 Constraints

These rules apply to every MI v3 skill.

## Evidence Rules

- Every numeric claim must trace to a source, `Calculated field`, `Through Primary Research`, or `Assumption - [rationale]`.
- Every market size statement must include value, year, geography, and source.
- When two credible sources disagree, show both and explain the discrepancy in `Agent Notes`.
- Calculated fields must show the derivation.

## Anti-Speculation Rules

- Do not make forward-looking projections unless the source itself reports the projection.
- Do not write speculative language such as "could potentially", "may grow to", or "is expected to" without a cited source.
- Do not turn weak directional evidence into a quantitative estimate.
- Do not claim a market is large, attractive, or venture-scale without a traceable numeric chain.

## Source Discipline

- Prefer Tier 1 and Tier 2 sources from `source-credibility-guidelines.md`.
- If only Tier 3 material exists, use it sparingly and flag it in `Agent Notes`.
- Do not use AI-generated summaries as sources.
- Preserve every used URL in `sources.json`.

## Output Discipline

- Keep data cells blank instead of inventing placeholders.
- Use `Agent Notes` only for issues an analyst should notice.
- Preserve deterministic ordering so reruns are comparable.
