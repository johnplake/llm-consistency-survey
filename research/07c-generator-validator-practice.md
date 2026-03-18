# Generator–Validator Gap in Practice: Expanded Literature Pass

## Scope
This pass focuses on **practical/system-building evidence** for the generator–validator gap, especially items that strengthen:
- LLM-as-judge reliability and bias analysis
- inference-time compute scaling (search, voting, reranking, verifiers)
- self-critique/self-refine/constitutional pipelines and their limits
- concrete open repos used in real stacks
- benchmark evidence for generation-vs-evaluation asymmetry

---

## Must-add now (prioritized top 10)

1. **Tree of Thoughts: Deliberate Problem Solving with Large Language Models** (Yao et al., 2023)  
   URL: https://arxiv.org/abs/2305.10601  
   Why now: canonical search-over-thoughts framing; explicit compute-for-search tradeoff.

2. **Language Agent Tree Search (LATS): LLMs as Optimizers with Environment Feedback** (Zhou et al., 2023)  
   URL: https://arxiv.org/abs/2310.04406  
   Why now: practical integration of tree search + reflection + external reward signal.

3. **Large Language Models are not Fair Evaluators** (Wang et al., 2023)  
   URL: https://arxiv.org/abs/2305.17926  
   Why now: direct evidence that judge models carry systematic biases; key caveat for validator role.

4. **AlpacaEval: An Automatic Evaluator of Instruction-following Models** (Dubois et al., 2023)  
   URL: https://arxiv.org/abs/2307.12652  
   Why now: operational benchmark infrastructure for fast LLM-as-judge comparisons.

5. **PandaLM: An Automatic Evaluation Benchmark for LLM Instruction Tuning Optimization** (Wang et al., 2023)  
   URL: https://arxiv.org/abs/2306.05087  
   Why now: practical auto-judge setup with pairwise protocols and bias diagnostics.

6. **JudgeLM: Fine-tuned Large Language Models are Scalable Judges** (Zhu et al., 2023)  
   URL: https://arxiv.org/abs/2310.17631  
   Why now: shows how to distill/scale judge capability rather than relying only on frontier APIs.

7. **Prometheus: Inducing Fine-grained Evaluation Capability in Language Models** (Kim et al., 2024)  
   URL: https://arxiv.org/abs/2310.08491  
   Why now: rubric-conditioned judging; bridges evaluator training with production eval criteria.

8. **SelfCheckGPT: Zero-Resource Black-Box Hallucination Detection for Generative Large Language Models** (Manakul et al., 2023)  
   URL: https://arxiv.org/abs/2303.08896  
   Why now: simple but effective generation-consistency-as-validator signal in black-box settings.

9. **Chain-of-Verification Reduces Hallucination in Large Language Models** (Dhuliawala et al., 2024)  
   URL: https://arxiv.org/abs/2309.11495  
   Why now: explicit verification chain design pattern with practical reliability gains.

10. **Do Language Models Know When They’re Wrong?** (Kadavath et al., 2022)  
    URL: https://arxiv.org/abs/2207.05221  
    Why now: calibration/confidence evidence for when validators can be trusted and when not.

---

## A. LLM-as-judge reliability, bias, and evaluator training

1. **Large Language Models are not Fair Evaluators** — *Wang et al.*, 2023  
   URL: https://arxiv.org/abs/2305.17926  
   Why it matters: documents position/style/verbosity and other judge biases; essential caution for validator deployment.

2. **PandaLM: An Automatic Evaluation Benchmark for LLM Instruction Tuning Optimization** — *Wang et al.*, 2023  
   URL: https://arxiv.org/abs/2306.05087  
   Why it matters: practical pairwise LLM-judge framework with explicit meta-eval framing.

3. **AlpacaEval: An Automatic Evaluator of Instruction-following Models** — *Dubois et al.*, 2023  
   URL: https://arxiv.org/abs/2307.12652  
   Why it matters: high-velocity benchmark pipeline used broadly in open-model iteration loops.

4. **JudgeLM: Fine-tuned Large Language Models are Scalable Judges** — *Zhu et al.*, 2023  
   URL: https://arxiv.org/abs/2310.17631  
   Why it matters: evaluator distillation recipe; lowers cost/latency for judge-heavy systems.

5. **Prometheus: Inducing Fine-grained Evaluation Capability in Language Models** — *Kim et al.*, 2024  
   URL: https://arxiv.org/abs/2310.08491  
   Why it matters: rubric-conditioned judging aligns better with task-specific criteria than raw preference prompts.

6. **G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment** — *Liu et al.*, 2023  
   URL: https://arxiv.org/abs/2303.16634  
   Why it matters: strong evaluator prompt design; demonstrates both usefulness and fragility of LLM judges.

7. **Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena** — *Zheng et al.*, 2023  
   URL: https://arxiv.org/abs/2306.05685  
   Why it matters: direct empirical baseline for judge-vs-human agreement and where it fails.

---

## B. Inference-time compute scaling via search, voting, and reranking

8. **Tree of Thoughts: Deliberate Problem Solving with Large Language Models** — *Yao et al.*, 2023  
   URL: https://arxiv.org/abs/2305.10601  
   Why it matters: formalizes branching search + evaluator-guided pruning.

9. **Language Agent Tree Search (LATS)** — *Zhou et al.*, 2023  
   URL: https://arxiv.org/abs/2310.04406  
   Why it matters: practical MCTS-like agent loop with critique and environment feedback.

10. **Reasoning via Planning with World Models and Monte Carlo Tree Search** — *Hao et al.*, 2023  
    URL: https://arxiv.org/abs/2305.14992  
    Why it matters: connects classical planning/search to LLM reasoning-time scaling.

11. **Graph of Thoughts: Solving Elaborate Problems with LLMs** — *Besta et al.*, 2023  
    URL: https://arxiv.org/abs/2308.09687  
    Why it matters: generalizes chain/tree structures for candidate exploration and selection.

12. **Self-Consistency Improves Chain of Thought Reasoning in Language Models** — *Wang et al.*, 2022/2023  
    URL: https://arxiv.org/abs/2203.11171  
    Why it matters: prototypical inference-time scaling law via sample-and-vote.

13. **Training Verifiers to Solve Math Word Problems** — *Cobbe et al.*, 2021  
    URL: https://arxiv.org/abs/2110.14168  
    Why it matters: strongest early best-of-N + verifier reranking result in reasoning.

14. **Let’s Verify Step by Step** — *Lightman et al.*, 2023  
    URL: https://arxiv.org/abs/2305.20050  
    Why it matters: process-level verification beats pure outcome scoring in many math settings.

---

## C. Self-refine / critique / constitutional loops (and limits)

15. **Self-Refine: Iterative Refinement with Self-Feedback** — *Madaan et al.*, 2023  
    URL: https://arxiv.org/abs/2303.17651  
    Why it matters: practical self-critique pipeline; useful baseline for “intrinsic” correction.

16. **Reflexion: Language Agents with Verbal Reinforcement Learning** — *Shinn et al.*, 2023  
    URL: https://arxiv.org/abs/2303.11366  
    Why it matters: shows gains when critique is tied to external/environment outcomes.

17. **Constitutional AI: Harmlessness from AI Feedback** — *Bai et al.*, 2022  
    URL: https://arxiv.org/abs/2212.08073  
    Why it matters: codifies structured critique criteria; important for validator objective design.

18. **Large Language Models Cannot Self-Correct Reasoning Yet** — *Huang et al.*, 2023  
    URL: https://arxiv.org/abs/2310.01798  
    Why it matters: key negative result for intrinsic self-correction without new signal.

19. **Chain-of-Verification Reduces Hallucination in Large Language Models** — *Dhuliawala et al.*, 2024  
    URL: https://arxiv.org/abs/2309.11495  
    Why it matters: practical decomposition of validate-then-answer style prompting.

20. **SelfCheckGPT: Zero-Resource Black-Box Hallucination Detection** — *Manakul et al.*, 2023  
    URL: https://arxiv.org/abs/2303.08896  
    Why it matters: low-friction validator proxy (sample consistency) usable without finetuning.

---

## D. Benchmark evidence for generation–evaluation asymmetry

21. **Do Language Models Know When They’re Wrong?** — *Kadavath et al.*, 2022  
    URL: https://arxiv.org/abs/2207.05221  
    Why it matters: confidence calibration is partial and task-dependent; separates generation quality from uncertainty estimation.

22. **TruthfulQA: Measuring How Models Mimic Human Falsehoods** — *Lin et al.*, 2021  
    URL: https://arxiv.org/abs/2109.07958  
    Why it matters: models can produce fluent but false generations; validators can mitigate but also share blind spots.

23. **MATH: Measuring Mathematical Problem Solving with the MATH Dataset** — *Hendrycks et al.*, 2021  
    URL: https://arxiv.org/abs/2103.03874  
    Why it matters: high-entropy reasoning benchmark where selection/reranking strategies show large gains.

24. **PRM800K Dataset/Release** — *OpenAI*, 2023  
    URL: https://github.com/openai/prm800k  
    Why it matters: practical step-level supervision substrate that enables validator-centric training/eval.

---

## E. High-value technical posts (practice-oriented)

25. **OpenAI — Let’s verify step by step** (2023-05-31)  
    URL: https://openai.com/research/lets-verify-step-by-step  
    Why it matters: concrete product-facing argument for process supervision and verifier pipelines.

26. **Anthropic — Constitutional AI: Harmlessness from AI Feedback** (2022-12-15)  
    URL: https://www.anthropic.com/research/constitutional-ai-harmlessness-from-ai-feedback  
    Why it matters: practical critique-revision loop design with explicit principles.

27. **LMSYS — MT-Bench / Chatbot Arena resources** (2023–ongoing)  
    URL: https://lmsys.org/blog/2023-06-22-leaderboard/  
    Why it matters: operational guidance for pairwise judging and evaluator benchmarking.

28. **OpenAI — Learning to reason with LLMs (o1)** (2024)  
    URL: https://openai.com/index/learning-to-reason-with-llms/  
    Why it matters: strong industry framing of inference-time compute as core performance lever.

29. **Google DeepMind — AlphaCode 2 technical report/blog** (2024)  
    URL: https://deepmind.google/discover/blog/alphacode-2-solving-competitive-programming-problems/  
    Why it matters: real system combining generation, filtering, and selection at scale.

---

## F. Major repos to cite for system implementation

30. **openai/prm800k** (2023)  
    URL: https://github.com/openai/prm800k  
    Why it matters: step-level process supervision dataset/tools.

31. **openai/evals** (ongoing)  
    URL: https://github.com/openai/evals  
    Why it matters: production-style evaluator harness for model comparisons.

32. **lm-sys/FastChat** (ongoing)  
    URL: https://github.com/lm-sys/FastChat  
    Why it matters: Arena/MT-Bench infrastructure for LLM-as-judge and pairwise eval.

33. **tatsu-lab/alpaca_eval** (ongoing)  
    URL: https://github.com/tatsu-lab/alpaca_eval  
    Why it matters: lightweight automated preference eval used in open model iteration.

34. **huggingface/trl** (ongoing)  
    URL: https://github.com/huggingface/trl  
    Why it matters: practical reward-model and preference-optimization stack used with verifier-like objectives.

35. **vllm-project/vllm** (ongoing)  
    URL: https://github.com/vllm-project/vllm  
    Why it matters: infrastructure for high-throughput best-of-N / reranking-heavy inference pipelines.

36. **OpenBMB/UltraFeedback** (2023)  
    URL: https://github.com/OpenBMB/UltraFeedback  
    Why it matters: large-scale AI feedback data useful for training/benchmarking judge models.

---

## Notes on gaps this list closes

- Adds **judge-bias and judge-training** coverage missing from verifier-centric math-only discussions.
- Adds **search/planning-style inference-time scaling** (ToT/LATS/RAP/GoT), not only BoN+verifier.
- Adds **black-box verification methods** (SelfCheckGPT, Chain-of-Verification) useful in API-only practice.
- Adds **implementation repos** directly used in modern evaluator/reranker stacks.

---

## BibTeX (paper additions)

```bibtex
@article{yao2023tree,
  title={Tree of Thoughts: Deliberate Problem Solving with Large Language Models},
  author={Yao, Shunyu and Yu, Dian and Zhao, Jeffrey and others},
  journal={arXiv preprint arXiv:2305.10601},
  year={2023}
}

@article{zhou2023lats,
  title={Language Agent Tree Search Unifies Reasoning, Acting, and Planning in Language Models},
  author={Zhou, Andy and others},
  journal={arXiv preprint arXiv:2310.04406},
  year={2023}
}

@article{hao2023rap,
  title={Reasoning with Language Model is Planning with World Model},
  author={Hao, Shibo and Gu, Yi and Ma, Haotian and Hong, Joshua and Wang, Zhen and Wang, Daisy and Hu, Zhiting},
  journal={arXiv preprint arXiv:2305.14992},
  year={2023}
}

@article{besta2023graph,
  title={Graph of Thoughts: Solving Elaborate Problems with Large Language Models},
  author={Besta, Maciej and Blach, Nils and Kubicek, Ales and others},
  journal={arXiv preprint arXiv:2308.09687},
  year={2023}
}

@article{wang2023fair,
  title={Large Language Models are not Fair Evaluators},
  author={Wang, Xuhui and others},
  journal={arXiv preprint arXiv:2305.17926},
  year={2023}
}

@article{dubois2023alpacaeval,
  title={AlpacaEval: An Automatic Evaluator of Instruction-following Models},
  author={Dubois, Yann and Galambosi, Balazs and Liang, Percy and Hashimoto, Tatsunori},
  journal={arXiv preprint arXiv:2307.12652},
  year={2023}
}

@article{wang2023pandalm,
  title={PandaLM: An Automatic Evaluation Benchmark for LLM Instruction Tuning Optimization},
  author={Wang, Xuezhi and others},
  journal={arXiv preprint arXiv:2306.05087},
  year={2023}
}

@article{zhu2023judgelm,
  title={JudgeLM: Fine-tuned Large Language Models are Scalable Judges},
  author={Zhu, Wanrong and others},
  journal={arXiv preprint arXiv:2310.17631},
  year={2023}
}

@article{kim2024prometheus,
  title={Prometheus: Inducing Fine-grained Evaluation Capability in Language Models},
  author={Kim, Seungone and others},
  journal={arXiv preprint arXiv:2310.08491},
  year={2024}
}

@article{manakul2023selfcheckgpt,
  title={SelfCheckGPT: Zero-Resource Black-Box Hallucination Detection for Generative Large Language Models},
  author={Manakul, Potsawee and Liusie, Adian and Gales, Mark},
  journal={arXiv preprint arXiv:2303.08896},
  year={2023}
}

@article{dhuliawala2024cov,
  title={Chain-of-Verification Reduces Hallucination in Large Language Models},
  author={Dhuliawala, Shehzaad and others},
  journal={arXiv preprint arXiv:2309.11495},
  year={2024}
}

@article{kadavath2022knowwrong,
  title={Language Models (Mostly) Know What They Know},
  author={Kadavath, Saurav and others},
  journal={arXiv preprint arXiv:2207.05221},
  year={2022}
}
```

---

## Quick integration hint for main 07 chapter

If space is limited, merge as three sub-blocks under `07-generator-validator-gap.md`:
1. **Judge reliability is the validator bottleneck** (bias + distillation papers)  
2. **Inference-time compute is mostly search + evaluation** (ToT/LATS/RAP + verifier reranking)  
3. **Intrinsic critique is brittle; structured/extrinsic critique works better** (Self-Refine/Reflexion/Constitutional/CoV/SelfCheckGPT)
