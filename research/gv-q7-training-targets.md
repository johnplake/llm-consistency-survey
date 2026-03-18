# GV-Q7: Training targets — pairwise ranking vs outcome supervision vs process supervision/verifier traces

Date: 2026-03-18
Collection: `LLM-inconsistency / GV-Training-targets` (`JHTSZAAA`)

## Scope
This note compares training-target families for generator/validator systems:
- **Pairwise ranking / preference objectives** (RLHF, DPO, RRHF, RLAIF)
- **Outcome supervision** (final-answer correctness / trajectory-level reward)
- **Process supervision / verifier traces** (step-level labels/rewards)
- **Hybrid objectives** (combinations of process + outcome, or iterative self-reward)

## Papers added to Zotero subcollection (11)
All 11 were added to `LLM-inconsistency / GV-Training-targets` with PDFs attached.

1. Christiano et al. (2017), *Deep Reinforcement Learning from Human Preferences* [`7NV84BF5`]
2. Ouyang et al. (2022), *Training language models to follow instructions with human feedback* [`6CXT6JS5`]
3. Bai et al. (2022), *Constitutional AI: Harmlessness from AI Feedback* [`P2DNKJVT`]
4. Lee et al. (2023), *RLAIF: Scaling Reinforcement Learning from Human Feedback with AI Feedback* [`T4WKR2PP`]
5. Rafailov et al. (2023), *Direct Preference Optimization* [`6QF6EH9W`]
6. Yuan et al. (2023), *RRHF: Rank Responses to Align Language Models with Human Feedback* [`PRNCMIKU`]
7. Cobbe et al. (2021), *Training Verifiers to Solve Math Word Problems* [`SRA64W3C`]
8. Uesato et al. (2022), *Solving Math Word Problems With Process- and Outcome-Based Feedback* [`TF5S674H`]
9. Lightman et al. (2023), *Let’s Verify Step by Step* [`GMGQ2RVG`]
10. Wang et al. (2023), *Math-Shepherd* [`XZM4TK2Q`]
11. Yuan et al. (2024), *Self-Rewarding Language Models* [`I7U5FHBM`]

## Comparative synthesis

### 1) Pairwise ranking objectives: strengths and limits
**Strengths**
- Very scalable and cheap relative to dense process labeling.
- Strong for style/helpfulness/harmlessness preference shaping (Christiano 2017; Ouyang 2022; DPO/RRHF/RLAIF).
- DPO/RRHF simplify optimization versus full RL pipelines.

**Limits (sufficiency failures)**
- **Underspecification**: pairwise judgments on full outputs do not uniquely identify correct latent reasoning; many distinct chains can produce same final text quality.
- **Credit assignment collapse**: supervision lands on whole response, not intermediate steps; hard to fix specific reasoning errors.
- **Reward hacking / verbosity bias**: models can exploit annotator or reward-model heuristics (persuasive style, longer answers) without better internal correctness.
- **Weak signal in domains with objective correctness** (math, logic, code proofs) unless pairwise labels are extremely high quality and domain-specialized.

### 2) Outcome supervision (final-answer correctness, trajectory-level verifiers)
**Strengths**
- Better aligned than generic preference for tasks with verifiable outcomes.
- Cobbe et al. show verifier-guided reranking improves math solve rates.
- Lower annotation burden than full process traces.

**Limits**
- Still coarse: correct final answer can mask flawed intermediate reasoning.
- Sparse signal for long-horizon reasoning; hard to detect where error occurred.
- Can overfit shortcut patterns that correlate with correct final answers.

### 3) Process supervision / verifier traces
**Evidence where process matters**
- Uesato et al. (2022): direct process-vs-outcome comparisons indicate process feedback can improve reasoning reliability/generalization.
- Lightman et al. (2023): process reward models (PRM) outperform outcome reward models in key math reasoning settings; step-level signals are more diagnostic.
- Math-Shepherd extends step-level verification with weaker/automatic supervision, showing practical gains without fully manual dense labels.

**Why it helps**
- Finer-grained credit assignment.
- Better detection of local reasoning faults early in chain.
- Better robustness when outcome labels are sparse/ambiguous.

**Tradeoff**
- Labeling process traces is expensive; requires high-quality rubrics and QA.

### 4) Hybrid objectives
- Constitutional AI and RLAIF combine preference optimization with critique/revision or AI-generated supervisory signals.
- Self-Rewarding LM frames iterative generation + judging loops as a scalable hybrid.
- In practice, hybrids can recover much of process-supervision benefit when human trace labels are limited, but may inherit judge/model bias.

## Practical recommendations by data regime

### Regime A: **Low data / low budget**
- Start with **pairwise ranking** (DPO/RRHF style) on carefully curated prompts.
- Add **outcome checks** where possible (unit tests, exact-match graders, schema validators).
- Avoid overclaiming reasoning improvement from pairwise wins alone.

### Regime B: **Medium data budget**
- Use **hybrid training**: pairwise objective + targeted outcome supervision on high-stakes domains.
- Add lightweight **process signals** on a small but representative subset (error-prone tasks).
- Train verifier/reranker to improve sample selection at inference.

### Regime C: **High data / safety-critical reasoning**
- Invest in **process supervision** (step labels or trace verification) for core domains.
- Combine with outcome and preference objectives in multi-stage training.
- Use separate verifier models and adversarial evals for shortcut/reward-hacking detection.

### Regime D: **Noisy labels / weak human expertise**
- Prefer **AI-assisted critique + filtering** (Constitutional/RLAIF-like pipelines).
- Distill high-confidence subsets for human review.
- Treat automated verifier traces as provisional; calibrate against gold expert traces.

## Bottom line
- **Pairwise ranking is usually necessary but not sufficient** for robust reasoning consistency.
- **Outcome supervision** improves objective-task alignment but remains coarse.
- **Process supervision/verifier traces** provide the strongest evidence for improved reasoning reliability where intermediate correctness matters.
- Best practical recipe: **progressive hybridization** — start pairwise, layer outcome checks, then add targeted process supervision where error costs are highest.
