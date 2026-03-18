# GV Q1 Detailed Dossier — Generator Improvement via Validator/Judge Signals

Collection: `LLM-inconsistency / GV-Generator-improvement-using-validator` (`4AZ47QHF`)

Method note: numbers below are only included when directly verified from the paper text available in this pass; otherwise marked **not verified**.

---

## 1) Training Verifiers to Solve Math Word Problems (Cobbe et al., 2021)  
**Zotero key:** `Z4S8N89S`

### Core contribution
- Introduces **GSM8K** and a generator+verifier recipe: generate many solutions, train a verifier to score correctness, then select the top-scoring candidate.
- Argues verification scales better than pure generator finetuning for math reasoning.

### Problem setup and objective
- Task: solve grade-school math word problems with multi-step reasoning.
- Objective: improve final solve rate by adding a learned verifier over sampled solutions.

### Data/tasks/benchmarks used
- **GSM8K** dataset, reported size **8.5K** problems.
- Also discusses relation to harder **MATH** benchmark (contextual comparison).

### Model/training setup (as available)
- Baseline: finetuned generator LM.
- Verifier: trained to classify/rank candidate solutions for correctness.
- Inference: best-of-N style sampling + verifier reranking.

### Key empirical findings (verified numbers)
- Paper states verifier-based selection significantly improves GSM8K performance.
- Text explicitly claims verifier gain is comparable to roughly a **30× model-size increase** (exact table context not fully re-verified here).
- Specific full table values and exact N-by-N scaling curves: **not verified** in this pass.

### Why it matters for improving generator using validator
- Canonical demonstration that a validator can improve generator outputs without changing base decoding objective.
- Establishes a practical path: sample diversity + validator filtering.

### Limits/caveats
- Heavy dependence on candidate sampling budget.
- Domain focus is math reasoning; transfer beyond math is not guaranteed.
- Some exact numeric claims need re-check against tables.

### Follow-up questions
- How does verifier quality trade off against candidate count at fixed compute?
- Can process-level verification outperform outcome-only verification on GSM8K with equal labels?
- How robust is verifier ranking under distribution shift (non-GSM8K math)?

---

## 2) Solving Math Word Problems With Process- and Outcome-Based Feedback (Uesato et al., 2022)  
**Zotero key:** `T9WTR9N3`

### Core contribution
- First broad comparison of **process-based** vs **outcome-based** feedback on natural-language reasoning (GSM8K), including SFT, reranking, and RL variants.

### Problem setup and objective
- Train models that produce reasoning traces and final answers.
- Evaluate both final-answer correctness and trace correctness.

### Data/tasks/benchmarks used
- Primary: **GSM8K**.
- Additional generalization checks include **MATH** (as stated in paper).

### Model/training setup (as available)
- Large pretrained LM backbone (paper states Chinchilla-family base; exact size in this pass: **not verified**).
- Methods include supervised training, reward modeling (ORM/PRM), and expert-iteration-style RL.

### Key empirical findings (verified numbers)
- Improves prior SOTA: final-answer error **16.8% → 12.7%** and trace error among final-answer-correct solutions **14.0% → 3.4%**.
- With abstention on 30% of questions, final-answer error reported at **2.7%**.
- Outcome vs process final-answer error: **23.5% vs 22.3%** (without reward models), **16.6% vs 14.8%** (with reward models).
- Best process-oriented methods reduce trace error markedly (paper text cites **3.8%** best process vs **12.4%** final-answer-RL style baseline; context verified in abstract/body summary).

### Why it matters for improving generator using validator
- Shows validator design matters: process-aware validators improve not just final outcomes but reasoning quality.
- Supports using learned validators as selection and RL signals to shape generators.

### Limits/caveats
- Heavy annotation requirements for process labels.
- Results may be dataset-specific (math tasks with checkable answers).

### Follow-up questions
- What is the best low-label proxy for process supervision?
- Can step-level validator confidence calibrate when to abstain?
- How does trace quality correlate with out-of-domain robustness?

---

## 3) Let’s Verify Step by Step (Lightman et al., 2023)  
**Zotero key:** `B496R7FJ`

### Core contribution
- Strong process-supervised reward modeling results for mathematical reasoning.
- Releases **PRM800K** (800k step-level human labels).

### Problem setup and objective
- Compare outcome-supervised RMs (ORMs) vs process-supervised RMs (PRMs).
- Goal: improve reliable reasoning on MATH via verifier-guided selection.

### Data/tasks/benchmarks used
- Main benchmark: **MATH**.
- Training includes large-scale step-level annotation set PRM800K.

### Model/training setup (as available)
- Generator samples candidate solutions.
- Reward model scores steps/solutions; best-of-N selection used.
- Active-learning-based data collection for process labels.

### Key empirical findings (verified numbers)
- Process-supervised model solves about **78%** of a representative MATH test subset (also quoted as **78.2%** in body).
- Active learning gives **2.6×** data efficiency gain for process supervision.
- PRM800K size: **800,000** step-level labels.

### Why it matters for improving generator using validator
- Strong evidence that a high-quality step-level validator materially improves chosen generations.
- Provides practical data strategy (active learning) to make validator training more efficient.

### Limits/caveats
- Evaluation subseting and best-of-N protocols can make headline numbers sensitive to setup.
- High annotation cost and domain concentration in math.

### Follow-up questions
- Can synthetic step labels replace part of PRM800K without quality loss?
- How does PRM performance degrade with fewer candidate samples?
- Is there a portable process-verifier architecture for non-math domains?

---

## 4) Constitutional AI: Harmlessness from AI Feedback (Bai et al., 2022)  
**Zotero key:** `BAZNUAS3`

### Core contribution
- Introduces Constitutional AI pipeline: self-critique/revision SFT + RL from AI feedback (RLAIF), replacing large amounts of direct human preference labels with principle-guided AI feedback.

### Problem setup and objective
- Improve harmlessness while preserving helpfulness and reducing evasiveness.
- Objective: train assistant behavior via validator-like critique and AI preference signals.

### Data/tasks/benchmarks used
- Red-teaming prompts and helpful/harmless conversational evaluations.
- Elo-style pairwise evaluations by crowdworkers/model judges are discussed.

### Model/training setup (as available)
- Two stages:
  1. Supervised stage with self-critiques and revisions under a “constitution”.
  2. RL stage with preference model trained on AI-generated comparisons.
- Includes CoT-style reasoning for critique/eval variants.

### Key empirical findings (verified numbers)
- Paper reports strong harmlessness gains and better harmlessness/helpfulness trade-off vs RLHF baselines.
- States use of roughly order-**10²** simple principles (exact count and all eval deltas in this pass: **not verified**).
- Mentions preference-model binary accuracy can exceed **90%** in some settings (exact table value: **not verified**).

### Why it matters for improving generator using validator
- Validator/critic signals (AI-generated) can be integrated at both data-generation and RL optimization phases.
- Demonstrates scalable “generator improved by judge” loop with reduced human labeling burden.

### Limits/caveats
- Domain is safety/helpfulness alignment, not factual correctness per se.
- Outcome quality depends on constitution quality and critique faithfulness.
- Several key quantitative improvements require table-by-table verification.

### Follow-up questions
- Which constitutional principles contribute most to actual behavior change?
- How well does AI-feedback RL transfer across domains/tasks?
- Can faithfulness validators detect superficial harmlessness vs genuine refusal quality?

---

## 5) ReST: Reinforced Self-Training for Language Modeling (Gulcehre et al., 2023)  
**Zotero key:** `RBSMC5WC`

### Core contribution
- Proposes **ReST**: an offline, growing-batch RLHF alternative with alternating **Grow** (sample data) and **Improve** (filter + offline policy update) loops.

### Problem setup and objective
- Improve generation quality/alignment while reducing online RL costs and instability.
- Instantiated mainly for machine translation.

### Data/tasks/benchmarks used
- MT benchmarks including **IWSLT14 De-En** and **Web Domain En-Zh** (as cited in results text).

### Model/training setup (as available)
- Start from supervised policy.
- Generate multiple outputs per context.
- Rank/filter outputs with reward model.
- Update policy with offline RL objective; iterate G/I loops.

### Key empirical findings (verified numbers)
- Reported improvement of about **+5.3** points on IWSLT14 De-En and **+0.8** on Web Domain En-Zh (metric context in paper section).
- Human evaluations reported to prefer ReST variants over supervised baselines (exact preference percentages: **not verified**).

### Why it matters for improving generator using validator
- Directly operationalizes validator-guided data curation for iterative generator improvement.
- Highlights compute/sample efficiency advantages over fully online PPO loops.

### Limits/caveats
- Translation-centric evidence; general instruction-following gains not primary evidence here.
- Reward-model misspecification still a risk.

### Follow-up questions
- How does ReST compare to DPO-like methods under equal preference data budgets?
- Can validator uncertainty be used for adaptive filtering thresholds?
- Does iterative offline reuse induce mode collapse in open-ended generation?

---

## 6) RRHF: Rank Responses to Align Language Models with Human Feedback (Yuan et al., 2023)  
**Zotero key:** `E3WMSCXK`

### Core contribution
- Replaces PPO-style policy optimization with a ranking-based objective over sampled responses; simpler pipeline with 1–2 models.

### Problem setup and objective
- Align LMs with preferences using ranked responses from mixed sources (self, other LMs, human outputs).
- Emphasis on robustness and reduced hyperparameter complexity.

### Data/tasks/benchmarks used
- Helpful-Harmless (HH) style alignment benchmarks and human evaluation setups.

### Model/training setup (as available)
- Sample multiple responses; assign expert/ranking signals.
- Optimize log-prob-based ranking loss (with pairwise ranking component).
- Sampling policy quality is central to outcomes.

### Key empirical findings (verified numbers)
- Reports comparable alignment quality to PPO on reward/human evaluations (headline claim).
- Reward-model accuracy examples in text include **68.49%** (gptj-rm-static) and RRHF-style model around **61.75%** in one setup.
- Some variants show negative/low scores when sampling quality is weak (table-specific details partly visible; full matrix **not verified**).

### Why it matters for improving generator using validator
- Validator signal is represented as ranking constraints over candidates, directly training generator toward judge-preferred responses.
- Simpler than PPO while preserving “judge improves generator” effect.

### Limits/caveats
- Highly sensitive to candidate sampling diversity/quality.
- Evaluation reporting in paper mixes metrics; direct apples-to-apples may require careful reconstruction.

### Follow-up questions
- What is optimal sampling policy for RRHF under fixed compute?
- Can dynamic candidate generation reduce “best-of-n learner” dependence?
- How stable is RRHF under noisy synthetic judge labels?

---

## 7) Direct Preference Optimization (Rafailov et al., 2023)  
**Zotero key:** `4DCF8NWX`

### Core contribution
- Derives a direct objective (DPO) that optimizes preference alignment without explicit RL rollouts or separate reward-model training loop.

### Problem setup and objective
- Use pairwise preferences to directly optimize policy relative to a reference model.
- Reduce RLHF complexity while preserving alignment quality.

### Data/tasks/benchmarks used
- Summarization (e.g., TL;DR/CNN-DM contexts in paper) and dialogue preference evaluation.
- Uses GPT-4/human win-rate style evaluations.

### Model/training setup (as available)
- Binary classification-style objective from preference pairs.
- No PPO inner loop; no online sampling needed during optimization.

### Key empirical findings (verified numbers)
- In one cited setup, DPO achieves roughly **61%** win rate at temperature 0.0 vs PPO around **57%** at its best temperature.
- Paper text notes DPO preferred over PPO around **58%** in direct sample comparison (specific experiment context).

### Why it matters for improving generator using validator
- If validator/judge can produce pairwise preferences, DPO provides a direct path from judge signals to generator updates.
- Important bridge between inference-time judging and train-time policy improvement.

### Limits/caveats
- Quality bounded by preference data quality and judge reliability.
- Some reported win-rate advantages may vary with prompt/eval protocol.

### Follow-up questions
- How does DPO perform with fully AI-generated preference labels vs human labels?
- Can uncertainty-aware DPO reduce overfitting to noisy validators?
- What are failure modes under distribution shift?

---

## 8) Self-Refine: Iterative Refinement with Self-Feedback (Madaan et al., 2023)  
**Zotero key:** `7ZFU4ZJ3`

### Core contribution
- Inference-time iterative loop where the same LLM generates output, critiques itself, and refines repeatedly.

### Problem setup and objective
- Improve output quality without additional training or human labeling.
- Works across diverse tasks by prompt-structured feedback.

### Data/tasks/benchmarks used
- 7 tasks including dialog, constrained generation, code optimization, and math reasoning.
- Evaluated with human preference and task-specific automatic metrics.

### Model/training setup (as available)
- Single LLM reused in three roles: generator, feedback provider, refiner.
- Iterative termination by fixed steps or stop condition.

### Key empirical findings (verified numbers)
- Reports about **~20% absolute average** improvement across tasks vs one-shot generation.
- Reported gains span roughly **5–40%** depending on task/model.
- GPT-4 code optimization example: **27.3% → 36.0%** (+8.7 absolute).

### Why it matters for improving generator using validator
- Clear example of validator-like signal (self-feedback) improving generation at inference time.
- No retraining requirement makes it practical as a drop-in quality layer.

### Limits/caveats
- Self-feedback can be wrong/redundant; gains may plateau with more iterations.
- Depends on prompt quality and task structure.

### Follow-up questions
- When is external validator better than self-validator?
- Can confidence-based stopping reduce unnecessary refinement loops?
- How do gains compare to best-of-N reranking at equal token budget?

---

## 9) Self-Rewarding Language Models (Yuan et al., 2024/2025 versioned)  
**Zotero key:** `9XE5V7E2`

### Core contribution
- Unifies generator and judge: model provides its own reward labels via LLM-as-a-Judge prompting during iterative DPO training.

### Problem setup and objective
- Improve instruction-following and reward-judging ability jointly over iterations.
- Remove bottleneck of fixed frozen external reward model.

### Data/tasks/benchmarks used
- Instruction-following evaluations including pairwise win-rate setups and AlpacaEval-style leaderboard reporting.
- Additional benchmarks include MT-Bench and academic tasks (mentioned in paper).

### Model/training setup (as available)
- Base: **Llama 2 70B** fine-tuned iteratively (M1→M2→M3 style).
- Pipeline: generate responses, judge pairwise, select preferences, run DPO, repeat.

### Key empirical findings (verified numbers)
- Head-to-head examples in text:
  - M2 vs M1: **55.5%** vs **11.7%** wins.
  - M3 vs M2: **47.7%** vs **12.5%** wins.
  - M3 vs SFT baseline: **62.5%** vs **9.8%** wins.
- AlpacaEval-over-GPT4-Turbo win rates reported to improve across iterations: **9.94% → 15.38% → 20.44%**.

### Why it matters for improving generator using validator
- Directly instantiates “improving generator using validator” where validator is endogenous and iteratively improved.
- Suggests a scalable closed loop for continual enhancement.

### Limits/caveats
- Risk of self-reinforcing biases if judge quality drifts.
- Strong dependence on prompting and evaluation protocol for judge behavior.

### Follow-up questions
- How to calibrate/anchor self-judging against external human references?
- Does iterative self-rewarding converge or drift over many more rounds?
- Can hybrid human+AI judge mixing improve stability?

---

## 10) LLM-Blender: Ensembling LLMs with PairRank and GenFuser (Jiang et al., 2023)  
**Zotero key:** `5SMQUPA3`

### Core contribution
- Ensembling framework with:
  - **PairRank**: pairwise ranker over candidate outputs.
  - **GenFuser**: fuses top-ranked candidates into improved final response.
- Introduces **MixInstruct** benchmark for large-scale comparison.

### Problem setup and objective
- Different LLMs are best on different examples; objective is per-example model/candidate selection and fusion.

### Data/tasks/benchmarks used
- MixInstruct (mixture of instruction datasets with oracle pairwise comparisons).
- Evaluations include GPT-based ranking and reference-based metrics.

### Model/training setup (as available)
- Generate N candidates from multiple open-source LLMs.
- Use pairwise cross-attention ranker for comparisons.
- Infer ranking matrix; select top-K; fuse via generator.

### Key empirical findings (verified numbers)
- In motivating distribution chart, best single model ranks first only **21.22%** of examples (others also frequently top-ranked), supporting per-example routing.
- Top-3 presence figures in text include **68.59%** (one model) vs **52.88%** (another baseline context).
- PairRank-selected output average GPT-rank **3.20**, reported as **+0.70** (~**18% relative**) better than best individual model in cited section.

### Why it matters for improving generator using validator
- Uses learned ranker (validator) to select/fuse candidates, improving generation quality without retraining source LLMs.
- Strong inference-time architecture for validator-guided generation.

### Limits/caveats
- Requires multiple base models and candidate generation cost.
- Quality sensitive to pairwise ranker calibration and pair coverage.

### Follow-up questions
- Can a lighter validator approximate PairRank with lower latency?
- How does GenFuser behave when top candidates are mutually inconsistent?
- What is the best compute allocation between more candidates vs better ranker?
