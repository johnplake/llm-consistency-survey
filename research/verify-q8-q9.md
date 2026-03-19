# Verification of Q8 and Q9 claims in `gv-gap-survey.tex`

Date: 2026-03-18
Verifier: subagent `verify-q8-q9`
Method: downloaded each paper PDF via `zot pdf KEY --library group`, converted with `pdftotext`, and checked each specific claim in Q8/Q9 paragraphs against paper text.  
Rule applied: numeric claims marked VERIFIED only when the number appears in the paper text.

---

## Q8: Inference-Time Compute

### FA2MV8GU — Self-Consistency (Wang et al., 2022)

1. **Claim:** “Generate diverse reasoning chains via temperature sampling, then take a majority vote over final answers.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** paper describes replacing greedy decode with sampling multiple reasoning paths and “taking a majority vote over final answers.”

2. **Claim:** “Headline gains: approximately +18 percentage points on GSM8K and consistent improvements across SVAMP, AQuA, StrategyQA, and ARC-type benchmarks versus greedy CoT decoding.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** abstract/introduction report: GSM8K **+17.9%**, SVAMP **+11.0%**, AQuA **+12.2%**, StrategyQA **+6.4%**, ARC-challenge **+3.9%** vs CoT/greedy setup.

3. **Claim:** “Mechanism: when generator errors are random/diverse, majority voting exploits better-than-chance validation capacity implicitly.”  
   **Verdict:** **UNVERIFIABLE**  
   **Reason:** this is interpretive mechanism language; paper motivates diversity/consistency, but does not explicitly phrase this as “better-than-chance validation capacity.”

---

### P4CSZPVW — Tree of Thoughts (Yao et al., 2023)

1. **Claim:** “ToT frames reasoning as a search problem; the model generates, evaluates, and selects intermediate thought states via a tree structure.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** paper explicitly defines tree of thoughts with thought generation, state evaluation, and BFS/DFS tree search.

2. **Claim:** “On Game of 24, performance jumps from near-zero with standard prompting to much higher success rates (near order-of-magnitude relative gain).”  
   **Verdict:** **VERIFIED**  
   **Evidence:** abstract states GPT-4 CoT solves **4%** of Game of 24, ToT reaches **74%**.

3. **Claim:** “Externalizing validation at intermediate steps via search prevents commitment to early wrong branches.”  
   **Verdict:** **UNVERIFIABLE**  
   **Reason:** consistent with method motivation, but “prevents commitment” is interpretive wording rather than a directly measured statement.

---

### PN3PMAWR — LATS (Zhou et al., 2023)

1. **Claim:** “LATS applies MCTS-style search to agent trajectories, combining generation, evaluation, and backtracking.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** paper explicitly presents LATS as an MCTS-based framework with selection/expansion/evaluation/simulation/backpropagation for LM agents.

2. **Claim:** “Improvements on programming and WebArena-style tasks demonstrate superiority over linear chains.”  
   **Verdict:** **INCORRECT**  
   **Correction:** The paper reports gains on **programming (HumanEval)** and **WebShop** web navigation (plus HotPotQA/math), not WebArena.  
   **Evidence:** abstract and experiments mention HumanEval and WebShop; no WebArena benchmark in paper text.

3. **Claim:** “Allocating more inference compute to validator-guided exploration narrows the GV gap.”  
   **Verdict:** **UNVERIFIABLE**  
   **Reason:** high-level interpretation; paper shows performance gains from search/inference-time compute, but does not explicitly quantify a “GV gap” metric.

---

### 7ZFEBG78 — Multiagent Debate (Du et al., 2023)

1. **Claim:** “Multiple independent LLM agents propose and critique each other’s answers across rounds, then aggregate.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** method section describes multiple agents generating initial answers, debating across rounds, and using final aggregated/quorum outcome.

2. **Claim:** “Improved factuality and reasoning quality compared to single-agent generation on math and factual QA tasks.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** paper reports gains over single-model baselines on reasoning tasks (arithmetic/GSM8K/chess) and factual tasks (Biographies/MMLU).

3. **Claim:** “Repeated exposure to alternative critiques forces convergence toward more consistent outputs.”  
   **Verdict:** **UNVERIFIABLE**  
   **Reason:** consistent with qualitative framing, but wording (“forces convergence”) is interpretive and not directly quantified as stated.

---

### ICKQRMSG — Large Language Monkeys (Brown et al., 2024)

1. **Claim:** “Scaling laws for repeated sampling: more samples predictably improve success rates.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** paper repeatedly reports increasing pass@k/coverage with more samples across tasks.

2. **Claim:** “Power-law relationship between sample count and performance.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** paper states coverage vs sample budget is often modeled by an **exponentiated power law** and shows corresponding fits.

3. **Claim:** “Supports a compute–quality frontier where mismatch can be bought down by inference compute up to validator limits.”  
   **Verdict:** **UNVERIFIABLE**  
   **Reason:** first half (compute improves coverage) is supported; “mismatch” and “validator limits” wording is interpretive synthesis rather than explicit paper claim.

---

## Q9: Judge Reliability

### CKB5PSDP — Large Language Models are not Fair Evaluators (Wang et al., 2024)

1. **Claim:** “Pairwise LLM judge outcomes change substantially depending on which answer appears first (position bias).”  
   **Verdict:** **VERIFIED**  
   **Evidence:** core finding: swapping order changes outcomes; GPT-4 tends to prefer first position, ChatGPT often second.

2. **Claim:** “Model scoring differs across social and stylistic correlates.”  
   **Verdict:** **UNVERIFIABLE**  
   **Reason:** this paper focuses on positional bias and calibration; no clear direct evidence in text for “social and stylistic correlates.”

3. **Claim:** “Position randomization and bidirectional scoring are necessary minimum controls.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** proposed debiasing includes evaluating both orders and combining signals; paper advocates swap-based calibration.

---

### IPU4JPDM — Judging the Judges (Shi et al., 2024)

1. **Claim:** “Systematically maps position bias across judge models and protocols.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** large empirical study over 15 judges, tasks, and pairwise/list-wise settings with dedicated position-bias metrics.

---

### W56W4SBT — Split and Merge (Li et al., 2024)

1. **Claim:** “Split and Merge proposes splitting evaluation in two (A vs B; B vs A) and merging scores to cancel positional effects.”  
   **Verdict:** **INCORRECT**  
   **Correction:** This paper’s Split-and-Merge (PORTIA) splits **responses into aligned segments** and merges aligned content for fairer pairwise evaluation; it is **not** the simple bidirectional A/B + B/A averaging protocol.  
   **Evidence:** method section describes segment splitting/alignment/merged prompts.

2. **Claim:** “Shows reduced bias without eliminating judge utility.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** experiments report substantial reduction in position bias while maintaining/improving evaluation performance.

---

### CGMZFEFC — CalibraEval (Li et al., 2024)

1. **Claim:** “Addresses calibration of predicted preference/win probabilities under judge bias.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** paper formulates debiasing/calibration as mapping observed token/probability distributions to unbiased distributions.

2. **Claim:** “LLM judges are miscalibrated; confidence/distribution does not match empirical outcomes.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** motivation and experiments show selection bias (position/token) distorts judge probabilities; calibration improves consistency/performance.

---

### TPEWHVIS — AlpacaEval (Dubois et al., 2024, “A Simple Way to Debias Automatic Evaluators”)

1. **Claim:** “Addresses calibration of predicted win probabilities.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** paper models pairwise preference probabilities with a GLM and computes length-controlled win rates.

2. **Claim:** “Introduces length-controlled debiasing.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** central contribution is length-controlled AlpacaEval to reduce length bias/gameability.

3. **Claim:** “General confidence miscalibration claim (stated confidence vs empirical accuracy).”  
   **Verdict:** **UNVERIFIABLE**  
   **Reason:** this paper is about bias/debiasing (especially length), not primarily a generic confidence-calibration study of judge probabilities.

---

### 5P9M3TJH — Replacing Judges with Juries (Chan et al., 2024)

1. **Claim:** “Uses a panel of diverse models instead of a single judge.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** core proposal is PoLL/panel-of-LLMs judging.

2. **Claim:** “Improves rank stability and lowers sensitivity to individual judge bias.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** paper reports reduced intra-model bias and improved alignment/correlation of rankings vs ground truth.

3. **Claim:** “Practical implication: multi-judge ensembles with disagreement reporting are more reliable than single judges.”  
   **Verdict:** **UNVERIFIABLE**  
   **Reason:** reliability improvement is supported; explicit “disagreement reporting” as a required practice is not a direct tested claim.

---

### MBB3IJ2K — Prometheus (Kim et al., 2023)

1. **Claim:** “Fine-tuned rubric-following judge can reach GPT-4-level human correlation on specific domains and be open/customizable.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** paper reports Pearson correlation with human ratings **0.897** (Prometheus) vs **0.882** (GPT-4) on 45 customized rubrics, with open-source release.

2. **Claim:** “Reduces dependence on proprietary general-purpose judges.”  
   **Verdict:** **VERIFIED**  
   **Evidence:** explicit motivation and results emphasize open-source evaluator as lower-cost alternative to GPT-4.

---

## Summary of corrections needed in `gv-gap-survey.tex`

1. **Q8 / LATS paragraph:** replace “WebArena-style tasks” with **WebShop (web navigation)** (and optionally HotPotQA).  
2. **Q9 / Fair Evaluators paragraph:** remove or re-source claim about “social and stylistic correlates” (not established in this cited paper).  
3. **Q9 / Split and Merge paragraph:** revise method description; current text confuses PORTIA with simple A/B + B/A bidirectional averaging.

Everything else in Q8/Q9 is either directly supported or interpretive-but-plausible (marked UNVERIFIABLE where wording exceeds explicit evidence).
