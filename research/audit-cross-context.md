# Audit Report: `cross-context.qmd`

## Issues found
1. **Potential overclaiming in overview language**
   - Phrasing like “literature consistently shows” and prescriptive wording could read stronger than the cited evidence scope.
2. **Some claims in overview were not directly anchored to specific sources inline**
   - The high-level claims were plausible but not explicitly linked in the paragraph itself.
3. **Not all resource mentions were directly hyperlinked at mention site**
   - Several entries used plain bold names plus a separate “link” token/URL.
4. **Minor wording inconsistency**
   - “ICLR line” phrasing was informal/ambiguous.

## Fixes made
1. **Softened and tightened overview claims**
   - Replaced stronger generalized wording with more cautious phrasing.
   - Changed “requires perturbation testing” to “benefits from perturbation testing.”
2. **Added inline source anchors in overview**
   - Added direct links to Zhao et al. (2021), Lu et al. (2022), Sclar et al. (2023), and Wang et al. (2023) inside the narrative paragraph.
3. **Made paper/resource mentions directly clickable**
   - Converted all paper titles in “Key Papers” and “Preprints & Recent Work” to direct hyperlinks.
   - Linked practitioner resource titles directly (HF blog, OpenAI Cookbook, CRFM/HELM docs).
   - Linked benchmark names in the table and repo names in the GitHub section.
4. **Normalized wording**
   - Updated “ICLR line” → “ICLR.”

## Remaining uncertainties
1. **`references.bib` alignment (pre-existing gap):**
   - Multiple works listed in `cross-context.qmd` appear not to have corresponding entries in `references.bib` (e.g., Min et al. 2022, Wang et al. 2023 cross-lingual consistency, Shi et al. 2023, MMBench, MMMU, Look at the Labels).
   - I did **not** modify `references.bib` to avoid broader bibliography changes beyond the target file scope.
2. **MGSM citation granularity:**
   - The MGSM row links to the multilingual CoT paper (arXiv:2210.03057). This is commonly used but may not be the most specific standalone benchmark citation depending on project citation policy.
