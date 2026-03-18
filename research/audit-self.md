# Audit Report — `self-consistency.qmd`

## Issues found
- One potentially over-strong causal claim in the Overview (that self-consistency decoding works *precisely because* the model is inconsistent).
- One claim under TruthfulQA that read as too broad/definitive without direct support from the benchmark paper itself.
- One in-text paper mention in the Overview (“Wang et al. method”) was not directly hyperlinked at the mention point.

## Fixes made
- Softened the overclaim in the Overview to a more defensible interpretation:
  - from a strict causal assertion to a cautious statement about sampling diverse reasoning paths and majority selection.
- Reworded the TruthfulQA note to avoid overclaiming:
  - now states TruthfulQA is primarily a truthfulness benchmark and that prompt-variant use is a common practice in follow-on evaluations.
- Added a direct clickable hyperlink for the Wang et al. self-consistency method mention in the Overview.
- Verified that paper/resource mentions in lists/tables are clickable and links appear well-formed (no obvious placeholder/broken-format URLs).

## Remaining uncertainties
- `self-consistency.qmd` references several resources that do not appear to have entries in `references.bib` (e.g., HaluEval, ANLI, WinoGrande, Winogender as currently presented). This file currently uses direct hyperlinks rather than BibTeX citations, so rendering should still work; however, if the project’s preferred style is unified BibTeX-backed citation keys, those entries may need to be added later for full bibliography consistency.
