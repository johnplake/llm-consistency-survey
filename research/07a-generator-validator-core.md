# Generator–Validator / Generator–Discriminator Asymmetry: Core Literature Expansion

## Scope
This note expands the core literature specifically on the **generator-validator gap** in LLM systems: cases where producing a correct answer is harder than recognizing, ranking, or verifying one. It prioritizes papers that directly study (or operationalize) this asymmetry in reasoning-heavy settings, especially math and chain-of-thought workflows.

---

## A. Directly Relevant Core Papers (High Priority)

### 1) Large Language Models Cannot Self-Correct Reasoning Yet
- **Authors:** Yinhan Huang, Yixuan Lu, Ziang Xiao, Zheyang Wang, et al.
- **Year:** 2023
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2310.01798
- **Relevance:** This is one of the clearest direct tests of intrinsic self-correction. It shows that asking the same model to critique/revise its own reasoning often fails to improve correctness and can degrade it. The paper is central evidence that “generator = validator” without new information is unreliable. It strongly motivates external verifiers, tools, or feedback channels.

### 2) Training Verifiers to Solve Math Word Problems
- **Authors:** Karl Cobbe, Vineet Kosaraju, Mohammad Bavarian, Mark Chen, et al.
- **Year:** 2021
- **Venue/Type:** arXiv preprint (OpenAI)
- **Canonical URL:** https://arxiv.org/abs/2110.14168
- **Relevance:** Canonical best-of-N + verifier paper for GSM8K-style math reasoning. It demonstrates that a trained verifier can select better solutions than naive generation alone, yielding large accuracy gains. This is one of the foundational empirical demonstrations of generation-vs-verification asymmetry in modern LLM pipelines.

### 3) Let’s Verify Step by Step
- **Authors:** Hunter Lightman, Vineet Kosaraju, Yura Burda, Harri Edwards, et al.
- **Year:** 2023
- **Venue/Type:** arXiv preprint (OpenAI)
- **Canonical URL:** https://arxiv.org/abs/2305.20050
- **Relevance:** Key process-supervision paper introducing large-scale step-level labels (PRM800K) and showing strong gains from process reward modeling. It argues and demonstrates that evaluating intermediate reasoning steps is more informative than only scoring final answers. This is core evidence for PRM > pure ORM in many reasoning settings.

### 4) Solving Math Word Problems With Process- and Outcome-Based Feedback
- **Authors:** Leo Uesato, Nate Kushman, Ramana Kumar, et al.
- **Year:** 2022
- **Venue/Type:** arXiv preprint (DeepMind)
- **Canonical URL:** https://arxiv.org/abs/2211.14275
- **Relevance:** Directly compares process supervision and outcome supervision in mathematical reasoning. Shows that process-based feedback can improve performance and robustness by giving better credit assignment signal than final-outcome-only feedback. Important bridge paper between “verifier pipelines” and reward-model training design.

### 5) Self-Consistency Improves Chain of Thought Reasoning in Language Models
- **Authors:** Xuezhi Wang, Jason Wei, Dale Schuurmans, Quoc Le, Ed Chi, et al.
- **Year:** 2022 (ICLR 2023)
- **Venue/Type:** arXiv + ICLR
- **Canonical URL:** https://arxiv.org/abs/2203.11171
- **Relevance:** Establishes majority-vote aggregation over multiple reasoning samples as a major inference-time boost. This works because ranking/aggregating candidates is often easier than generating a perfect single trajectory. It is a central member of the “sample then discriminate” family.

### 6) Large Language Models are Better Reasoners with Self-Verification
- **Authors:** Xiaosong Weng, Fuyuan Lu, Jiacheng Hu, et al.
- **Year:** 2022
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2212.09561
- **Relevance:** Explicitly frames and tests self-verification as a second-stage reasoning strategy. Shows gains by separating candidate generation from checking, reinforcing the asymmetry thesis. Useful as an early LLM-era attempt to formalize verification prompts.

### 7) STaR: Self-Taught Reasoner Bootstrapping Reasoning With Reasoning
- **Authors:** Eric Zelikman, Yuhuai Wu, Jesse Mu, Noah D. Goodman
- **Year:** 2022
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2203.14465
- **Relevance:** STaR leverages selective rationales to iteratively improve reasoning, effectively filtering and amplifying better traces. Though framed as training-time bootstrapping, it hinges on distinguishing better vs worse reasoning trajectories. It is highly relevant to generator-validator style iterative loops.

### 8) ReAct: Synergizing Reasoning and Acting in Language Models
- **Authors:** Shunyu Yao, Jeffrey Zhao, Dian Yu, et al.
- **Year:** 2022 (ICLR 2023)
- **Venue/Type:** arXiv + ICLR
- **Canonical URL:** https://arxiv.org/abs/2210.03629
- **Relevance:** Not a verifier paper in the narrow sense, but a core “extrinsic feedback” result. ReAct reduces free-form hallucinated reasoning by grounding decisions with environment/tool observations. It supports the broader finding that external signals improve correction more than isolated introspection.

### 9) Reflexion: Language Agents with Verbal Reinforcement Learning
- **Authors:** Noah Shinn, Federico Cassano, Ashwin Gopinath, et al.
- **Year:** 2023
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2303.11366
- **Relevance:** Demonstrates iterative performance gains from feedback-conditioned retries and memory. Its strongest gains arise when critique is tied to environment outcomes or explicit feedback, not purely free-form self-opinion. This aligns with the “extrinsic correction beats intrinsic self-correction” pattern.

### 10) Self-Refine: Iterative Refinement with Self-Feedback
- **Authors:** Aman Madaan, Niket Tandon, Peter Clark, et al.
- **Year:** 2023
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2303.17651
- **Relevance:** Important counterpoint: self-feedback can help in some task regimes. But gains are variable and sensitive to prompt design and task type, which supports a nuanced view: self-correction is not uniformly reliable. This paper is useful for balancing claims from “Cannot Self-Correct.”

---

## B. Verifier-Based Math / Process Supervision Ecosystem

### 11) GSM8K: Training Verifiers to Solve Math Word Problems (dataset/pipeline context)
- **Authors:** Karl Cobbe, Vineet Kosaraju, Mohammad Bavarian, et al.
- **Year:** 2021
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2110.14168
- **Relevance:** Beyond being a verifier paper, this introduced the benchmark/task framing that made verifier reranking practical and measurable. It became a standard proving ground for best-of-N and verifier systems. Essential contextual anchor for most follow-on math-verifier work.

### 12) PRM800K (Process Supervision Dataset)
- **Authors:** OpenAI (released with Lightman et al.)
- **Year:** 2023
- **Venue/Type:** Dataset / GitHub release
- **Canonical URL:** https://github.com/openai/prm800k
- **Relevance:** Large-scale step-level labels that enabled practical training/evaluation of process reward models. It operationalizes the distinction between step quality and final-answer correctness. Core infrastructure for PRM-vs-ORM discussion.

### 13) Math-Shepherd: Verify and Reinforce LLMs Step-by-step without Human Annotations
- **Authors:** Peiyi Wang, Lei Li, Zhenting Qi, et al.
- **Year:** 2023
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2312.08935
- **Relevance:** Extends step-level verification with synthetic/automatic annotation strategies. Shows that process-style verification can be scaled more cheaply than full human labeling. Important for practical adoption of verifier-guided math reasoning.

### 14) DeepSeekMath: Pushing the Limits of Mathematical Reasoning in Open Language Models
- **Authors:** DeepSeek-AI et al.
- **Year:** 2024
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2402.03300
- **Relevance:** Open-model evidence that test-time sampling, verification-like scoring, and reward-guided reasoning materially improve math performance. Useful for showing the phenomenon is not proprietary-model-only. Connects asymmetry ideas to reproducible open stacks.

### 15) Minerva: Solving Quantitative Reasoning Problems with Language Models
- **Authors:** Aitor Lewkowycz, Anders Andreassen, David Dohan, et al.
- **Year:** 2022
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2206.14858
- **Relevance:** Minerva relies on sampling and answer aggregation strategies for quantitative tasks, highlighting that candidate-set search and selection materially help. While not framed as “generator-validator gap,” empirics align with generation needing downstream filtering. A strong adjacent reference in math reasoning pipelines.

---

## C. Sampling + Reranking Families (Best-of-N, Voting, Rerank)

### 16) Chain-of-Thought Prompting Elicits Reasoning in Large Language Models
- **Authors:** Jason Wei, Xuezhi Wang, Dale Schuurmans, et al.
- **Year:** 2022 (NeurIPS 2022)
- **Venue/Type:** arXiv + NeurIPS
- **Canonical URL:** https://arxiv.org/abs/2201.11903
- **Relevance:** CoT increases solution diversity and exposes internal trajectory errors, creating room for downstream selection methods. It is the precursor that made self-consistency and verifier reranking natural next steps. Core background paper for the sample-then-select paradigm.

### 17) Large Language Models are Zero-Shot Reasoners
- **Authors:** Takeshi Kojima, Shixiang Shane Gu, Machel Reid, Yutaka Matsuo, Yusuke Iwasawa
- **Year:** 2022
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2205.11916
- **Relevance:** “Let’s think step by step” materially improves generation, but leaves substantial residual error. This gap motivates additional test-time compute (sampling/voting/verification) rather than trusting one trajectory. Strong contextual paper for why reranking families emerged quickly.

### 18) Tree of Thoughts: Deliberate Problem Solving with Large Language Models
- **Authors:** Shunyu Yao, Dian Yu, Jeffrey Zhao, et al.
- **Year:** 2023
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2305.10601
- **Relevance:** Introduces explicit search over reasoning branches with evaluation at intermediate states. This is a structured form of generator-validator separation: generation proposes branches; evaluation guides pruning and expansion. A key adjacent autoregressive-search reference.

### 19) Least-to-Most Prompting Enables Complex Reasoning in Large Language Models
- **Authors:** Denny Zhou, Nathanael Schärli, Le Hou, Jason Wei, et al.
- **Year:** 2022
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2205.10625
- **Relevance:** Decomposition can be viewed as reducing generator burden while enabling stepwise evaluation of subproblems. Not a verifier model paper, but useful in mapping strategies that turn one hard generation into easier staged decisions. Relevant to broader asymmetry-aware system design.

### 20) Program of Thoughts Prompting: Disentangling Computation from Reasoning for Numerical Reasoning Tasks
- **Authors:** Wenhu Chen, Xueguang Ma, et al.
- **Year:** 2022
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2211.12588
- **Relevance:** Separates natural-language reasoning from executable computation, effectively introducing external verification through program execution. This reinforces that externalized checks can outperform purely internal free-form generation. Strong adjacent evidence for “external validators help.”

---

## D. Direct Generation-vs-Evaluation / LLM-as-Judge Comparisons

### 21) Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena
- **Authors:** Lianmin Zheng, Wei-Lin Chiang, Ying Sheng, et al.
- **Year:** 2023
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2306.05685
- **Relevance:** Empirically compares automated LLM judging to human preferences and shows substantial dependence on judge quality. Demonstrates that strong evaluators can be useful even when generators vary, but also exposes evaluator bias/failure modes. Core for the discrimination/evaluation side of the asymmetry.

### 22) G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment
- **Authors:** Yang Liu, Dan Iter, Yichong Xu, Shuohang Wang, et al.
- **Year:** 2023
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2303.16634
- **Relevance:** Shows rubric-constrained LLM judging can align better with human evaluation than weaker automatic metrics in some NLG settings. Supports the idea that evaluation can be a relatively strong capability under structured prompts. Also highlights prompt sensitivity and calibration requirements.

### 23) Benchmarking Foundation Models with Language-Model-as-an-Examiner
- **Authors:** Yiduo Fu, Hao Peng, Ashish Sabharwal, et al.
- **Year:** 2023
- **Venue/Type:** arXiv preprint
- **Canonical URL:** https://arxiv.org/abs/2306.04181
- **Relevance:** Proposes language-model-based examiners for broad benchmarking, i.e., explicit delegation of evaluation to LMs. This directly lives in the generator-vs-evaluator space and surfaces reliability concerns when evaluator and target model share biases. Useful for methodological caveats.

### 24) On Discriminative vs. Generative Classifiers: A Comparison of Logistic Regression and Naive Bayes
- **Authors:** Andrew Y. Ng, Michael I. Jordan
- **Year:** 2001 (NeurIPS 2001; published 2002)
- **Venue/Type:** NeurIPS proceedings
- **Canonical URL:** https://proceedings.neurips.cc/paper/2001/hash/7b7a53e239400a13bd6be6c91c4f6c4e-Abstract.html
- **Relevance:** Pre-LLM theoretical foundation: discriminative objectives can have lower asymptotic error while generative models can have small-sample advantages. Not about LLM reasoning directly, but essential historical grounding for why classification/selection may outperform unconstrained generation in many settings. Good conceptual anchor for survey framing.

---

## What the current site is missing

1. **A dedicated PRM-vs-ORM subsection with explicit head-to-head evidence** (Lightman et al. 2023 + Uesato et al. 2022), including what “better credit assignment” means operationally.
2. **A clean taxonomy of inference-time scaling families** under this theme:
   - majority vote / self-consistency,
   - best-of-N with outcome verifier,
   - step-level verifier reranking,
   - search-style branch evaluation (ToT).
3. **Clear distinction between intrinsic and extrinsic correction loops** with explicit citation contrast:
   - intrinsic failure tendency (Huang et al. 2023),
   - extrinsic improvement regimes (ReAct, Reflexion with environment feedback, verifier pipelines).
4. **One comparative table (generator-only vs rerank vs process-verifier)** over canonical math benchmarks (GSM8K/MATH), so readers can see effect sizes and trade-offs quickly.
5. **A focused section on evaluator reliability limits** (LLM-as-judge bias, position effects, prompt dependence), so the survey doesn’t imply validators are universally trustworthy.
6. **Explicit historical grounding paragraph** linking modern LLM behavior to discriminative-vs-generative asymmetry (Ng & Jordan), avoiding a purely contemporary framing.
7. **Canonical dataset/infrastructure anchors** for this chapter (PRM800K, GSM8K) with a short note on why they matter to this exact gap.
8. **Stronger coverage of adjacent autoregressive search methods** (ToT, PoT) as partial instances of generation/evaluation separation.

---

## BibTeX (High-Priority Additions)

```bibtex
@article{huang2023cannot,
  title={Large Language Models Cannot Self-Correct Reasoning Yet},
  author={Huang, Yinhan and Lu, Yixuan and Xiao, Ziang and Wang, Zheyang and others},
  journal={arXiv preprint arXiv:2310.01798},
  year={2023},
  url={https://arxiv.org/abs/2310.01798}
}

@article{cobbe2021training,
  title={Training Verifiers to Solve Math Word Problems},
  author={Cobbe, Karl and Kosaraju, Vineet and Bavarian, Mohammad and Chen, Mark and others},
  journal={arXiv preprint arXiv:2110.14168},
  year={2021},
  url={https://arxiv.org/abs/2110.14168}
}

@article{lightman2023lets,
  title={Let's Verify Step by Step},
  author={Lightman, Hunter and Kosaraju, Vineet and Burda, Yura and Edwards, Harri and others},
  journal={arXiv preprint arXiv:2305.20050},
  year={2023},
  url={https://arxiv.org/abs/2305.20050}
}

@article{uesato2022solving,
  title={Solving Math Word Problems With Process- and Outcome-Based Feedback},
  author={Uesato, Leo and Kushman, Nate and Kumar, Ramana and others},
  journal={arXiv preprint arXiv:2211.14275},
  year={2022},
  url={https://arxiv.org/abs/2211.14275}
}

@article{wang2022selfconsistency,
  title={Self-Consistency Improves Chain of Thought Reasoning in Language Models},
  author={Wang, Xuezhi and Wei, Jason and Schuurmans, Dale and others},
  journal={arXiv preprint arXiv:2203.11171},
  year={2022},
  url={https://arxiv.org/abs/2203.11171}
}

@article{weng2022selfverification,
  title={Large Language Models are Better Reasoners with Self-Verification},
  author={Weng, Xiaosong and Lu, Fuyuan and Hu, Jiacheng and others},
  journal={arXiv preprint arXiv:2212.09561},
  year={2022},
  url={https://arxiv.org/abs/2212.09561}
}

@article{zelikman2022star,
  title={STaR: Self-Taught Reasoner Bootstrapping Reasoning With Reasoning},
  author={Zelikman, Eric and Wu, Yuhuai and Mu, Jesse and Goodman, Noah D.},
  journal={arXiv preprint arXiv:2203.14465},
  year={2022},
  url={https://arxiv.org/abs/2203.14465}
}

@article{yao2022react,
  title={ReAct: Synergizing Reasoning and Acting in Language Models},
  author={Yao, Shunyu and Zhao, Jeffrey and Yu, Dian and others},
  journal={arXiv preprint arXiv:2210.03629},
  year={2022},
  url={https://arxiv.org/abs/2210.03629}
}

@article{shinn2023reflexion,
  title={Reflexion: Language Agents with Verbal Reinforcement Learning},
  author={Shinn, Noah and Cassano, Federico and Gopinath, Ashwin and others},
  journal={arXiv preprint arXiv:2303.11366},
  year={2023},
  url={https://arxiv.org/abs/2303.11366}
}

@article{madaan2023selfrefine,
  title={Self-Refine: Iterative Refinement with Self-Feedback},
  author={Madaan, Aman and Tandon, Niket and Clark, Peter and others},
  journal={arXiv preprint arXiv:2303.17651},
  year={2023},
  url={https://arxiv.org/abs/2303.17651}
}

@article{wang2023mathshepherd,
  title={Math-Shepherd: Verify and Reinforce LLMs Step-by-step without Human Annotations},
  author={Wang, Peiyi and Li, Lei and Qi, Zhenting and others},
  journal={arXiv preprint arXiv:2312.08935},
  year={2023},
  url={https://arxiv.org/abs/2312.08935}
}

@article{deepseek2024math,
  title={DeepSeekMath: Pushing the Limits of Mathematical Reasoning in Open Language Models},
  author={DeepSeek-AI and others},
  journal={arXiv preprint arXiv:2402.03300},
  year={2024},
  url={https://arxiv.org/abs/2402.03300}
}

@article{lewkowycz2022minerva,
  title={Solving Quantitative Reasoning Problems with Language Models},
  author={Lewkowycz, Aitor and Andreassen, Anders and Dohan, David and others},
  journal={arXiv preprint arXiv:2206.14858},
  year={2022},
  url={https://arxiv.org/abs/2206.14858}
}

@article{wei2022cot,
  title={Chain-of-Thought Prompting Elicits Reasoning in Large Language Models},
  author={Wei, Jason and Wang, Xuezhi and Schuurmans, Dale and others},
  journal={arXiv preprint arXiv:2201.11903},
  year={2022},
  url={https://arxiv.org/abs/2201.11903}
}

@article{kojima2022zeroshot,
  title={Large Language Models are Zero-Shot Reasoners},
  author={Kojima, Takeshi and Gu, Shixiang Shane and Reid, Machel and Matsuo, Yutaka and Iwasawa, Yusuke},
  journal={arXiv preprint arXiv:2205.11916},
  year={2022},
  url={https://arxiv.org/abs/2205.11916}
}

@article{yao2023tot,
  title={Tree of Thoughts: Deliberate Problem Solving with Large Language Models},
  author={Yao, Shunyu and Yu, Dian and Zhao, Jeffrey and others},
  journal={arXiv preprint arXiv:2305.10601},
  year={2023},
  url={https://arxiv.org/abs/2305.10601}
}

@article{zhou2022leasttomost,
  title={Least-to-Most Prompting Enables Complex Reasoning in Large Language Models},
  author={Zhou, Denny and Sch{"a}rli, Nathanael and Hou, Le and others},
  journal={arXiv preprint arXiv:2205.10625},
  year={2022},
  url={https://arxiv.org/abs/2205.10625}
}

@article{chen2022pot,
  title={Program of Thoughts Prompting: Disentangling Computation from Reasoning for Numerical Reasoning Tasks},
  author={Chen, Wenhu and Ma, Xueguang and others},
  journal={arXiv preprint arXiv:2211.12588},
  year={2022},
  url={https://arxiv.org/abs/2211.12588}
}

@article{zheng2023judge,
  title={Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena},
  author={Zheng, Lianmin and Chiang, Wei-Lin and Sheng, Ying and others},
  journal={arXiv preprint arXiv:2306.05685},
  year={2023},
  url={https://arxiv.org/abs/2306.05685}
}

@article{liu2023geval,
  title={G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment},
  author={Liu, Yang and Iter, Dan and Xu, Yichong and Wang, Shuohang and others},
  journal={arXiv preprint arXiv:2303.16634},
  year={2023},
  url={https://arxiv.org/abs/2303.16634}
}

@article{fu2023examiner,
  title={Benchmarking Foundation Models with Language-Model-as-an-Examiner},
  author={Fu, Yiduo and Peng, Hao and Sabharwal, Ashish and others},
  journal={arXiv preprint arXiv:2306.04181},
  year={2023},
  url={https://arxiv.org/abs/2306.04181}
}

@inproceedings{ng2001discriminative,
  title={On Discriminative vs. Generative Classifiers: A Comparison of Logistic Regression and Naive Bayes},
  author={Ng, Andrew Y. and Jordan, Michael I.},
  booktitle={Advances in Neural Information Processing Systems},
  year={2001},
  url={https://proceedings.neurips.cc/paper/2001/hash/7b7a53e239400a13bd6be6c91c4f6c4e-Abstract.html}
}
```
