# GV-Q6: Evaluation design artifact vs true inconsistency

## Scope
This note targets papers that **separate genuine model inconsistency** from inconsistency induced by:
- prompt framing / template choice,
- forced-choice vs free generation interfaces,
- metric and protocol sensitivity,
- benchmark design effects (position/length/context effects).

Excluded: generic benchmark criticism without a concrete diagnostic protocol.

## Papers added to Zotero
Target collection: `LLM-inconsistency / GV-Evaluation-design-artifact-vs-inconsistency`

Added 10 high-relevance papers (all with PDFs attached):

1. **Calibrate Before Use: Improving Few-Shot Performance of Language Models** (2021)  
   Zotero key: `EJ9WKDHV`
2. **Fantastically Ordered Prompts and Where to Find Them: Overcoming Few-Shot Prompt Order Sensitivity** (2022)  
   Zotero key: `FHME8CQ7`
3. **Quantifying Language Models' Sensitivity to Spurious Features in Prompt Design** (2023)  
   Zotero key: `G6BUTZ5I`
4. **PromptBench: Towards Evaluating the Robustness of Large Language Models on Adversarial Prompts** (2023)  
   Zotero key: `FHH789NP`
5. **Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena** (2023)  
   Zotero key: `SQUJX9I6`
6. **Large Language Models are not Fair Evaluators** (2024)  
   Zotero key: `7HIJ83Q4`
7. **G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment** (2023)  
   Zotero key: `DCVQSX6W`
8. **AlpacaEval: An Automatic Evaluator of Instruction-following Models** (2023)  
   Zotero key: `AIFCUCJ5`
9. **Lost in the Middle: How Language Models Use Long Contexts** (2024)  
   Zotero key: `FFA4NXXD`
10. **POSIX: A Prompt Sensitivity Index For Large Language Models** (2024)  
    Zotero key: `V2NMFPXN`

---

## What these papers contribute diagnostically

### 1) Prompt framing / template artifacts
- **Prompt-order perturbation tests** (Fantastically Ordered Prompts): hold examples fixed, permute order, measure variance in output/accuracy.
- **Spurious-feature audits** (Sclar et al.): systematically vary lexical/surface features while preserving task semantics; estimate sensitivity coefficients.
- **Prompt robustness suites** (PromptBench, POSIX): standardized paraphrase/attack sets; report performance dispersion across prompt variants, not just a single score.

**Diagnostic signal:** if performance swings substantially under semantically equivalent prompts, observed inconsistency is likely **interface-induced** rather than core belief instability.

### 2) Forced-choice vs free generation interface effects
- **Calibrate Before Use** shows option-label priors and verbalizer effects in classification-style prompting; measured gains from calibration indicate substantial protocol artifact.
- **G-Eval / LLM-as-judge papers** reveal rubric form, chain-of-thought scaffolding, and structured fields can change judgments vs unconstrained outputs.

**Diagnostic signal:** compare the same underlying task in multiple response interfaces (MCQ label choice, scalar rating, pairwise choice, free generation). Divergence localizes inconsistency to **response format**.

### 3) Metric/protocol sensitivity
- **AlpacaEval**: pairwise win-rate estimates can be biased by length/style; introduces protocol choices that alter ranking stability.
- **Judging LLM-as-a-Judge** + **LLMs are not Fair Evaluators**: evaluator identity, answer order, and prompt wrapper materially alter outcomes.

**Diagnostic signal:** rank correlation / win-rate stability under protocol swaps (judge model, order randomization, rubric variants, decoding settings). Low stability implies metric artifact.

### 4) Benchmark design effects
- **Lost in the Middle**: position-dependent retrieval/use of evidence creates apparent inconsistency attributable to context layout.
- **Judge fairness papers**: positional and presentation biases in comparative setups can mimic “preference inconsistency.”

**Diagnostic signal:** randomized placement/counterbalancing of evidence/options; measure effect sizes by position and length.

---

## Concrete diagnostic protocol synthesized from the literature

Use this as a minimal battery before claiming “model inconsistency”:

1. **Template perturbation panel**  
   Evaluate each item over K semantically equivalent prompt templates/paraphrases.
2. **Order randomization**  
   Randomize few-shot exemplar order, option order, and pairwise A/B answer order.
3. **Interface triangulation**  
   Run forced-choice, pairwise, and free-generation variants of same item set.
4. **Metric triangulation**  
   Report multiple metrics (accuracy, pairwise win rate, calibration error, agreement) and their cross-metric rank correlations.
5. **Context-layout counterbalancing**  
   Randomize evidence position and distractor placement in long-context setups.
6. **Variance decomposition**  
   Attribute variance to: seed/decoding, prompt template, order/position, judge model, and item difficulty.
7. **Consistency claim threshold**  
   Only label behavior as “true inconsistency” when effects persist after controlling the above artifacts and confidence intervals remain separated.

---

## Practical takeaways for this survey
- A large fraction of reported inconsistency can be reclassified as **evaluation-design sensitivity**.
- Stronger claims require **counterbalanced, multi-interface, multi-metric** protocols.
- For generator-validator work specifically, judge-side artifacts (position/length/rubric bias) must be audited before attributing failure to generator instability.
