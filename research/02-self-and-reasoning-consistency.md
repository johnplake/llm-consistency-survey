# Self-Consistency, Contradiction & Reasoning Consistency: Research Notes

## Self-Consistency Issues: Key Papers

1. **Self-Consistency Improves Chain of Thought Reasoning in Language Models**  
   **Authors:** Xuezhi Wang, Jason Wei, Dale Schuurmans, Quoc Le, Ed Chi, Sharan Narang, Aakanksha Chowdhery, Denny Zhou  
   **Year/Venue:** 2023, ICLR (paper first appeared in 2022 as arXiv preprint)  
   **URL:** https://arxiv.org/abs/2203.11171  
   Introduces *self-consistency decoding* (sample multiple CoT paths, majority-vote the final answer). Important for this survey because it addresses inconsistency as an *algorithmic mitigation*, not as a diagnosis of the underlying inconsistency problem.

2. **SelfCheckGPT: Zero-Resource Black-Box Hallucination Detection for Generative Large Language Models**  
   **Authors:** Potsawee Manakul, Adian Liusie, Mark Gales  
   **Year/Venue:** 2023, Findings of EMNLP  
   **URL:** https://arxiv.org/abs/2303.08896  
   Uses cross-sample inconsistency as a signal for hallucination: if independently sampled responses disagree strongly, factual reliability is lower. This is one of the clearest practical links between output inconsistency and factual untrustworthiness.

3. **TruthfulQA: Measuring How Models Mimic Human Falsehoods**  
   **Authors:** Stephanie Lin, Jacob Hilton, Owain Evans  
   **Year/Venue:** 2022, ACL  
   **URL:** https://arxiv.org/abs/2109.07958  
   Evaluates whether models produce truthful answers vs popular misconceptions. While not framed purely as “consistency,” it reveals models can provide contradictory/unstable factual claims across prompts and settings.

4. **CheckList: Beyond Accuracy Behavioral Testing of NLP Models**  
   **Authors:** Marco Tulio Ribeiro, Tongshuang Wu, Carlos Guestrin, Sameer Singh  
   **Year/Venue:** 2020, ACL  
   **URL:** https://aclanthology.org/2020.acl-main.442/  
   Introduces invariance tests (e.g., paraphrases) that directly target consistency failures. Widely adopted methodology for detecting prompt/paraphrase sensitivity.

5. **PAWS: Paraphrase Adversaries from Word Scrambling**  
   **Authors:** Yuan Zhang, Jason Baldridge, Luheng He  
   **Year/Venue:** 2019, NAACL  
   **URL:** https://aclanthology.org/N19-1382/  
   Shows strong lexical-overlap pairs can flip semantics, exposing brittleness to paraphrase-like variations. Useful for consistency audits because semantically similar forms can induce different model behavior.

6. **WinoGrande: An Adversarial Winograd Schema Challenge at Scale**  
   **Authors:** Keisuke Sakaguchi, Ronan Le Bras, Chandra Bhagavatula, Yejin Choi  
   **Year/Venue:** 2020, AAAI  
   **URL:** https://arxiv.org/abs/1907.10641  
   A pronoun/coreference benchmark that reduces annotation artifacts. Helpful for studying whether entity-resolution judgments remain stable under minimal surface changes.

7. **Winogender Schemas for Diagnosing Gender Bias in Coreference Resolution**  
   **Authors:** Rachel Rudinger, Jason Naradowsky, Brian Leonard, Benjamin Van Durme  
   **Year/Venue:** 2018, NAACL-HLT  
   **URL:** https://aclanthology.org/N18-2003/  
   Not an LLM-era paper, but highly relevant for consistency in pronoun/entity resolution: equivalent contexts with swapped demographics often lead to inconsistent predictions.

8. **Language Models (Mostly) Know What They Know**  
   **Authors:** Saurav Kadavath et al.  
   **Year/Venue:** 2022, arXiv preprint  
   **URL:** https://arxiv.org/abs/2207.05221  
   Primarily on calibration/confidence, but relevant to consistency because confidence and answer stability are related axes of reliability. Useful background for belief-consistency discussions.

## Paraphrase Sensitivity

1. **CheckList** (Ribeiro et al., ACL 2020) — https://aclanthology.org/2020.acl-main.442/  
   Behavioral testing framework with explicit invariance tests (e.g., rephrasings). Demonstrates that models frequently violate expected invariance under paraphrase.

2. **PAWS** (Zhang et al., NAACL 2019) — https://aclanthology.org/N19-1382/  
   Constructs hard paraphrase/non-paraphrase pairs; many models fail despite strong lexical cues. Highlights fragility to form-level perturbations.

3. **On the Robustness of Natural Language Processing Models to Spelling Noise**  
   **Authors:** Javid Ebrahimi et al.  
   **Year/Venue:** 2018, ACL  
   **URL:** https://aclanthology.org/P18-2006/  
   Early robustness study showing small input perturbations can strongly alter predictions. Though pre-LLM, the invariance logic carries over to prompt robustness tests.

4. **Right for the Wrong Reasons: Diagnosing Syntactic Heuristics in Natural Language Inference**  
   **Authors:** R. Thomas McCoy, Ellie Pavlick, Tal Linzen  
   **Year/Venue:** 2019, ACL  
   **URL:** https://aclanthology.org/P19-1334/  
   Shows models can rely on shallow heuristics and fail under controlled rephrasings that preserve meaning. Useful for understanding why paraphrase and reformulation can trigger inconsistent answers.

5. **PromptBench: Towards Evaluating the Robustness of Large Language Models on Adversarial Prompts**  
   **Authors:** Xinyu Zhu et al.  
   **Year/Venue:** 2023, arXiv  
   **URL:** https://arxiv.org/abs/2306.04528  
   Benchmarks how prompt variations and adversarial modifications affect outputs. Useful practical resource for measuring prompt sensitivity at scale.

## Logical Contradiction

1. **TruthfulQA** (Lin et al., ACL 2022) — https://arxiv.org/abs/2109.07958  
   Models often produce plausible but false statements; under different elicitation styles, answers can conflict with known facts. A core benchmark for factual contradiction tendencies.

2. **SelfCheckGPT** (Manakul et al., Findings EMNLP 2023) — https://arxiv.org/abs/2303.08896  
   Internal contradiction across sampled generations is used as a proxy for hallucination. Directly operationalizes contradiction detection without external knowledge bases.

3. **HaluEval: A Large-Scale Hallucination Evaluation Benchmark for Large Language Models**  
   **Authors:** Junyi Li et al.  
   **Year/Venue:** 2023, EMNLP Findings / arXiv  
   **URL:** https://arxiv.org/abs/2305.11747  
   Broad hallucination benchmark that includes contradiction-like failures against source evidence and world facts.

4. **ANLI: A New Benchmark for Natural Language Understanding**  
   **Authors:** Yichen Nie, Adina Williams, Emily Dinan, Mohit Bansal, Jason Weston  
   **Year/Venue:** 2020, ACL  
   **URL:** https://arxiv.org/abs/1910.14599  
   Adversarial NLI benchmark emphasizing contradiction/entailment discrimination in hard cases. Useful for logical consistency testing.

5. **HANS: Heuristic Analysis for NLI Systems**  
   **Authors:** R. Thomas McCoy, Ellie Pavlick, Tal Linzen  
   **Year/Venue:** 2019, ACL  
   **URL:** https://aclanthology.org/P19-1334/  
   A focused test set for lexical-overlap, subsequence, and constituent heuristics. Useful for contradiction consistency because it reveals logically invalid but high-confidence NLI behavior.

## Chain-of-Thought Faithfulness

1. **Chain-of-Thought Prompting Elicits Reasoning in Large Language Models**  
   **Authors:** Jason Wei et al.  
   **Year/Venue:** 2022, NeurIPS  
   **URL:** https://arxiv.org/abs/2201.11903  
   Foundational CoT prompting paper. Improves performance, but does not by itself guarantee that generated rationale is causally faithful.

2. **Large Language Models are Zero-Shot Reasoners**  
   **Authors:** Takeshi Kojima, Shixiang Shane Gu, Machel Reid, Yutaka Matsuo, Yusuke Iwasawa  
   **Year/Venue:** 2022, NeurIPS  
   **URL:** https://arxiv.org/abs/2205.11916  
   “Let’s think step by step” often boosts answer quality. Also helped motivate later work asking whether these steps are genuinely faithful or post-hoc.

3. **Language Models Don’t Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting**  
   **Authors:** Miles Turpin, Julian Michael, Ethan Perez, Samuel Bowman  
   **Year/Venue:** 2023, arXiv  
   **URL:** https://arxiv.org/abs/2305.04388  
   Shows CoT explanations can be systematically unfaithful: models can produce persuasive reasoning traces that do not reflect true decision mechanisms.

4. **Faithful Chain-of-Thought Reasoning**  
   **Authors:** Qing Lyu, Marianna Apidianaki, Xiaodan Zhu, Chris Callison-Burch  
   **Year/Venue:** 2023, arXiv  
   **URL:** https://arxiv.org/abs/2301.13379  
   Proposes approaches to align generated reasoning with executable/verifiable intermediate steps, aiming to improve faithfulness rather than only final accuracy.

5. **Attention is not Explanation** *(faithfulness context for rationale quality)*  
   **Authors:** Sarthak Jain, Byron C. Wallace  
   **Year/Venue:** 2019, NAACL  
   **URL:** https://aclanthology.org/N19-1357/  
   Shows that human-plausible explanatory signals can diverge from true model decision mechanisms, a key conceptual precursor to CoT unfaithfulness findings.

6. **Faithful and Consistent Natural Language Explanations by Learning to Say and Do**  
   **Authors:** Huan Sun et al.  
   **Year/Venue:** 2020, EMNLP  
   **URL:** https://aclanthology.org/2020.emnlp-main.28/  
   Pre-LLM but central for explanation faithfulness: ties textual explanations to executable actions, reducing unsupported rationales.

## Reasoning Reliability: General

1. **GSM8K: Training Verifiers to Solve Math Word Problems**  
   **Authors:** Karl Cobbe et al.  
   **Year/Venue:** 2021, arXiv  
   **URL:** https://arxiv.org/abs/2110.14168  
   Introduced GSM8K and verifier-based workflows. Key for studying reliability gaps between plausible reasoning text and correct outcomes.

2. **Let’s Verify Step by Step**  
   **Authors:** Hunter Lightman et al.  
   **Year/Venue:** 2023, arXiv  
   **URL:** https://arxiv.org/abs/2305.20050  
   Process supervision paper (PRM800K) showing step-level reward signals can improve reasoning reliability beyond outcome-only scoring.

3. **ReAct: Synergizing Reasoning and Acting in Language Models**  
   **Authors:** Shunyu Yao et al.  
   **Year/Venue:** 2023, ICLR  
   **URL:** https://arxiv.org/abs/2210.03629  
   Combines reasoning traces with tool actions; improves verifiability and reduces purely free-form hallucinated reasoning in some tasks.

4. **Tree of Thoughts: Deliberate Problem Solving with Large Language Models**  
   **Authors:** Shunyu Yao et al.  
   **Year/Venue:** 2023, NeurIPS  
   **URL:** https://arxiv.org/abs/2305.10601  
   Uses branching reasoning and search; helpful for consistency because multiple candidate reasoning paths can be compared before committing.

5. **Reflexion: Language Agents with Verbal Reinforcement Learning**  
   **Authors:** Noah Shinn et al.  
   **Year/Venue:** 2023, NeurIPS  
   **URL:** https://arxiv.org/abs/2303.11366  
   Self-critique loop can improve repeatability and reduce repeated reasoning errors, though quality depends on critic faithfulness.

6. **Beyond the Imitation Game: Quantifying and Extrapolating the Capabilities of Language Models**  
   **Authors:** Aarohi Srivastava et al.  
   **Year/Venue:** 2022, arXiv (BIG-bench)  
   **URL:** https://arxiv.org/abs/2206.04615  
   Introduces BIG-bench and shows capability estimates are sensitive to task design and prompting. This is central background for robustness and consistency concerns in reasoning evaluation.

## Mathematical/Arithmetic Consistency

1. **Measuring Mathematical Problem Solving with the MATH Dataset**  
   **Authors:** Dan Hendrycks, Collin Burns, Steven Basart, Andy Zou, Mantas Mazeika, Dawn Song, Jacob Steinhardt  
   **Year/Venue:** 2021, NeurIPS  
   **URL:** https://arxiv.org/abs/2103.03874  
   Hard benchmark for multi-step symbolic reasoning. Exposes inconsistency under small prompt or sampling changes.

2. **GSM8K** (Cobbe et al., 2021) — https://arxiv.org/abs/2110.14168  
   Grade-school math benchmark used extensively to test arithmetic reliability and step-level consistency.

3. **SVAMP: Shuffle & Swap adversarial benchmark for Math Word Problems**  
   **Authors:** Shubham Gupta et al.  
   **Year/Venue:** 2021, AAAI  
   **URL:** https://arxiv.org/abs/2109.07197  
   Demonstrates brittleness under minor perturbations in math word problems, revealing shortcut-based reasoning.

4. **AQuA-RAT: Arithmetic Word Problems with Rationales**  
   **Authors:** Lingpeng Kong et al.  
   **Year/Venue:** 2019, arXiv  
   **URL:** https://arxiv.org/abs/1903.00161  
   Includes rationales for arithmetic QA; useful for analyzing agreement between rationale quality and answer correctness.

5. **Game of 24: Evaluating and Improving Planning and Reasoning of Large Language Models**  
   **Authors:** Shunyu Yao et al.  
   **Year/Venue:** 2023, arXiv  
   **URL:** https://arxiv.org/abs/2305.10601 (ToT includes Game of 24 experiments)  
   Highlights that multi-step mathematical search can reduce random failures compared with single-pass CoT.

## Benchmarks & Datasets

- **TruthfulQA (2022)** — Truthfulness under misconception-prone questions.  
  URL: https://arxiv.org/abs/2109.07958
- **GSM8K (2021)** — Grade-school math reasoning benchmark.  
  URL: https://arxiv.org/abs/2110.14168
- **MATH (2021)** — Competition-level math problems requiring multi-step reasoning.  
  URL: https://arxiv.org/abs/2103.03874
- **SVAMP (2021)** — Adversarial perturbations for math word problems.  
  URL: https://arxiv.org/abs/2109.07197
- **AQuA-RAT (2019)** — Arithmetic QA with rationales.  
  URL: https://arxiv.org/abs/1903.00161
- **ANLI (2020)** — Adversarial NLI with entailment/contradiction emphasis.  
  URL: https://arxiv.org/abs/1910.14599
- **WinoGrande (2020)** — Coreference resolution at scale.  
  URL: https://arxiv.org/abs/1907.10641
- **Winogender (2018)** — Pronoun/coreference consistency and bias diagnostics.  
  URL: https://aclanthology.org/N18-2003/
- **HaluEval (2023)** — Hallucination evaluation across tasks and settings.  
  URL: https://arxiv.org/abs/2305.11747
- **BIG-Bench Hard (2023)** — Hard reasoning subset revealing fragility and inconsistency.  
  URL: https://github.com/suzgunmirac/BIG-Bench-Hard

## Blog Posts & Practitioner Resources

1. **Techniques to Improve Reliability** — OpenAI, 2023  
   URL: https://platform.openai.com/docs/guides/prompt-engineering  
   Practical guidance on prompt decomposition, verification, and sampling strategies that reduce inconsistency in deployed systems.

2. **Process Supervision and PRMs (Let’s Verify Step by Step release context)** — OpenAI, 2023  
   URL: https://arxiv.org/abs/2305.20050  
   Discusses why rewarding intermediate reasoning steps can improve reliability vs pure outcome scoring.

3. **Constitutional AI: Harmlessness from AI Feedback** — Anthropic, 2022  
   URL: https://arxiv.org/abs/2212.08073  
   Not specifically about contradiction, but relevant to consistency of model behavior under varied prompts and self-critique regimes.

4. **Chain-of-Thought Prompting papers + community explainers** — Google Research / Papers with Code entries  
   URL: https://paperswithcode.com/paper/chain-of-thought-prompting-elicits-reasoning  
   Useful practitioner index for tracking methods and replications related to CoT consistency.

5. **Prompting Guide (Self-Consistency, CoT, ToT)** — DAIR.AI Prompt Engineering Guide, ongoing  
   URL: https://www.promptingguide.ai/techniques/consistency  
   Practical catalog of prompting techniques, with implementation templates for consistency-improving decoding.

## GitHub Repos

- **BIG-Bench Hard** — https://github.com/suzgunmirac/BIG-Bench-Hard  
  Hard reasoning evaluations; often used to test robustness/consistency.

- **SelfCheckGPT (implementations/community forks)** — example search entry: https://github.com/potsawee/selfcheckgpt  
  Tools for detecting hallucinations via self-consistency signals.

- **Chain-of-Thought Hub** — https://github.com/FranxYao/chain-of-thought-hub  
  Reproducible prompts and evaluation scripts for reasoning tasks.

- **lm-evaluation-harness** — https://github.com/EleutherAI/lm-evaluation-harness  
  Standard framework for testing consistency/reliability across benchmarks and prompt variants.

- **OpenAI Evals** — https://github.com/openai/evals  
  Evaluation suite including reasoning/factuality-oriented tests and custom eval authoring.

## Key Takeaways

- LLM inconsistency appears at multiple levels: paraphrase changes, sampling randomness, and multi-turn self-contradiction.
- The famous **Self-Consistency** method (Wang et al.) is a *mitigation strategy* (majority vote over reasoning paths), not evidence that the base model is intrinsically consistent.
- Cross-sample disagreement is a useful practical signal for hallucination risk (e.g., SelfCheckGPT).
- Better final-answer accuracy does **not** imply faithful reasoning traces; CoT can be post-hoc or strategically generated (Turpin et al.).
- Process supervision (step-level rewards/verifiers) generally improves reasoning reliability vs outcome-only supervision in math/reasoning settings.
- Math and logical benchmarks reveal strong format sensitivity: small surface changes can produce large answer changes.
- Pronoun/entity resolution and NLI contradiction benchmarks remain important diagnostics for internal belief coherence and logical consistency.
- Shortcut learning/spurious cues are still a major failure mode; models can exploit dataset artifacts rather than robust reasoning.
- Reliable deployment needs *evaluation under perturbation* (paraphrase, reorderings, multi-sample checks), not just single-prompt leaderboard scores.

## BibTeX

```bibtex
@inproceedings{wang2023selfconsistency,
  title={Self-Consistency Improves Chain of Thought Reasoning in Language Models},
  author={Wang, Xuezhi and Wei, Jason and Schuurmans, Dale and Le, Quoc and Chi, Ed and Narang, Sharan and Chowdhery, Aakanksha and Zhou, Denny},
  booktitle={International Conference on Learning Representations (ICLR)},
  year={2023},
  url={https://arxiv.org/abs/2203.11171}
}

@inproceedings{wei2022chain,
  title={Chain-of-Thought Prompting Elicits Reasoning in Large Language Models},
  author={Wei, Jason and Wang, Xuezhi and Schuurmans, Dale and Bosma, Maarten and Xia, Fei and Chi, Ed and Le, Quoc and Zhou, Denny},
  booktitle={Advances in Neural Information Processing Systems (NeurIPS)},
  year={2022},
  url={https://arxiv.org/abs/2201.11903}
}

@inproceedings{kojima2022zeroshot,
  title={Large Language Models are Zero-Shot Reasoners},
  author={Kojima, Takeshi and Gu, Shixiang Shane and Reid, Machel and Matsuo, Yutaka and Iwasawa, Yusuke},
  booktitle={Advances in Neural Information Processing Systems (NeurIPS)},
  year={2022},
  url={https://arxiv.org/abs/2205.11916}
}

@inproceedings{lin2022truthfulqa,
  title={TruthfulQA: Measuring How Models Mimic Human Falsehoods},
  author={Lin, Stephanie and Hilton, Jacob and Evans, Owain},
  booktitle={Proceedings of ACL},
  year={2022},
  url={https://arxiv.org/abs/2109.07958}
}

@inproceedings{manakul2023selfcheckgpt,
  title={SelfCheckGPT: Zero-Resource Black-Box Hallucination Detection for Generative Large Language Models},
  author={Manakul, Potsawee and Liusie, Adian and Gales, Mark},
  booktitle={Findings of EMNLP},
  year={2023},
  url={https://arxiv.org/abs/2303.08896}
}

@inproceedings{turpin2023unfaithful,
  title={Language Models Don't Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting},
  author={Turpin, Miles and Michael, Julian and Perez, Ethan and Bowman, Samuel},
  booktitle={arXiv preprint arXiv:2305.04388},
  year={2023},
  url={https://arxiv.org/abs/2305.04388}
}

@article{lightman2023verify,
  title={Let's Verify Step by Step},
  author={Lightman, Hunter and Kosaraju, Vineet and Burda, Yura and Edwards, Harri and others},
  journal={arXiv preprint arXiv:2305.20050},
  year={2023},
  url={https://arxiv.org/abs/2305.20050}
}

@article{hendrycks2021math,
  title={Measuring Mathematical Problem Solving with the MATH Dataset},
  author={Hendrycks, Dan and Burns, Collin and Basart, Steven and Zou, Andy and Mazeika, Mantas and Song, Dawn and Steinhardt, Jacob},
  journal={NeurIPS},
  year={2021},
  url={https://arxiv.org/abs/2103.03874}
}

@article{cobbe2021gsm8k,
  title={Training Verifiers to Solve Math Word Problems},
  author={Cobbe, Karl and Kosaraju, Vineet and Bavarian, Mohammad and Chen, Mark and Jun, Heewoo and Kaiser, Lukasz and Plappert, Matthias and Tworek, Jerry and Hilton, Jacob and Nakano, Reiichiro and others},
  journal={arXiv preprint arXiv:2110.14168},
  year={2021},
  url={https://arxiv.org/abs/2110.14168}
}

@inproceedings{ribeiro2020checklist,
  title={Beyond Accuracy: Behavioral Testing of NLP Models with CheckList},
  author={Ribeiro, Marco Tulio and Wu, Tongshuang and Guestrin, Carlos and Singh, Sameer},
  booktitle={Proceedings of ACL},
  year={2020},
  url={https://aclanthology.org/2020.acl-main.442/}
}

@inproceedings{zhang2019paws,
  title={PAWS: Paraphrase Adversaries from Word Scrambling},
  author={Zhang, Yuan and Baldridge, Jason and He, Luheng},
  booktitle={Proceedings of NAACL},
  year={2019},
  url={https://aclanthology.org/N19-1382/}
}
```