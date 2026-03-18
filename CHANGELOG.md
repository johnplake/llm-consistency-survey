# Changelog

All notable changes to this project are documented in this file.

## [2026-03-18] Generator-validator completeness pass

### Added
- Expanded `generator-validator-gap.qmd` with substantial missing literature across:
  - direct generation-vs-validation asymmetry evidence
  - self-correction boundary studies
  - verifier/process-supervision work (including process-vs-outcome feedback)
  - inference-time scaling via ranking/search/reranking
  - LLM-as-judge reliability as validator proxy
  - pre-LLM historical roots relevant to verify-after-generate framing
- Added a new **Coverage note** subsection in `generator-validator-gap.qmd` summarizing what this pass added.
- Added high-priority BibTeX entries to `references.bib` for newly introduced works, including:
  - Uesato et al. (2022)
  - Zelikman et al. (2022)
  - Krishna et al. (2023)
  - Jiang et al. (2023)
  - McCallum & Nigam (1998)

### Changed
- Tightened several claims in `generator-validator-gap.qmd` to remain evidence-backed and avoid overclaiming.
- Synced `research/07-generator-validator-gap.md` with a short completeness-pass note.

## [2026-03-18] Audit pass: consistency, sourcing, and link integrity

### Added
- Added **section-level audit reports** under `research/`:
  - `audit-index.md`
  - `audit-taxonomy.md`
  - `audit-factual.md`
  - `audit-self.md`
  - `audit-reasoning.md`
  - `audit-behavioral.md`
  - `audit-calibration.md`
  - `audit-cross-context.md`
  - `audit-benchmark.md`
  - `audit-resources.md`
  - `audit-generator-gap.md`

### Changed
- Performed a comprehensive second-pass audit across all section pages for:
  - unsupported/overstated claims
  - citation and hyperlink coverage
  - consistency of wording and venue labels
- Tightened language in multiple sections to avoid overclaiming.
- Added/updated direct clickable source links in overviews and key-paper sections.
- Improved clickability by hyperlinking paper/resource titles directly where needed.
- Updated taxonomy claims with evidence-backed citations and more bounded phrasing.
- Updated index-level framing with stronger source grounding.

### Notes
- Some sections use URL-first citations rather than strict BibTeX citekeys; this was preserved for readability and continuity.
- Remaining bibliography harmonization opportunities are documented in the per-section audit reports.

## [2026-03-18] Compilation pass: full site population

### Added
- New dedicated page: `generator-validator-gap.qmd`

### Changed
- Populated all major section pages from research notes:
  - `factual-consistency.qmd`
  - `self-consistency.qmd`
  - `reasoning-consistency.qmd`
  - `behavioral-consistency.qmd`
  - `calibration.qmd`
  - `cross-context.qmd`
  - `benchmark-reliability.qmd`
  - `resources.qmd`
- Updated `_quarto.yml` navbar and render list to include generator-validator gap page.
- Expanded `taxonomy.qmd` with a generator-validator gap cross-cutting concept section.
- Populated `references.bib` with survey bibliography entries.
