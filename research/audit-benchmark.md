# Audit Report: `benchmark-reliability.qmd`

## Issues Found
- A few statements in the Overview were phrased as categorical claims (e.g., “highly sensitive,” “threats dominate”) without hedging.
- Two venue labels were potentially misleading/inconsistent with how the linked resources are presented:
  - `Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena` was labeled as a NeurIPS ecosystem item rather than clearly as arXiv/LMSYS.
  - `G-Eval` used the vague label “EMNLP line” while linking to arXiv.
- No obvious broken placeholder links were found, but several entries are arXiv-only where venue assignment can drift over time.

## Fixes Made
- Softened over-strong framing in Overview to better match evidence strength:
  - “are highly sensitive” → “can be highly sensitive”
  - “threats dominate” → “threats are repeatedly documented”
  - “strict metadata” → “stronger metadata”
- Standardized/clarified venue labeling for judge-related papers:
  - MT-Bench/Arena entry changed to `arXiv (LMSYS)`
  - G-Eval entry changed to `arXiv`
- Verified that all paper/resource mentions in this file remain clickable via explicit links.

## Remaining Uncertainties
- `benchmark-reliability.qmd` uses manual inline links rather than citekeys from `references.bib`; this is consistent with the file’s current style, but bibliography-level synchronization is therefore partial by design.
- Some paper venue statuses (especially recent preprints) may evolve; if strict publication-venue accuracy is required, a periodic metadata refresh is advisable.
