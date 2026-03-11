# Source Credibility Guidelines

These guidelines apply to all MI v3 skills.

## Credible Sources

### Tier 1: Primary Official

- Government filings and regulators: SEBI, ROC, RBI, SEC, IRDAI
- DRHPs and red herring documents
- Annual reports of public companies
- Form S-1 filings and other statutory disclosures
- Big Four sector reports when methodology is disclosed
- MBB reports when methodology is disclosed

### Tier 2: Reputable Research

- Gartner, Forrester, Grand View Research, MarketsandMarkets, IMARC, BCC Research, Mordor Intelligence, Allied Market Research
- Industry bodies such as NASSCOM and trade associations
- Reuters, Bloomberg, ET, Mint for events and quotes
- World Bank, UN agencies, WHO for macro or social data

### Tier 3: Usable With Caution

- Consultant reports produced for one company
- Reddit, Twitter/X, or community forums for sentiment only
- G2, Capterra, Product Hunt for reviews and feature signals
- Company blogs, marketing pages, and press releases

## Non-Credible Sources For Numbers

- Statista
- SEO-driven market-size blog posts
- Wikipedia as a final source
- AI-generated summaries without a primary source

## How To Judge An Unfamiliar Source

Check:

1. Whether methodology is disclosed
2. Whether sample size and scope are concrete
3. Whether the publisher has a conflict of interest
4. Whether the claim can be corroborated independently

## URL Preservation

Every web source used in MI v3 must be preserved in `sources.json` with:

- full URL
- publisher
- title
- tier
- source type
- access date

Do not drop URLs after copying the human-readable citation into a table cell.

## Source Deduplication

Before creating a new source entry:

1. Check whether the same URL already exists in `sources.json`.
2. Reuse the existing `src_NNN` ID when it does.
3. Append the new row usage to `used_by`.

## Citation Format

Visible source cells use the same human-readable format as MI v2:

- `(Source) - [Publisher/Document Name]`
- `Calculated field`
- `Through Primary Research`
- `Assumption - [rationale]`

The builder uses `source_refs` to attach hyperlinks without changing the visible text.
