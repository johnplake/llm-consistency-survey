# Audit Report: `reasoning-consistency.qmd`

## Issues Found

1. **Unsupported/high-level claims in Overview**
   - The Overview made several strong factual claims (process-outcome mismatch, CoT faithfulness limits, trend toward verifier/process supervision) without direct supporting links in that section.

2. **A couple of potentially over-strong phrasings**
   - ReAct summary implied a broad reduction in "unsupported internal speculation," which is stronger than what is typically established across settings.
   - Reflexion summary phrasing ("works best with external success signals") was plausible but somewhat absolute.

3. **Hyperlink coverage check**
   - Paper/resource entries were largely linked already; no obvious placeholder links like `TODO`, `example.com`, or malformed markdown links were found.

## Fixes Made

1. **Added explicit supporting links in the Overview**
   - Added direct links to:
     - Turpin et al. (2023): <https://arxiv.org/abs/2305.04388>
     - Wei et al. (2022): <https://arxiv.org/abs/2201.11903>
     - Kojima et al. (2022): <https://arxiv.org/abs/2205.11916>
     - Cobbe et al. (2021): <https://arxiv.org/abs/2110.14168>
     - Lightman et al. (2023): <https://arxiv.org/abs/2305.20050>
     - Tree of Thoughts: <https://arxiv.org/abs/2305.10601>

2. **Softened overclaims while preserving structure/style**
   - ReAct note revised to: improved traceability / reduced implicit reasoning on tool-using tasks (more bounded claim).
   - Reflexion note revised to: typically paired with external task feedback/signals (less absolute).

3. **Citation/link integrity pass**
   - Confirmed all paper/resource mentions in this file have clickable links.
   - Confirmed links are valid-looking and not obvious placeholders.

## Remaining Uncertainties

1. **`references.bib` coverage for all listed papers**
   - This section currently uses inline links rather than citation keys. Some listed papers (e.g., Faithful Chain-of-Thought by Lyu et al.) may not have corresponding entries in `references.bib`.
   - No bib-key conversion was performed to avoid unnecessary structural changes; if the project later standardizes on `@citekey` citations, a dedicated bib harmonization pass would be useful.
