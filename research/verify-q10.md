# Verification of Q10 claims in `gv-gap-survey.tex`

Section checked: `\section{Q10: Origin of the GV Gap and Post-Training Effects}`

Method:
- Downloaded PDFs via `zot pdf KEY --library group`
- Converted each with `pdftotext`
- Matched each specific factual claim to paper text
- Labels: **VERIFIED** / **INCORRECT** / **UNVERIFIABLE**

---

## 1) 46BIRPAA — TruthfulQA (Lin et al., 2022)

### Claim A
> “TruthfulQA provides 817 questions …”

**Status: VERIFIED**
- Paper text: “The benchmark comprises **817 questions** …” (abstract)
- Also in body: “TruthfulQA consists of a test set of **817 questions** …”

### Claim B
> “… questions that humans often answer incorrectly due to common misconceptions …”

**Status: VERIFIED**
- Paper text: “We crafted questions that some humans would answer falsely due to a false belief or **misconception**.”

### Claim C
> “GPT-3 answers truthfully on only 58% of questions …”

**Status: VERIFIED**
- Paper text: “the best-performing model (GPT-3-175B with ‘helpful’ prompt) was truthful on **58%** of questions”

### Claim D
> “… while larger models are sometimes less truthful (imitative behavior scales).”

**Status: VERIFIED**
- Paper text: “**Larger models are less truthful**.”
- Paper text: “the largest models were generally less truthful … This ‘inverse scaling’ trend … larger models produce more imitative falsehoods …”

### Claim E
> “This directly implicates pretraining as an origin of GV gap …”

**Status: UNVERIFIABLE** (as stated)
- The paper does discuss imitation from training data and imitative falsehoods.
- But it does **not** explicitly frame this as the “origin of GV gap” (that framing is survey-level interpretation).

---

## 2) K8MWVJ89 — Language Models (Mostly) Know What They Know (Kadavath et al., 2022)

### Claim A
> “the latent truth signal is present in the pretrained model”

**Status: VERIFIED (with wording caveat)**
- Paper shows self-evaluation signal (P(True), P(IK)) tracks correctness and calibration.
- E.g., abstract: models can “evaluate the probability ‘P(True)’ that their answers are correct,” with encouraging performance/calibration.
- “Latent truth signal” is interpretation, but supported by reported self-evaluation behavior.

### Claim B
> “what shifts with post-training is which signals are surfaced in free generation vs comparative settings.”

**Status: UNVERIFIABLE**
- This causal decomposition is not directly established in this paper.
- The paper includes an RLHF calibration note, but does not make this exact broader claim.

---

## 3) MZEPR8EX — Semantic Uncertainty (Kuhn et al., 2023)

### Claim A
> “semantic entropy … better calibrated than standard token-probability-based measures.”

**Status: INCORRECT (as written)**
- The paper’s core empirical claims are about **better uncertainty prediction** (AUROC / predictive ability), and explicitly warns calibration metrics can be problematic in free-form NLG.
- It does *not* primarily claim “better calibrated” than token-probability baselines.

**Correction:**
- “Semantic entropy is more predictive of model correctness / yields better uncertainty estimation than sequence-level entropy and p(True) baselines.”

### Claim B
> “uncertainty is partly a readout problem, not only a model capability problem.”

**Status: VERIFIED**
- Strongly supported by paper framing: meaning-space clustering/readout changes uncertainty quality.

---

## 4) UFKAC9B7 — Benchmarking and Improving Generator-Validator Consistency (Li et al., 2023)

### Claim A
> “directly measures and frames the GV gap.”

**Status: VERIFIED**
- Paper defines and benchmarks GV-consistency explicitly.

### Claim B
> “show a persistent gap: models validate better than they generate.”

**Status: VERIFIED (with nuance)**
- Paper demonstrates substantial generator-validator inconsistency (e.g., GPT-4 ~76% consistency, Alpaca-30B ~60%).
- The strict comparative phrase “validate better than they generate” is directionally consistent with setup, but primary reported metric is consistency + separate generator/validator metrics.

### Claim C
> “They propose training interventions that improve consistency.”

**Status: VERIFIED**
- Consistency fine-tuning is proposed and improves consistency substantially (e.g., Alpaca-30B ~60% to ~93/94%).

---

## 5) ECXF5XFM — RankAlign (Rodriguez et al., 2025)

### Claim A
> “generator and validator produce different orderings over candidate responses …”

**Status: VERIFIED**
- Central formulation is ranking correlation mismatch between generator and validator scores over candidates.

### Claim B
> “… trains toward agreement between them.”

**Status: VERIFIED**
- RankAlign uses ranking loss to align generator/validator orderings (primarily G2V; also V2G variant).

### Claim C
> “Empirical results show reduced measured gap across multiple benchmarks.”

**Status: VERIFIED**
- Paper reports substantial average correlation gains (e.g., ~31.8% average improvement) across tasks/models and discusses generalization/OOD checks.

---

## 6) DCMM3AE4 — InstructGPT (Ouyang et al., 2022)

### Claim A
> “InstructGPT … preference tuning narrows the gap between model output and human expectations.”

**Status: VERIFIED**
- Directly supported by human preference wins (1.3B InstructGPT preferred over 175B GPT-3; 175B InstructGPT strongly preferred over 175B GPT-3).

### Claim B
> “… but introduces mode shifts (verbosity, agreeableness) that can decouple fluency from factual correctness.”

**Status: UNVERIFIABLE**
- InstructGPT reports improvements in truthfulness/toxicity and preference; this exact “verbosity/agreeableness decoupling” claim is not directly evidenced in this paper text.

---

## 7) BNDQ5TB5 — DPO (Rafailov et al., 2023)

### Claim A
> “DPO makes the same tradeoff more efficient.”

**Status: VERIFIED (broadly)**
- Paper explicitly claims DPO solves RLHF objective with simple classification loss; “stable, performant, computationally lightweight,” simpler than PPO-based RLHF.

### Claim B
> (Earlier in survey: DPO win rates around 61% vs PPO ~57% on summarization/dialogue)

**Status: VERIFIED**
- Paper reports ~61% vs ~57% in TL;DR eval at temp 0.0 (GPT-4 judged), and additional head-to-head preference results.

### Claim C
> “same tradeoff” with factual-correctness caveat

**Status: UNVERIFIABLE**
- DPO paper does not directly establish the specific fluency-vs-factuality tradeoff phrasing used in Q10.

---

## Cross-claim in Q10 paragraph not among provided keys

### Claim
> “Constitutional AI adds a second-order validator-through-critique loop …”

**Status: UNVERIFIABLE in this pass**
- No Constitutional AI paper key/PDF was included in assigned verification set, so this claim cannot be validated here.

---

## Summary of strict outcomes

- **VERIFIED:** core numeric and headline claims for TruthfulQA, Li et al. (GV-consistency), RankAlign, InstructGPT preference improvements, and DPO simplification/performance claims.
- **INCORRECT:** Semantic Uncertainty claim should not be phrased primarily as “better calibrated than token-probability measures”; paper’s main support is better **uncertainty prediction** (AUROC) via semantic readout.
- **UNVERIFIABLE:** several interpretive/causal statements in Q10 (origin framing, post-training signal-surfacing story, verbosity/agreeableness decoupling, Constitutional AI-specific statement without source in assigned set).
