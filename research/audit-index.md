# Audit Report: `index.qmd`

Date: 2026-03-18

## Issues Found

1. **Unsupported/overstrong claims in intro and impact section**
   - Several statements (prompt sensitivity, response-shifting under user pressure, reproducibility/evaluation implications) were presented without citations.
   - Some phrasing was stronger than evidence warranted (e.g., universal-style claims).

2. **Citation coverage gaps for factual assertions**
   - The "Why This Matters" bullets made empirical claims without references.

3. **Hyperlink/clickability check**
   - Internal navigation/resource mentions were already linked (taxonomy/category pages, resources page, GitHub link).
   - No obvious placeholder or malformed links found.

## Fixes Made

- Added targeted citations in the opening paragraph:
  - `@lu2022orderedprompts`, `@sclar2023spurious`, `@perez2022modelwritten`
- Revised wording in the opening paragraph to reduce overclaiming (e.g., "may shift" / "can abandon prior claims").
- Rewrote all bullets in **Why This Matters** to be evidence-backed and slightly more cautious, adding citations:
  - Reproducibility/prompt sensitivity: `@lu2022orderedprompts`, `@liang2022helm`
  - Deployed variability: `@zhu2023promptbench`, `@sclar2023spurious`
  - Trust calibration/uncertainty mismatch: `@kadavath2022know`, `@xiong2023express`
  - Evaluation validity/prompt-template effects: `@lu2022orderedprompts`, `@liang2022helm`
  - Alignment/auditing relevance: `@ouyang2022instructgpt`, `@bai2022constitutional`
- Confirmed all newly used citation keys exist in `references.bib`.

## Remaining Uncertainties

- The specific claim about models "shifting answers to match user cues" is reasonably supported by broad behavior-discovery evidence (`@perez2022modelwritten`) but not by a dedicated sycophancy-specific citation in this bibliography. Current phrasing was softened accordingly.
- I did not validate external URL reachability over network; links are syntactically valid-looking and non-placeholder.
