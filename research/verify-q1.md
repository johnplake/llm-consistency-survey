## Training Verifiers to Solve Math Word Problems (Cobbe et al., 2021)
Claim: "This paper introduces GSM8K (8.5K grade-school math problems)." → VERIFIED
Claim: "[It] proposes training a separate learned verifier to score candidate solutions sampled from a generator; the highest-scoring candidate is selected." → VERIFIED
Claim: "Adding a verifier at reranking time can yield gains comparable to roughly a 30× increase in model size." → VERIFIED
Claim: "The verifier is trained on math and needs re-training or re-calibration for other domains." → UNVERIFIABLE (paper evidence is math-domain; explicit cross-domain retraining requirement is not directly demonstrated)
Claim: "Open question is how verifier quality and candidate sample count trade off at fixed compute budget." → UNVERIFIABLE (framed as commentary; not a directly stated quantified result)

## Solving Math Word Problems With Process- and Outcome-Based Feedback (Uesato et al., 2022)
Claim: "First rigorous comparison of process-based vs outcome-based feedback for math reasoning (GSM8K)." → UNVERIFIABLE ("first" priority claim not strictly verifiable from this paper alone)
Claim: "Using Chinchilla-family models..." → INCORRECT: paper reports a Base-70B model and compares against prior systems (e.g., PaLM-540B, Minerva-540B, Codex-175B, InstructGPT-175B); it does not present itself as a Chinchilla-family study.
Claim: "They study SFT, outcome reward modeling (ORM), process reward modeling (PRM), and expert-iteration-style RL variants." → VERIFIED
Claim: "Final-answer error falls from 16.8% to 12.7%." → VERIFIED
Claim: "Trace error falls from 14.0% to 3.4% (best models)." → VERIFIED
Claim: "With 30% abstention, final-answer error reaches 2.7%." → VERIFIED
Claim: "Outcome-only supervision is inferior in trace quality (23.5% vs 22.3% without RMs; 16.6% vs 14.8% with RMs)." → VERIFIED
Claim: "Process-aware validators improve both final-answer correctness and reasoning trace quality." → VERIFIED
Claim: "Main limitation is annotation cost for step-level labels." → VERIFIED (paper discusses human process annotations and their cost/collection burden)

## Let's Verify Step by Step (Lightman et al., 2023)
Claim: "This paper scales process supervision with PRM800K, a dataset of 800,000 human step-level labels." → VERIFIED
Claim: "Domain/task is math reasoning on MATH benchmark." → VERIFIED
Claim: "They compare ORMs vs PRMs, and step-level supervision outperforms outcome-level." → VERIFIED
Claim: "Best reported accuracy is ~78.2% on a representative subset of MATH test with PRM-guided best-of-N selection." → VERIFIED
Claim: "Active learning gives a 2.6× data-efficiency gain for process labels." → VERIFIED
Claim: "Open question: can synthetic step labels replace part of PRM800K?" → UNVERIFIABLE (reasonable extrapolation, but not a directly established paper result)

## Constitutional AI (Bai et al., 2022)
Claim: "Introduces a two-stage pipeline: (1) SFT with self-critique/revision under a constitution, then (2) RL from AI-generated pairwise feedback (RLAIF)." → VERIFIED
Claim: "Goal is improving harmlessness while maintaining helpfulness with substantially reduced human preference labeling." → VERIFIED
Claim: "Human evaluations report improved harmlessness/helpfulness trade-off versus RLHF baselines." → VERIFIED
Claim: "Model serves as its own validator under structured principle prompting, producing scalable training signal." → VERIFIED
Claim: "Constitution quality is a bottleneck; biased principles propagate into training." → UNVERIFIABLE (plausible interpretation; not presented as a directly measured quantitative finding)

## ReST: Reinforced Self-Training (Gulcehre et al., 2023)
Claim: "ReST is an offline iterative alternative to online PPO/RLHF with Grow and Improve steps." → VERIFIED
Claim: "Grow samples data from current policy; Improve filters with reward model then applies offline RL." → VERIFIED
Claim: "Instantiated primarily for machine translation." → VERIFIED
Claim: "IWSLT14 De-En: +5.3; Web Domain En-Zh: +0.8." → VERIFIED (reported as gains over earlier Grow-stage setting)
Claim: "Human preference gains are reported alongside." → VERIFIED
Claim: "Generalization to open-ended instruction following is not the primary contribution." → VERIFIED

## RRHF: Rank Responses to Align Language Models with Human Feedback (Yuan et al., 2023)
Claim: "RRHF replaces PPO-style RL with a ranking-based loss over responses." → VERIFIED
Claim: "Uses mixed response sources (self model, other LMs, human demonstrations)." → VERIFIED
Claim: "Aligns toward judge-preferred outputs without a separate RL inner loop." → VERIFIED
Claim: "Reports alignment comparable to PPO on Helpful-Harmless via reward-model and human evals." → VERIFIED
Claim: "Reward-model accuracy examples around 68.49%." → INCORRECT: 68.49% in the paper is for a specific reward model benchmark entry (Dahoas/gptj-rm-static), not a general RRHF alignment score.
Claim: "Strong sensitivity to candidate sampling quality / weak diversity degrades ranking signal." → UNVERIFIABLE (not established with a clear quantified sensitivity study in the paper text)

## Direct Preference Optimization (Rafailov et al., 2023)
Claim: "DPO removes separate reward-model fitting and online RL rollouts by directly optimizing preferences." → VERIFIED
Claim: "Derives a direct binary cross-entropy objective over preference pairs." → VERIFIED
Claim: "Pairwise judge/human preferences can be converted directly into generator weight updates." → VERIFIED
Claim: "Paper reports ~61% win rate at temperature 0 vs PPO ~57%." → VERIFIED
Claim: "Those 61/57 numbers are on summarization/dialogue tasks." → INCORRECT: the cited 61% vs 57% figure is from TL;DR summarization evaluation (GPT-4 judged against references), not a single aggregate over both summarization and dialogue human eval.

## Self-Refine: Iterative Refinement with Self-Feedback (Madaan et al., 2023)
Claim: "Uses the same LLM in generator/critic/refiner roles, iterating without weight updates." → VERIFIED
Claim: "Evaluates on 7 diverse tasks including dialog, constrained generation, code, and math reasoning." → VERIFIED
Claim: "~20% average absolute improvement vs one-shot generation, with ~5–40% task-specific range." → VERIFIED
Claim: "For code optimization (GPT-4), accuracy improves from 27.3% to 36.0%." → VERIFIED
Claim: "Self-feedback can be wrong and gains plateau." → UNVERIFIABLE (qualitative interpretation; explicit plateau quantification not clearly established as a headline result)

## Self-Rewarding Language Models (Yuan et al., 2024)
Claim: "Trains Llama 2 70B iteratively using model-generated judge scores as reward signal." → VERIFIED
Claim: "Loop is generate candidates → judge pairwise → create preferences → run DPO; repeated over rounds." → VERIFIED
Claim: "AlpacaEval-over-GPT-4-Turbo win rates improve 9.94% (M1) → 15.38% (M2) → 20.44% (M3)." → VERIFIED
Claim: "M3 wins 62.5% vs 9.8% against SFT baseline." → VERIFIED
Claim: "Generator and validator are unified and co-improved in a closed loop." → VERIFIED
Claim: "Risk is self-reinforcing judge bias / stability over many more rounds remains open." → UNVERIFIABLE (forward-looking interpretation rather than directly measured long-horizon result)

## LLM-Blender (Jiang et al., 2023)
Claim: "Introduces PairRank (pairwise ranker) and GenFuser (fusion generator)." → VERIFIED
Claim: "Introduces MixInstruct benchmark." → VERIFIED
Claim: "No single model is best on more than 21% of examples." → VERIFIED (paper reports ~21.22%)
Claim: "PairRank-selected outputs average GPT-rank 3.20, ~18% relative improvement over best single model." → VERIFIED
Claim: "Demonstrates a ranking validator can extract quality from ensemble diversity beyond any single generator." → VERIFIED
Claim: "Requires multiple candidate generators and adds latency." → UNVERIFIABLE (architecturally plausible; explicit latency quantification not clearly reported as a formal measured claim)
