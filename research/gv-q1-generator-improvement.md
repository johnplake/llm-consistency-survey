# GV Q1 — Improving Generator Quality Using Validator/Judge Signals

Target collection: **LLM-inconsistency / GV-Generator-improvement-using-validator** (group library)

Selection criterion used here: papers where a validator/judge/reward/ranker signal is used to *improve generation* (training and/or decoding), beyond plain SFT alone.

## Added papers (10)

1. **Training Verifiers to Solve Math Word Problems** (Cobbe et al., 2021)  
   Link: https://arxiv.org/abs/2110.14168  
   Why relevant: canonical generator+verifier setup; trains a verifier to score sampled solutions and uses verifier-guided selection to improve final answers.  
   SFT relation: **Beats plain generator-only SFT at inference** via verifier reranking (best-of-N + scoring), and motivates verifier-aware training loops.

2. **Solving Math Word Problems With Process- and Outcome-Based Feedback** (Uesato et al., 2022)  
   Link: https://arxiv.org/abs/2211.14275  
   Why relevant: directly studies reward/validator design (outcome vs process supervision) and uses those signals to improve generated reasoning quality.  
   SFT relation: **Complements and can outperform SFT baselines** when reward feedback is integrated (especially process-aware signals).

3. **Let’s Verify Step by Step** (Lightman et al., 2023)  
   Link: https://arxiv.org/abs/2305.20050  
   Why relevant: trains process supervision verifiers/reward models for intermediate steps; uses them to select better chains.  
   SFT relation: **Improves over pure SFT decoding** by adding verifier-guided search/selection over candidate reasoning traces.

4. **Constitutional AI: Harmlessness from AI Feedback** (Bai et al., 2022)  
   Link: https://arxiv.org/abs/2212.08073  
   Why relevant: uses AI-generated critique/judge signals plus rejection sampling and RL from AI feedback to improve generator behavior.  
   SFT relation: **Explicitly beyond SFT** (SFT + AI feedback + RLHF-style optimization); shows quality/alignment gains from judge-like feedback loops.

5. **ReST: Reinforced Self-Training for Language Modeling** (Gulcehre et al., 2023)  
   Link: https://arxiv.org/abs/2308.08998  
   Why relevant: combines policy improvement with reward/quality scoring and filtering; a direct “reward-model-guided self-training” recipe.  
   SFT relation: **Designed as an alternative/complement to SFT-only tuning**, using reward-guided data selection and iterative improvement.

6. **RRHF: Rank Responses to Align Language Models with Human Feedback** (Yuan et al., 2023)  
   Link: https://arxiv.org/abs/2304.05302  
   Why relevant: uses ranked responses (a judge/ranker signal) to optimize generation quality directly without full RL pipelines.  
   SFT relation: **Beyond vanilla SFT** by incorporating ranking supervision; generally stronger than SFT on preference-alignment style metrics.

7. **Direct Preference Optimization: Your Language Model is Secretly a Reward Model** (Rafailov et al., 2023)  
   Link: https://arxiv.org/abs/2305.18290  
   Why relevant: core method for using pairwise preference labels (human or validator-generated) to directly optimize generator policy.  
   SFT relation: **Alternative to SFT/RLHF stages**; not itself a verifier paper, but highly relevant when validator/judge supplies preference labels.

8. **Self-Refine: Iterative Refinement with Self-Feedback** (Madaan et al., 2023)  
   Link: https://arxiv.org/abs/2303.17651  
   Why relevant: generator receives critique/feedback and revises outputs iteratively; a direct “critic-guided refinement” paradigm.  
   SFT relation: **Inference-time complement to SFT**; gains come from validator-like feedback loops without retraining requirements.

9. **Self-Rewarding Language Models** (Yuan et al., 2024)  
   Link: https://arxiv.org/abs/2401.10020  
   Why relevant: uses model-generated reward/judge signals in iterative preference optimization; tightly matches validator-labeled DPO-style improvement.  
   SFT relation: **Beyond SFT** via self-generated reward supervision + preference optimization; reports improvements over SFT-only baselines.

10. **LLM-Blender: Ensembling Large Language Models with PairRank and GenFuser** (Jiang et al., 2023)  
    Link: https://arxiv.org/abs/2306.02561  
    Why relevant: explicit ranking/reranking (PairRank) of candidate generations before fusion; decoder-side quality improvement via judge/ranker signal.  
    SFT relation: **Complements SFT models at inference**, improving outputs through reranking and fusion rather than generator retraining alone.

---

## Notes on scope decisions

- Included: methods using **validator/reward/ranker/critic** signals for generation-time selection or training-time policy updates.
- Excluded: papers that are only about evaluator calibration/reliability and do not demonstrate generator-quality improvement workflows.
- DPO was included because it is a key objective when validator/judge labels can be converted into pairwise preferences.

All 10 papers were added to the target Zotero subcollection with PDF attachments where available (all had downloadable PDFs).