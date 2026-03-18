# Calibration Section Audit (`calibration.qmd`)

## Issues Found

1. **Unsupported high-level claim in Overview**
   - The statement about alignment methods (instruction tuning / preference optimization) affecting confidence behavior was plausible but uncited.

2. **Potential overclaim in semantic uncertainty summary**
   - The phrasing "often superior" to token entropy was too strong without narrowing conditions.

3. **Citation integrity check**
   - Most named papers/resources were already clickable.
   - No obvious placeholder/broken-style links (e.g., `TBD`, missing domains) were present.

## Fixes Made

1. **Added explicit clickable support for alignment-related confidence shift claim** in the Overview:
   - [InstructGPT](https://arxiv.org/abs/2203.02155)
   - [Constitutional AI](https://arxiv.org/abs/2212.08073)
   - [DPO](https://arxiv.org/abs/2305.18290)

2. **Softened semantic uncertainty overclaim**:
   - Changed from "often superior" to "can outperform ... in several settings," which is better calibrated to available evidence.

3. **Maintained structure and style**:
   - No section reorganization.
   - No added bloat; only targeted wording/citation edits.

## `references.bib` Consistency

- The newly cited papers are already present in `references.bib`:
  - `ouyang2022instructgpt`
  - `bai2022constitutional`
  - `rafailov2023dpo`
- No `.bib` edits were required.

## Remaining Uncertainties

- Link validity was checked for format/plausibility, not by live HTTP verification for every URL.
- Some resources remain arXiv links even when archival venues may exist; this is stylistically consistent with the current project but could be upgraded later if desired.
