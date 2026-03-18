# Audit Report: `factual-consistency.qmd`

## Issues found
- A few statements were slightly over-strong (e.g., "foundational," "canonical," "strongest mitigation stacks") without explicit supporting citation in-line.
- One entry had a placeholder-style venue label ("venue unconfirmed") for ALCE.
- The intrinsic/extrinsic hallucination distinction was presented without a directly attached citation in the overview paragraph.

## Fixes made
- Softened overclaims while preserving style/structure:
  - "foundational" → "early influential"
  - "heavily influenced" → "informed many later"
  - "canonical" → "widely adopted"
  - "strongest mitigation stacks" → "robust mitigation stacks often"
- Added direct supporting citation link for the intrinsic/extrinsic distinction in the overview:
  - Ji et al. (2023) survey link: <https://arxiv.org/abs/2202.03629>
- Replaced "venue unconfirmed" for ALCE with "arXiv preprint" to avoid placeholder/broken-status wording.
- Checked that paper/resource mentions in the file are accompanied by clickable links and that links appear valid-looking (no obvious placeholders).

## References/bibliography consistency
- No BibTeX keys or `references.bib` entries were modified.
- Existing content remains consistent with current `references.bib` usage patterns in this file (direct links rather than in-text citation keys).

## Remaining uncertainties
- Links were reviewed for format/plausibility, but not all were live-HTTP validated in this pass.
- Some benchmark rows (e.g., FRANK/TRUE/HaluEval/ALCE) use direct links without corresponding explicit BibTeX entries in `references.bib`; this is structurally fine for the current file format, but could be standardized later if the project migrates to citation-key-driven rendering.
