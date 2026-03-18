# Audit Report: behavioral-consistency.qmd

## Issues found
- The **Overview** section made broad causal claims (alignment/preference optimization and judge bias) without immediate supporting links.
- One sentence was slightly over-strong: “Robust systems now treat … as standard checks.”
- Two venue labels were potentially imprecise/awkward:
  - “NeurIPS Datasets/Benchmarks ecosystem” for Zheng et al. (2023)
  - “EMNLP Findings-era” for G-Eval

## Fixes made
- Added direct clickable supporting links in the Overview for key factual claims:
  - Perez et al. (2022) for sycophancy evidence
  - Ouyang et al. (2022) and Bai et al. (2022) for alignment-objective framing
  - Zheng et al. (2023) and Liu et al. (2023, G-Eval) for judge bias framing
- Softened overclaim language:
  - Replaced “standard checks” wording with “many evaluation stacks include … as robustness checks.”
- Normalized potentially confusing venue descriptors:
  - Zheng et al. → “arXiv / widely used evaluation reference”
  - G-Eval → “arXiv”
- Verified all paper/resource mentions in this file are hyperlinked and clickable.

## Remaining uncertainties
- `From Yes-Men to Truth-Tellers` (Chen et al., 2024) remains included with arXiv link and “venue unconfirmed” note; this appears appropriate but should be revisited if final publication metadata is needed.
- Several works referenced in this file are not present in `references.bib`; no citation-key conversion was performed here to avoid introducing inconsistency without broader bibliography updates.

## Files changed
- `/home/node/.openclaw/workspace/Projects/llm-consistency-survey/behavioral-consistency.qmd`
- `/home/node/.openclaw/workspace/Projects/llm-consistency-survey/research/audit-behavioral.md`
