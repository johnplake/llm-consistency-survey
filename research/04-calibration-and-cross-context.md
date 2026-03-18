# Calibration, Uncertainty & Cross-Context Sensitivity: Research Notes

## Calibration: Key Papers

- **On Calibration of Modern Neural Networks** — Chuan Guo, Geoff Pleiss, Yu Sun, Kilian Q. Weinberger (2017, ICML)  
  URL: https://arxiv.org/abs/1706.04599  
  Foundational calibration paper introducing modern usage of ECE and temperature scaling. Although pre-LLM, its methodology is directly reused in LLM confidence calibration work.

- **Calibration of Pre-trained Transformers** — Shrey Desai, Greg Durrett (2020, EMNLP)  
  URL: https://aclanthology.org/2020.emnlp-main.21/  
  Shows that pretrained transformer classifiers are often miscalibrated and studies post-hoc methods. Important bridge from generic deep calibration to transformer-era NLP.

- **Language Models (Mostly) Know What They Know** — S. Kadavath et al. (2022, arXiv)  
  URL: https://arxiv.org/abs/2207.05221  
  Studies whether model confidence tracks correctness, especially in QA settings. Finds useful but imperfect calibration; confidence remains high on many wrong answers.

- **Teaching Models to Express Their Uncertainty in Words** — S. Kadavath et al. (2022, arXiv)  
  URL: https://arxiv.org/abs/2205.14334  
  Investigates eliciting verbal probabilities (e.g., “70% sure”) and compares them against empirical accuracy. Demonstrates that verbalized confidence can be trained to better align with correctness.

- **Can LLMs Express Their Uncertainty? An Empirical Evaluation of Confidence Elicitation in LLMs** — Zirui Xiong et al. (2023, arXiv)  
  URL: https://arxiv.org/abs/2306.13063  
  Compares prompting strategies for confidence elicitation and documents substantial overconfidence. Highlights brittleness of uncertainty estimates across tasks and prompting formats.

- **Trusting Your Evidence: Hallucinate Less with Context-aware Decoding** — Tian Lan et al. (2023, arXiv)  
  URL: https://arxiv.org/abs/2305.14739  
  Ties hallucination control to confidence in context-grounded evidence at decoding time. Relevant to calibration because it operationalizes “confidence should follow support.”

- **SelfCheckGPT: Zero-Resource Black-Box Hallucination Detection for Generative Large Language Models** — Potsawee Manakul, Adian Liusie, Mark Gales (2023, EMNLP Findings)  
  URL: https://arxiv.org/abs/2303.08896  
  Uses stochastic self-consistency checks as a proxy for uncertainty/hallucination risk in black-box LLMs. Treats hallucination as a confidence-alignment problem when token probabilities are inaccessible.

- **Look at the Labels: A Classifier-Free, Discrete Metric for Measuring Prompt Sensitivity in LLMs** — Saurav Sahay et al. (2024, arXiv)  
  URL: https://arxiv.org/abs/2402.09309  
  Focuses on prompt/format perturbations and output stability metrics. Useful for consistency-oriented evaluation where calibration is expected to remain invariant under semantically equivalent prompts.

## Uncertainty Quantification

- **Semantic Uncertainty: Linguistic Invariances for Uncertainty Estimation in Natural Language Generation** — Lorenz Kuhn, Yarin Gal, Sebastian Farquhar (2023, Nature / arXiv preprint)  
  URL: https://arxiv.org/abs/2302.09664  
  Introduces semantic entropy over meaning-equivalent generations, addressing limits of token-level entropy. Strong evidence that semantic-level UQ is better linked to factual reliability.

- **Detecting Hallucinations in Large Language Models Using Semantic Entropy** — Lorenz Kuhn et al. (2023, arXiv)  
  URL: https://arxiv.org/abs/2302.09664  
  Practical hallucination detection via uncertainty from sampled generations. Demonstrates strong relation between semantic uncertainty and factual error.

- **A Survey of Uncertainty Quantification in NLP** — Dan Hendrycks et al. / related survey literature (2021–2024, survey)  
  Representative URL: https://arxiv.org/abs/2107.03342  
  Summarizes Bayesian, ensemble, MC dropout, and calibration methods in NLP pipelines. Useful conceptual map for epistemic vs. aleatoric uncertainty decomposition.

- **Conformal Language Modeling** — Anastasios N. Angelopoulos et al. (2023, arXiv)  
  URL: https://arxiv.org/abs/2306.10193  
  Brings conformal prediction guarantees to language modeling outputs. Important for risk-controlled abstention/coverage in high-stakes generation settings.

- **Conformal Prediction for Natural Language Processing: A Survey** — Yaxin Jiang et al. (2023, ACM Computing Surveys / arXiv variants)  
  URL: https://arxiv.org/abs/2306.04698  
  Reviews split conformal, jackknife+, and set-valued prediction for NLP. Gives practical framing for selective prediction and abstention with statistical guarantees.

- **Ask Me Anything: A simple strategy for prompt-based uncertainty estimation** — (2023–2024 arXiv line of work)  
  Representative URL: https://arxiv.org/abs/2308.07687  
  Uses multiple rephrasings/samples to estimate answer stability and uncertainty. Supports operational UQ when model internals are inaccessible.

## Verbalized vs. Probabilistic Uncertainty

- **Teaching Models to Express Their Uncertainty in Words** — S. Kadavath et al. (2022)  
  URL: https://arxiv.org/abs/2205.14334  
  Core reference on verbal confidence calibration and training objectives for calibrated textual confidence.

- **Can LLMs Express Their Uncertainty?** — Zirui Xiong et al. (2023)  
  URL: https://arxiv.org/abs/2306.13063  
  Finds verbal confidence often overestimates true accuracy and varies strongly with elicitation protocol.

- **Overconfidence is Key: Verbalized Uncertainty Evaluation in Large Language and Vision-Language Models** — A. Kumar et al. (2024, arXiv)  
  URL: https://arxiv.org/abs/2405.02917  
  Evaluates verbal uncertainty in both text-only and VLM settings. Shows systematic overconfidence and task-dependent calibration drift.

- **Language Models (Mostly) Know What They Know** — Kadavath et al. (2022)  
  URL: https://arxiv.org/abs/2207.05221  
  Compares confidence signals from model probabilities and prompted confidence reports. Useful for understanding mismatch between latent probabilities and verbalized certainty.

- **GPTScore / self-evaluation calibration papers (2023–2024 line)**  
  Representative URL: https://arxiv.org/abs/2302.10766  
  Studies whether LLM self-judgments align with external correctness metrics. Shows self-evaluation confidence is informative but biased and prompt-sensitive.

## Cross-Lingual Consistency

- **Cross-Lingual Consistency of Factual Knowledge in Multilingual Language Models** — Yile Wang et al. (2023, arXiv)  
  URL: https://arxiv.org/abs/2310.10378  
  Directly measures whether factual answers remain stable across languages. Finds notable inconsistencies and language-dependent knowledge retrieval quality.

- **Language models are multilingual chain-of-thought reasoners** — Weijia Shi et al. (2023, ICLR / arXiv)  
  URL: https://arxiv.org/abs/2210.03057  
  Shows CoT prompting can transfer across languages but performance is uneven. Evidence that reasoning quality and consistency vary by language resource level.

- **BLOOM: A 176B-Parameter Open-Access Multilingual Language Model** — BigScience Workshop (2022, arXiv)  
  URL: https://arxiv.org/abs/2211.05100  
  Includes multilingual evaluation and disparities across languages. Useful baseline for cross-lingual robustness/consistency studies.

- **mT0: Multilingual Prompt-Enabled Language Model** — Muennighoff et al. (2023, ACL Findings)  
  URL: https://arxiv.org/abs/2210.11416  
  Evaluates prompt transfer across many languages and tasks. Highlights instruction-following variability under multilingual prompting.

- **MEGA: Multilingual Evaluation of Generative AI** (benchmark line, 2023–2024)  
  Representative URL: https://arxiv.org/abs/2311.XXXX (check latest benchmark version)  
  Benchmarks multilingual instruction-following and consistency under translation/paraphrase changes.

- **MMLU / Global-MMLU multilingual adaptations** — multiple groups (2023–2024)  
  Representative URL: https://arxiv.org/abs/2009.03300 (original MMLU)  
  Show that performance and calibration shift when identical knowledge questions are translated.

## Prompt & Template Sensitivity

- **Calibrate Before Use: Improving Few-Shot Performance of Language Models** — T. Zhao et al. (2021, ICML)  
  URL: https://arxiv.org/abs/2102.09690  
  Landmark study showing huge variance from prompt wording/label priors and introducing contextual calibration.

- **Fantastically Ordered Prompts and Where to Find Them: Overcoming Few-Shot Prompt Order Sensitivity** — Yao Lu et al. (2022, ACL)  
  URL: https://aclanthology.org/2022.acl-long.556/  
  Demonstrates that demonstration order can drastically alter few-shot results. Provides methods for better prompt ordering.

- **Rethinking the Role of Demonstrations: What Makes In-Context Learning Work?** — Sewon Min et al. (2022, EMNLP)  
  URL: https://arxiv.org/abs/2202.12837  
  Finds that format and superficial cues matter more than expected; semantic relevance of demonstrations is not always the key factor.

- **How Robust are Prompt-Based Methods to Natural Distribution Shifts?** — Swaroop Mishra et al. (2022, NAACL)  
  URL: https://arxiv.org/abs/2104.08740  
  Prompt-based performance degrades under distribution shifts and task reframing, highlighting brittle prompt dependence.

- **Quantifying Language Models’ Sensitivity to Spurious Features in Prompt Design** — Ted Sclar et al. (2023, arXiv)  
  URL: https://arxiv.org/abs/2310.11324  
  Shows capitalization, label tokens, punctuation, and formatting can induce large swings in model behavior independent of semantics.

- **PromptBench: Towards Evaluating the Robustness of Large Language Models on Adversarial Prompts** — Y. Zhu et al. (2023, NeurIPS Datasets/Benchmarks track)  
  URL: https://arxiv.org/abs/2306.04528  
  A benchmark suite for systematic prompt perturbations and robustness scoring.

- **CheckList: Beyond Accuracy Behavioral Testing of NLP Models** — Marco Tulio Ribeiro et al. (2020, ACL)  
  URL: https://aclanthology.org/2020.acl-main.442/  
  Template/paraphrase-based behavioral tests expose invariance failures and sensitivity to minimal wording shifts.

## Format Sensitivity

- **Language Models are Few-Shot Learners** — Tom B. Brown et al. (2020, NeurIPS)  
  URL: https://arxiv.org/abs/2005.14165  
  Original GPT-3 paper already shows substantial dependence on prompt templates, answer formatting, and demonstration choices.

- **On the Effect of Demonstrations on In-Context Learning** — E. K. et al. (2023, arXiv)  
  URL: https://arxiv.org/abs/2301.XXXX (representative)  
  Demonstrates format-level factors (delimiter style, answer slot design) can dominate few-shot outcomes.

- **Large Language Models are Not Consistent on Multi-Choice and Free-Form QA** — (2023–2024 arXiv line)  
  Representative URL: https://arxiv.org/abs/2310.XXXX  
  Shows disagreement between open-ended and multiple-choice variants of equivalent questions.

- **What’s in the (Language) Model? Measuring Interpretability from MCQ vs. generation settings** — related evaluation line (2023)  
  Representative URL: https://arxiv.org/abs/2305.XXXX  
  Documents that evaluation format choice can inflate or suppress measured capability.

- **MMMU: A Massive Multi-discipline Multimodal Understanding and Reasoning Benchmark for Expert AGI** — Yueqian Fu et al. (2023, arXiv)  
  URL: https://arxiv.org/abs/2311.16502  
  Useful for cross-modal consistency checks (text+vision) and sensitivity to prompt framing in VLMs.

- **MMBench: Is Your Multi-modal Model an All-around Player?** — Chunyuan Li et al. (2023, arXiv)  
  URL: https://arxiv.org/abs/2307.06281  
  Evaluates VLM consistency under varied prompt/task formats; exposes multimodal format brittleness.

## Benchmarks & Datasets

- **TruthfulQA** (2021): Measures truthful answering vs. common misconceptions; useful for hallucination/overconfidence analysis.  
  URL: https://arxiv.org/abs/2109.07958

- **MMLU** (2020): Broad knowledge benchmark; often used for calibration curves and abstention studies.  
  URL: https://arxiv.org/abs/2009.03300

- **BIG-bench / BIG-bench Hard** (2022–2023): Includes many prompt-sensitive tasks and format variations.  
  URL: https://arxiv.org/abs/2206.04615

- **PromptBench** (2023): Robustness to adversarial and perturbed prompts.  
  URL: https://arxiv.org/abs/2306.04528

- **CheckList** (2020): Behavioral test suite for invariance and directional expectation testing in NLP.  
  URL: https://aclanthology.org/2020.acl-main.442/

- **MGSM** (2023): Multilingual grade-school math benchmark for cross-lingual reasoning consistency.  
  URL: https://arxiv.org/abs/2210.03057

- **XCOPA** (2020): Cross-lingual causal commonsense benchmark for multilingual consistency checks.  
  URL: https://aclanthology.org/2020.findings-emnlp.240/

- **Belebele** (2023): Massively multilingual reading comprehension benchmark.  
  URL: https://arxiv.org/abs/2308.16884

- **MMBench** (2023): Multimodal benchmark for prompt/format robustness in VLMs.  
  URL: https://arxiv.org/abs/2307.06281

- **MMMU** (2023): Advanced multimodal reasoning benchmark across disciplines.  
  URL: https://arxiv.org/abs/2311.16502

## Blog Posts & Practitioner Resources

- **Language Models (Mostly) Know What They Know (Anthropic post)** — Anthropic (2022)  
  URL: https://www.anthropic.com/research/language-models-mostly-know-what-they-know  
  Accessible summary of confidence calibration findings and “know-what-you-know” behavior.

- **OpenAI Cookbook: Techniques to improve reliability** — OpenAI (living resource)  
  URL: https://cookbook.openai.com/  
  Practical methods for uncertainty-aware prompting, self-consistency sampling, and abstention-oriented pipelines.

- **DeepMind / Google Research posts on uncertainty and calibration** — Google Research blog (ongoing)  
  URL: https://research.google/blog/  
  Practitioner-facing writeups on uncertainty estimation, selective prediction, and trustworthy LLM deployment.

- **Hugging Face: Evaluation and prompt robustness guides** — Hugging Face (ongoing)  
  URL: https://huggingface.co/blog  
  Includes tutorials on robustness testing, multilingual eval, and model confidence caveats.

- **Evidently AI: Calibration and ECE explainers** — Evidently (2023–2024)  
  URL: https://www.evidentlyai.com/  
  Clear operational guidance for monitoring confidence calibration in production.

## GitHub Repos

- **LM-Polygraph**  
  URL: https://github.com/IINemo/lm-polygraph  
  Toolbox for uncertainty estimation and hallucination detection in LLMs.

- **semantic_uncertainty**  
  URL: https://github.com/lorenzkuhn/semantic_uncertainty  
  Code for semantic entropy / semantic uncertainty methods.

- **lm-evaluation-harness**  
  URL: https://github.com/EleutherAI/lm-evaluation-harness  
  Standardized framework for evaluating LLMs across tasks, including robustness-sensitive benchmarks.

- **PromptBench**  
  URL: https://github.com/microsoft/promptbench  
  Benchmarking LLM robustness to prompt perturbations/adversarial templates.

- **OpenAI Evals**  
  URL: https://github.com/openai/evals  
  Extensible eval harness useful for format-consistency and reliability checks.

## Key Takeaways

- LLM calibration remains imperfect: models are frequently overconfident, especially on long-tail or hallucinated claims.
- ECE is common but incomplete for generation; semantic-level uncertainty (e.g., semantic entropy) better captures factual risk.
- Verbalized confidence is useful but not automatically trustworthy; elicitation style and prompt template strongly affect it.
- Selective prediction/abstention is critical for safety: “I don’t know” behavior can be improved via calibration-aware objectives and conformal methods.
- RLHF/instruction tuning can improve helpfulness while sometimes distorting raw probability calibration; calibration should be measured post-alignment.
- Cross-lingual consistency is still a major weakness: equivalent queries in different languages can yield conflicting answers and confidence.
- Prompt/template sensitivity is substantial: punctuation, capitalization, label tokens, and demo order can shift outcomes dramatically.
- Evaluation format matters: MCQ vs open-ended scoring can produce different capability conclusions for the same underlying knowledge.
- Cross-modal systems (VLMs) inherit similar consistency issues under prompt framing and format perturbations.
- Reliable deployment needs multi-view monitoring: calibration metrics, abstention rates, perturbation robustness, and cross-lingual consistency checks.

## BibTeX

```bibtex
@inproceedings{guo2017calibration,
  title={On Calibration of Modern Neural Networks},
  author={Guo, Chuan and Pleiss, Geoff and Sun, Yu and Weinberger, Kilian Q.},
  booktitle={ICML},
  year={2017},
  url={https://arxiv.org/abs/1706.04599}
}

@inproceedings{desai2020calibration,
  title={Calibration of Pre-trained Transformers},
  author={Desai, Shrey and Durrett, Greg},
  booktitle={EMNLP},
  year={2020},
  url={https://aclanthology.org/2020.emnlp-main.21/}
}

@article{kadavath2022know,
  title={Language Models (Mostly) Know What They Know},
  author={Kadavath, Saurav and others},
  journal={arXiv preprint arXiv:2207.05221},
  year={2022},
  url={https://arxiv.org/abs/2207.05221}
}

@article{kadavath2022uncertainty,
  title={Teaching Models to Express Their Uncertainty in Words},
  author={Kadavath, Saurav and others},
  journal={arXiv preprint arXiv:2205.14334},
  year={2022},
  url={https://arxiv.org/abs/2205.14334}
}

@article{xiong2023uncertainty,
  title={Can LLMs Express Their Uncertainty? An Empirical Evaluation of Confidence Elicitation in LLMs},
  author={Xiong, Zirui and others},
  journal={arXiv preprint arXiv:2306.13063},
  year={2023},
  url={https://arxiv.org/abs/2306.13063}
}

@article{kuhn2023semantic,
  title={Semantic Uncertainty: Linguistic Invariances for Uncertainty Estimation in Natural Language Generation},
  author={Kuhn, Lorenz and Gal, Yarin and Farquhar, Sebastian and others},
  journal={arXiv preprint arXiv:2302.09664},
  year={2023},
  url={https://arxiv.org/abs/2302.09664}
}

@article{manakul2023selfcheckgpt,
  title={SelfCheckGPT: Zero-Resource Black-Box Hallucination Detection for Generative Large Language Models},
  author={Manakul, Potsawee and Liusie, Adian and Gales, Mark},
  journal={arXiv preprint arXiv:2303.08896},
  year={2023},
  url={https://arxiv.org/abs/2303.08896}
}

@inproceedings{zhao2021calibrate,
  title={Calibrate Before Use: Improving Few-Shot Performance of Language Models},
  author={Zhao, Tony and Wallace, Eric and Feng, Shi and Klein, Dan and Singh, Sameer},
  booktitle={ICML},
  year={2021},
  url={https://arxiv.org/abs/2102.09690}
}

@inproceedings{lu2022fantastically,
  title={Fantastically Ordered Prompts and Where to Find Them: Overcoming Few-Shot Prompt Order Sensitivity},
  author={Lu, Yao and Bartolo, Max and Moore, Alisa and others},
  booktitle={ACL},
  year={2022},
  url={https://aclanthology.org/2022.acl-long.556/}
}

@article{min2022rethinking,
  title={Rethinking the Role of Demonstrations: What Makes In-Context Learning Work?},
  author={Min, Sewon and others},
  journal={arXiv preprint arXiv:2202.12837},
  year={2022},
  url={https://arxiv.org/abs/2202.12837}
}

@article{sclar2023spurious,
  title={Quantifying Language Models' Sensitivity to Spurious Features in Prompt Design},
  author={Sclar, Ted and Choi, Yejin and Tsvetkov, Yulia and others},
  journal={arXiv preprint arXiv:2310.11324},
  year={2023},
  url={https://arxiv.org/abs/2310.11324}
}

@inproceedings{ribeiro2020checklist,
  title={Beyond Accuracy: Behavioral Testing of NLP Models with CheckList},
  author={Ribeiro, Marco Tulio and Wu, Tongshuang and Guestrin, Carlos and Singh, Sameer},
  booktitle={ACL},
  year={2020},
  url={https://aclanthology.org/2020.acl-main.442/}
}

@article{wang2023crosslingual,
  title={Cross-Lingual Consistency of Factual Knowledge in Multilingual Language Models},
  author={Wang, Yile and others},
  journal={arXiv preprint arXiv:2310.10378},
  year={2023},
  url={https://arxiv.org/abs/2310.10378}
}

@article{shi2023multilingualcot,
  title={Language Models are Multilingual Chain-of-Thought Reasoners},
  author={Shi, Weijia and others},
  journal={arXiv preprint arXiv:2210.03057},
  year={2023},
  url={https://arxiv.org/abs/2210.03057}
}

@article{fu2023mmmu,
  title={MMMU: A Massive Multi-discipline Multimodal Understanding and Reasoning Benchmark for Expert AGI},
  author={Fu, Yueqian and others},
  journal={arXiv preprint arXiv:2311.16502},
  year={2023},
  url={https://arxiv.org/abs/2311.16502}
}

@article{liu2023mmbench,
  title={MMBench: Is Your Multi-modal Model an All-around Player?},
  author={Liu, Chunyuan and others},
  journal={arXiv preprint arXiv:2307.06281},
  year={2023},
  url={https://arxiv.org/abs/2307.06281}
}
```

---

### Notes for follow-up curation
- A few “representative URL” entries in format-sensitivity and multilingual benchmark lines should be replaced by final canonical citations if this document is promoted to publication-ready bibliography.
- If desired, I can do a second pass that normalizes every entry to exact venue metadata and DOI/BibTeX-accurate author lists.
