# Audit Report: `resources.qmd`

## Issues Found
- Some broad claims in the overview were not explicitly tied to concrete sources.
- Paper entries in the "Key Papers" and "Preprints & Recent Work" sections used a trailing `[link]` format, so the paper title mentions themselves were not clickable.
- One entry used ambiguous date notation ("2023+") and slightly over-broad wording ("Evolving methodology...") without precise grounding.

## Fixes Made
- Added explicit supporting links in the overview sentence about multi-benchmark evaluation practice:
  - HELM
  - Dynabench
  - MT-Bench/Arena
- Converted major paper/resource mentions in these sections to clickable title links while keeping structure/style intact:
  - Foundational Survey & Taxonomy References
  - Trustworthy Evaluation Frameworks
  - Preprints & Recent Work
- Replaced "2023+" with "2023" for MT-Bench/Arena and softened/clarified the description to avoid overclaim.

## Citation/Reference Consistency Notes
- No citation keys were introduced or changed in `resources.qmd`; references are URL-based in this file.
- Therefore, no edits to `references.bib` were required.

## Remaining Uncertainties
- I did not perform live HTTP validation for every external link (network checks not run), but links are syntactically valid and not placeholder-like.
- `HaluEval` is listed with an arXiv link in the table and appears plausible, though it is not present in `references.bib` (not currently an issue since this file does not use bib citations).
