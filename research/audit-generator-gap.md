# Audit Report: `generator-validator-gap.qmd`

## Issues found

1. **A few potentially over-broad claims** in the Overview and Key Insights used near-absolute wording (e.g., “All of them…”, “Reliable improvements usually require…”, “generally outperform…”), which could read as stronger than the cited evidence supports.
2. **Support for high-level factual claims** in the Overview was implicit rather than explicit; key statements were not directly linked to sources in that section.
3. **Paper/resource mentions were not uniformly hyperlinked as titles** in the paper lists (titles were plain text followed by a separate `[link]`), which is less robust for clickability/readability.

## Fixes made

1. **Softened overclaims** while preserving meaning and structure:
   - “All of them transform…” → “Many of these methods transform…”
   - “The gap also explains…” → “The gap also helps explain…”
   - “Reliable improvements usually require…” → “Strong gains typically come from…”
   - “generally outperform…” → “often outperform…”
2. **Added direct citation links in the Overview** to support key factual statements:
   - Cobbe et al. (2021), Lightman et al. (2023), Huang et al. (2023), Shinn et al. (2023).
3. **Made paper/resource mentions consistently clickable** by turning titles themselves into hyperlinks across:
   - Key Papers
   - Preprints & Recent Work
   - Blog Posts & Practitioner Resources
   - GitHub Repos
4. **Kept style/structure intact** (same section layout, same overall content density).

## Remaining uncertainties

1. **No live link-check was run** (network validation not performed here), but all links are valid-looking and non-placeholder.
2. **`references.bib` consistency:** this file still uses direct links rather than BibTeX citation keys; no `.bib` entries were edited. Existing mention-link consistency was preserved, but some cited works (e.g., DeepSeekMath, LM-as-an-Examiner) may or may not already exist in `references.bib` depending on broader project conventions.
