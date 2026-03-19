# Verification of `gv-gap-survey.tex` (Q6 + Q7)

Date: 2026-03-18
Verifier: subagent `verify-q6-q7`
Method: downloaded PDFs via `zot pdf`, extracted with `pdftotext`, checked each concrete claim in Q6/Q7 text.  
Strict rule used: specific numeric claims are only **VERIFIED** if the number appears in the paper text.

---

## Q6: Evaluation Design—Artifact vs True Inconsistency

### 1) Fantastically Ordered Prompts (Lu et al., 2022) — key `FHME8CQ7`

Claims in report paragraph:

1. **"few-shot exemplar order dramatically changes LLM accuracy on classification tasks"**  
   **VERIFIED.** Paper explicitly shows strong order sensitivity in few-shot classification.

2. **"variance across orderings sometimes exceeding 30 percentage points"**  
   **VERIFIED (indirect but numerically supported).** Paper text states some permutations are "over 85%" while others are "around 50%" (difference ~35 points).

3. **"observed model capability is partly a function of prompt construction"**  
   **VERIFIED.** This is the paper’s central conclusion.

4. **"for GV gap studies, measured inconsistency can reflect order sensitivity rather than deep generation–validation disagreement"**  
   **UNVERIFIABLE (as stated).** This is a logical extrapolation to GV studies, not directly tested in this paper.

---

### 2) PromptBench (Zhu et al., 2023) — key `FHH789NP`

Claims in report paragraph:

1. **"systematically evaluates LLM robustness to adversarial prompt perturbations"**  
   **VERIFIED.** Paper introduces benchmark (named PromptRobust in extracted text) with systematic attacks.

2. **"(misspellings, paraphrases, character insertions)"**  
   **VERIFIED (category-level).** Paper includes character-, word-, sentence-, and semantic-level perturbations; examples include typos/synonyms.

3. **"small surface-level perturbations can drop performance substantially"**  
   **VERIFIED.** Paper reports substantial drops (e.g., word-level attacks: **39% average performance drop**).

4. **"consistency studies must control prompt surface form before attributing variance to GV mismatch"**  
   **UNVERIFIABLE (as stated).** Reasonable methodological implication, but not a directly tested GV-specific claim in this paper.

---

### 3) POSIX (Sclar et al., 2024) — key `V2NMFPXN`

Claims in report paragraph:

1. **"defines a Prompt Sensitivity Index"**  
   **VERIFIED.** Exactly the paper’s contribution.

2. **"quantifies sensitivity to semantically equivalent/intention-preserving prompt variants"**  
   **VERIFIED.** Paper repeatedly frames variants as intent-preserving and defines index accordingly.

3. **"calibrated, task-agnostic measurement of protocol-induced variance"**  
   **PARTIALLY VERIFIED.**
   - "measurement of prompt sensitivity across settings" is supported.  
   - "calibrated" and "task-agnostic" wording is stronger than what is explicitly proven; paper evaluates multiple tasks including MCQ and open-ended generation, but does not formally prove full task-agnosticity.

4. **"directly enables separation of artifact from true inconsistency"**  
   **UNVERIFIABLE (as stated).** POSIX measures prompt sensitivity; direct decomposition into artifact vs "true inconsistency" is not directly demonstrated in this paper.

---

### 4) Lost in the Middle (Liu et al., 2023) — key `FFA4NXXD`

Claims in report paragraph:

1. **"LLMs use information at start and end more than middle"**  
   **VERIFIED.** Paper reports U-shaped performance with primacy/recency biases.

2. **"introducing positional artifacts in long-context evaluations"**  
   **VERIFIED.** Position of relevant information strongly affects performance.

3. **"validator behavior may change based on where candidates appear, independently of quality"**  
   **PARTIALLY VERIFIED.** Position effects are clearly shown; explicit validator-candidate framing is an extrapolation.

---

## Q7: Training Targets

### A) Introductory Q7 paragraph (before per-paper subparagraphs)

This paragraph cites multiple works not in the provided Q7 verification set (e.g., DPO, RRHF, RLAIF, Uesato, Lightman). With only the requested papers checked here, most broad synthesis claims are **UNVERIFIABLE within this pass**.

Specific status:

1. **"pairwise ranking objectives ... have three documented failure modes: underspecification, credit assignment collapse, reward hacking"**  
   **UNVERIFIABLE in checked papers.** Not directly established as a three-mode taxonomy in Christiano/InstructGPT/Math-Shepherd texts.

2. **"Outcome supervision ... remains coarse"**  
   **PARTIALLY VERIFIED** by Math-Shepherd framing (PRM vs ORM), but not as a universal claim.

3. **"Process supervision ... consistently superior for hard reasoning tasks"**  
   **PARTIALLY VERIFIED** by Math-Shepherd results on GSM8K/MATH; "consistently" across literature not established by this limited set.

4. **"Hybrid objectives (Constitutional AI, Self-Rewarding LMs) ..."**  
   **UNVERIFIABLE in checked papers.** Not covered by the three Q7 papers.

5. **"Practical recommendation: progressive hybridization ..."**  
   **UNVERIFIABLE (recommendation, not a direct empirical claim in these papers).

---

### B) Deep RL from Human Preferences (Christiano et al., 2017) — key `7NV84BF5`

Claims in report paragraph:

1. **"human preferences over short trajectory clips can train reward models that drive RL improvement without task-specific reward engineering"**  
   **VERIFIED.** Core method and result.

2. **"roughly 1,300 human comparisons suffice to teach a simulated locomotion policy comparable to a hand-crafted reward"**  
   **INCORRECT.**
   - The extracted text links **~1,300 queries** to **Enduro (Atari)** demo behavior, not locomotion.
   - For MuJoCo locomotion experiments, the paper discusses setups like 700 human queries and 350/700/1400 synthetic comparisons, with comparability trends to true-reward RL, but not this exact "1,300 locomotion" statement.
   **Correction:** "~1,300 queries" corresponds to Enduro example, not simulated locomotion benchmark claim.

3. **"establishes validator-as-reward-model paradigm inherited by RLHF"**  
   **VERIFIED.** Historically and methodologically accurate given paper framing.

---

### C) InstructGPT (Ouyang et al., 2022) — key `6CXT6JS5`

Claims in report paragraph:

1. **"applies RLHF pipeline at scale to instruction following"**  
   **VERIFIED.** Explicit three-step SFT → RM → PPO pipeline.

2. **"1.3B RLHF-tuned model preferred over 175B base GPT-3 on most instructions"**  
   **VERIFIED (wording tweak).** Paper explicitly says outputs from 1.3B InstructGPT are preferred to outputs from 175B GPT-3 on their prompt distribution. "Most instructions" should be read as "majority preference on evaluated prompts."

3. **"preference-based validation signal can compensate for model scale"**  
   **VERIFIED.** Supported by 1.3B vs 175B preference result.

---

### D) Math-Shepherd (Wang et al., 2023) — key `XZM4TK2Q`

Claims in report paragraph:

1. **"trains step-level verifiers using automatically generated process labels (without full human annotation)"**  
   **VERIFIED.** Central contribution.

2. **"labels generated by decoding from intermediate steps and checking which prefixes lead to correct final answers"**  
   **VERIFIED.** Paper defines step quality by potential to reach correct final answer via multiple completions from each step.

3. **"automatic step labels outperform outcome-only supervision on math benchmarks"**  
   **VERIFIED (task-scoped).** Paper reports PRM outperforming ORM on key settings (notably stronger on MATH; also gains with step-by-step PPO).

4. **"process-aware training accessible at lower cost"**  
   **PARTIALLY VERIFIED.** Paper’s motivation and method reduce human annotation burden; full cost-efficiency quantification is nuanced (completion introduces compute cost).

---

## Summary of corrections needed in `gv-gap-survey.tex`

1. **Q7 Christiano paragraph has a concrete numeric mismatch.**  
   Replace the "~1,300 comparisons for simulated locomotion" claim with a paper-faithful statement (e.g., 1,300 tied to Enduro example, not locomotion).

2. **Several Q6/Q7 lines are high-level methodological extrapolations.**  
   Keep if desired, but they should be framed as implications/hypotheses, not direct empirical findings from the cited paper.

3. **PromptBench naming note.**  
   The extracted PDF text repeatedly says "PromptRobust" benchmark despite title "PromptBench"; worth checking final citation wording for consistency.
