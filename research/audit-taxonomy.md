# Audit Report: `taxonomy.qmd`

## Issues found

1. **Unsupported/overstrong claims**
   - Several key-insight statements were asserted without citations.
   - A few phrasings were too absolute (e.g., implying definitive conclusions about internal representations).

2. **Citation coverage gaps**
   - The taxonomy section made factual/meta-evaluative claims across categories (hallucination prevalence, CoT faithfulness limits, benchmark instability, etc.) without direct references.
   - Generator-validator claims were uncited despite referencing specific empirical patterns.

3. **Link/clickability checks**
   - Internal section links were present but needed validation against actual project files.

## Fixes made

- Added targeted citations (existing keys from `references.bib`) to support major factual claims in:
  - Factual consistency/hallucination
  - Self-consistency
  - Reasoning consistency
  - Behavioral consistency/sycophancy
  - Calibration/uncertainty
  - Cross-context sensitivity
  - Benchmark reliability
  - Generator-validator gap

- Softened overclaims by replacing absolute framing with evidence-aligned language (e.g., “suggests,” “at least partly,” “interpreted with care”).

- Kept structure/style intact:
  - No section reorganization
  - No added subsections
  - Minimal line edits to preserve tone and flow

- Verified internal links point to existing files in project root:
  - `factual-consistency.qmd`, `self-consistency.qmd`, `reasoning-consistency.qmd`, `behavioral-consistency.qmd`, `calibration.qmd`, `cross-context.qmd`, `benchmark-reliability.qmd`, `generator-validator-gap.qmd`

- Maintained consistency with `references.bib` by using only existing citation keys.

## Remaining uncertainties

- Citation clickability at render time depends on the project’s bibliography/citation configuration in Quarto (not audited here), but keys used are valid and present in `references.bib`.
- Some category bullets (e.g., specific subtype definitions) remain conceptual and uncited; they are taxonomy definitions rather than empirical claims, but could be additionally sourced if desired.
