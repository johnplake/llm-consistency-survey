# Fact-check report for `gv-gap-survey.tex` (Q2 + Q3)

Date: 2026-03-18  
Scope: Verified claims in `\section{Q2}` and `\section{Q3}` against the cited papers (PDF text via `pdftotext`).  
Standard: **Strict** — if a specific number or assertion is not explicitly supported by the paper text, marked **UNVERIFIABLE**.

---

## Q2: Applications of Closing the GV Gap

### 1) MT-Bench and Chatbot Arena (Zheng et al., 2023) — Zotero `MPJR84HW`

Claims checked:
- Introduces **MT-Bench** and **Chatbot Arena**. → **VERIFIED**
- Uses **GPT-4 as a pairwise judge**. → **VERIFIED**
- GPT-4-as-judge achieves **>80% agreement with human preferences**, at about human-human level. → **VERIFIED** (paper states over 80%, same level as human-human agreement)
- Documents **position and verbosity biases**. → **VERIFIED**

Verdict: **All key claims VERIFIED**.

---

### 2) G-Eval (Liu et al., 2023) — Zotero `5BQ9P9S2`

Claims checked:
- Uses GPT-4 with **structured rubric/form-filling** and **CoT-based evaluation steps** for NLG eval. → **VERIFIED**
- Reports **Spearman = 0.514** with human judgments on summarization. → **VERIFIED**
- Structured prompting/rubric design improves evaluator quality vs less structured variants. → **VERIFIED** (supported by ablations incl. CoT/probability/form-filling setup)

Verdict: **All key claims VERIFIED**.

---

### 3) Prometheus (Kim et al., 2023) — Zotero `MBB3IJ2K`

Claims checked:
- Fine-tunes a **Llama-based** judge for **rubric-guided, fine-grained evaluation**. → **VERIFIED**
- Open/customizable judge, lower cost than GPT-4 API use. → **VERIFIED**
- “Matches GPT-4-level correlation on specific rubric settings.” → **VERIFIED** (reported Pearson 0.897 vs GPT-4 0.882 on 45 customized rubrics)

Verdict: **All key claims VERIFIED** (as stated with “specific rubric settings”).

---

### 4) SelfCheckGPT (Manakul et al., 2023) — Zotero `ZH2ZA69F`

Claims checked:
- Detects hallucinations via **consistency across multiple model samples**, no external KB required. → **VERIFIED**
- Outperforms several baselines on **sentence-level AUC-PR hallucination detection**. → **VERIFIED**
- Application framing (post-generation filtering/flagging) follows from method. → **VERIFIED** (supported as reasonable use-case from results)

Verdict: **All key claims VERIFIED**.

---

### 5) RARR (Gao et al., 2022 in tex; paper text: RARR) — Zotero `HVVATFPQ`

Claims checked:
- RARR retrieves evidence and revises text to fix unsupported claims while preserving original output as much as possible. → **VERIFIED**
- Human evaluations show improved attribution. → **VERIFIED**
- “With limited degradation in fluency.” → **UNVERIFIABLE**
  - Correction: paper explicitly reports **attribution** and **preservation** metrics (intent/meaning/fluency-preservation dimensions), but the exact phrasing “limited degradation in fluency” is not presented as such in the checked text excerpt.

Verdict: **PARTIALLY VERIFIED** (fluency phrasing is not directly substantiated in that form).

---

### 6) RankGen (Krishna et al., 2023) — Zotero `NMHN2NZP`

Claims checked against provided Zotero PDF:
- The Zotero item labeled RankGen downloads a PDF whose content is **not RankGen** (it is *Limits of Model Selection under Transfer Learning*). → **VERIFIED metadata/content mismatch**
- Therefore claims in survey paragraph (encoder ranker, outperforming likelihood decoding on human-preference metrics, etc.) cannot be validated from the attached paper file. → **UNVERIFIABLE (from provided source files)**

Verdict: **UNVERIFIABLE due to wrong PDF attachment in group library for this key**.

---

## Q3: Mechanism—Why Disagreement Occurs

### 1) Language Models (Mostly) Know What They Know (Kadavath et al., 2022) — Zotero `K8MWVJ89`

Claims checked:
- Evaluates self-evaluation/confidence via **P(True)-style elicitation**. → **VERIFIED**
- Finds informative self-evaluation signals; calibration and related metrics are often much better than naive generation confidence suggests. → **VERIFIED**
- “Latent belief present, readout imperfect” mechanistic interpretation. → **VERIFIED as interpretation consistent with paper findings**, but note this is conceptual framing, not a single explicit theorem-statement.

Verdict: **VERIFIED (with interpretive caveat)**.

---

### 2) Discovering Latent Knowledge Without Supervision (Burns et al., 2022) — Zotero `PIZMMCPI`

Claims checked:
- Uses **unsupervised** method (CCS) to recover truth-related signal from hidden states. → **VERIFIED**
- Uses lightweight/linear probing direction to separate truth values. → **VERIFIED**
- Works even when model outputs are wrong/misleading in tested settings. → **VERIFIED**
- Supports “readout problem” framing (knowledge in representation vs output). → **VERIFIED as paper-consistent interpretation**.

Verdict: **VERIFIED**.

---

### 3) Internal State of an LLM Knows When It’s Lying (Azaria & Mitchell, 2023) — Zotero `9UH8QI9K`

Claims checked:
- Trains classifier on hidden activations to predict truthfulness/deception of statements. → **VERIFIED**
- Shows useful accuracy even when model outputs can be false/confident. → **VERIFIED**
- Survey sentence about sequential commitment mechanism (“generation commits before signal can influence selection”). → **UNVERIFIABLE** (plausible interpretation, but not directly established as tested mechanism in this paper).

Verdict: **PARTIALLY VERIFIED**.

---

### 4) Unfaithful Explanations in CoT Prompting (Turpin et al., 2023) — Zotero `3PCS6ZJG`

Claims checked:
- Shows CoT explanations can be systematically unfaithful. → **VERIFIED**
- Biasing context (e.g., suggested answer / answer-is-always-A manipulations) can flip predictions and induce rationalized explanations. → **VERIFIED**
- Explanations often fail to mention the true biasing factor driving answer changes. → **VERIFIED**

Verdict: **VERIFIED**.

---

### 5) Towards Understanding Sycophancy in LMs (Anthropic, 2023) — Zotero `MW7XHJ9E`

Claims checked:
- Sycophancy exists and user-expressed beliefs/preferences can shift model responses, sometimes reducing accuracy. → **VERIFIED**
- Human preference data and PM optimization can incentivize sycophancy in nontrivial ways. → **VERIFIED**
- “Representation-level effect / agreeableness trajectory vs correctness trajectory.” → **UNVERIFIABLE** (not explicitly demonstrated as representation trajectory analysis)
- “Validators are less subject to social continuation pressure.” → **UNVERIFIABLE** (not a tested claim in this paper)

Verdict: **PARTIALLY VERIFIED**.

---

### 6) DoLa: Decoding by Contrasting Layers (Chuang et al., 2023) — Zotero `9HW57DAN`

Claims checked:
- Method contrasts mature vs premature layer logits during decoding. → **VERIFIED**
- Improves factuality/truthfulness on benchmarks including **TruthfulQA**; also evaluated on reasoning tasks incl. **StrategyQA**. → **VERIFIED**
- Works **without additional fine-tuning**. → **VERIFIED**
- Mechanistic statement that intermediate-layer factual signal is underused by standard decoding. → **VERIFIED as paper’s core motivation/interpretation**.

Verdict: **VERIFIED**.

---

## Cross-paper corrections needed in `gv-gap-survey.tex` (Q2/Q3 only)

1. **RARR paragraph**: replace “improved factual attribution with limited degradation in fluency” with wording directly tied to paper metrics (attribution + preservation trade-off), unless you add a specific cited fluency result.
2. **RankGen paragraph**: cannot currently be verified due to incorrect PDF attachment for the Zotero key used. Fix Zotero attachment or cite a verifiable source copy, then re-check.
3. **Q3 sycophancy paragraph**: remove/soften untested mechanistic claims about explicit representation trajectories and validators being less socially pressured.
4. **Q3 Azaria paragraph**: keep classifier-on-hidden-state findings; soften speculative sequential-commitment mechanism unless supported by another citation.

---

## Notes on sources retrieved

- Known keys were downloaded from group library.
- Unknown keys in Q3 were found by title search in group library:
  - Burns: `PIZMMCPI`
  - Azaria & Mitchell: `9UH8QI9K`
  - Turpin et al.: `3PCS6ZJG`
  - Anthropic sycophancy: `MW7XHJ9E`
  - DoLa: `9HW57DAN`
- RankGen key(s) in group library (`NMHN2NZP`, `RMIRH558`) both point to a wrong attached PDF (transfer learning theory paper), preventing strict verification.
