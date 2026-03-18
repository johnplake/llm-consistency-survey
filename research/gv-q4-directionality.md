# GV Directionality: When to Align Generator→Validator vs Validator→Generator

## Scope
This note synthesizes evidence on **directionality choices** in generator–validator (G–V) systems:
- **Validator→Generator (V→G):** improve/learn validator first, then use it to train/select generator outputs.
- **Generator→Validator (G→V):** improve generator first (or jointly), then use stronger generations/critic loops to improve validator behavior.

Target question: under what conditions does each direction work best, and what practical policy should we follow?

## Papers added to Zotero collection
Added 10 high-relevance papers (with PDFs) to:
**LLM-inconsistency / GV-Directionality**

1. Cobbe et al. (2021) *Training Verifiers to Solve Math Word Problems*.
2. Uesato et al. (2022) *Solving Math Word Problems With Process- and Outcome-Based Feedback*.
3. Lightman et al. (2023) *Let’s Verify Step by Step*.
4. Bai et al. (2022) *Constitutional AI: Harmlessness from AI Feedback*.
5. Rafailov et al. (2023) *Direct Preference Optimization*.
6. Yuan et al. (2023) *RRHF: Rank Responses to Align Language Models with Human Feedback*.
7. Lee et al. (2023) *RLAIF: Scaling RLHF with AI Feedback*.
8. Yuan et al. (2024) *Self-Rewarding Language Models*.
9. Madaan et al. (2023) *Self-Refine*.
10. Shinn et al. (2023) *Reflexion*.

---

## Evidence by directionality

## 1) Validator-first (V→G) is strongest when:

### A. You can define a reliable local objective (especially process-level checks)
- **Cobbe et al. 2021**: trained verifiers to score candidate math solutions; best-of-N with verifier substantially outperforms pure sampling.
- **Lightman et al. 2023** and **Uesato et al. 2022**: process supervision / step-level feedback beats pure outcome reward in difficult reasoning settings.
- Interpretation: if validator signal has high precision on *intermediate reasoning quality*, improving validator first gives immediate generator gains.

### B. Search/reranking budget is available at inference
- Verifier-guided selection (best-of-N, reranking) gives monotonic gains with more candidate diversity (up to saturation), making V→G especially attractive for high-stakes reasoning.

### C. Generator outputs are noisy but diverse
- V→G can exploit diversity even when unconditional generator quality is moderate; the validator acts as a selective bottleneck.

### D. Human labels are scarce but a structured rubric exists
- Process criteria and explicit constraints allow data-efficient validator training; then reuse across many generator updates.

**Failure mode:** weakly calibrated validators produce reward hacking/specification gaming; gains may collapse out-of-domain.

---

## 2) Generator-first (G→V) is strongest when:

### A. Validator quality is bottlenecked by poor training distributions
- **Constitutional AI (Bai et al. 2022)** and **RLAIF (Lee et al. 2023)**: iterative self-critique / AI feedback loops improve both policy and supervision quality by generating better candidate/comparison data.
- If existing validator sees mostly low-quality generations, improving generator first can produce richer contrastive data that improves validator learning.

### B. Objective is preference-style and implicit (hard to hand-engineer verifier features)
- **DPO (Rafailov et al. 2023)** and **RRHF (Yuan et al. 2023)** effectively absorb preference signal directly into policy optimization, reducing dependency on separately trained high-fidelity reward models.
- In this regime, strong generator updates can be easier than building a robust standalone validator.

### C. Tasks require open-ended style/helpfulness where validator over-regularization hurts
- Generator improvements can recover fluency/helpfulness dimensions that rigid validators underweight.

### D. Joint bootstrapping is possible
- **Self-Rewarding LMs (Yuan et al. 2024)** shows iterative co-improvement (generator produces/rewrites, model-judge scores) can outperform static one-direction pipelines.

**Failure mode:** self-reinforcing bias loops (model judges its own style), reduced calibration, and hidden collapse in factual/logic reliability.

---

## 3) Asymmetric objectives & ablation signals

Several studies imply a practical asymmetry:
- **Reasoning/math:** process validator quality disproportionately determines final performance (V→G dominant early).
- **General alignment/helpfulness:** policy adaptation and data generation often dominate early returns (G→V or joint cycles).

Observed ablation pattern across these works:
1. Better candidate generation with weak validator: modest gains.
2. Better validator with same candidate pool: larger gains in constrained reasoning.
3. Best results: alternating updates, with **validator calibration checks** each cycle.

---

## Practical decision framework (literature-grounded)

Use this 5-step policy to choose directionality:

1. **Assess verifier testability**
   - If you can score intermediate steps or local constraints reliably → start **V→G**.
   - If scoring is mainly holistic preference with weak decomposition → start **G→V** or joint.

2. **Measure current bottleneck via two micro-ablations**
   - A: hold generator fixed, improve validator (or reranker).
   - B: hold validator fixed, improve generator.
   - Pick direction with larger marginal gain per unit compute.

3. **Check calibration & gaming risk**
   - If validator is miscalibrated or exploitable, do calibration/robustness work before scaling V→G.
   - If self-judging loops drift, inject external/human anchors before further G→V iterations.

4. **Match to deployment budget**
   - High inference budget (best-of-N/rerank allowed): bias toward **V→G**.
   - Tight latency budget (single-shot generation): bias toward **G→V** with lightweight critics.

5. **Adopt alternating schedule once either side plateaus**
   - Early phase: whichever side has clearer signal.
   - Mid/late phase: alternate (e.g., 1–2 validator updates per generator update in reasoning-heavy tasks; inverse in open-ended preference tasks).

### Rule-of-thumb matrix
- **Math/reasoning, safety-critical correctness, reranking allowed** → **Validator-first (V→G)**.
- **Open-ended assistant quality, sparse rubrics, preference-heavy objectives** → **Generator-first (G→V)**.
- **Long-run robust alignment** → **Alternating co-training with explicit calibration checkpoints**.

---

## Bottom line
Directionality is not one-size-fits-all. Evidence suggests:
- **V→G wins earliest** when high-quality verifiable signals exist (especially process supervision).
- **G→V wins earliest** when supervision quality is itself data-limited and preference-implicit.
- **Best sustained performance** generally comes from **asymmetric alternating loops** with calibration and anti-gaming controls.
