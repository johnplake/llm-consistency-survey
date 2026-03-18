# Benchmark Reliability: Research Notes

## Data Contamination

- **Language Models are Few-Shot Learners**  
  **Authors:** Brown et al. (OpenAI)  
  **Year/Venue:** 2020, NeurIPS  
  **URL:** https://arxiv.org/abs/2005.14165  
  **Summary:** GPT-3 explicitly discusses benchmark contamination checks and overlap analysis as a threat to valid evaluation. The paper helped establish contamination auditing as a standard part of modern LLM evaluation reporting.

- **The Pile: An 800GB Dataset of Diverse Text for Language Modeling**  
  **Authors:** Gao et al.  
  **Year/Venue:** 2020, arXiv  
  **URL:** https://arxiv.org/abs/2101.00027  
  **Summary:** Introduces a large pretraining corpus and documents dataset construction issues relevant to contamination. Demonstrates how benchmark leakage risk scales with broad web-scale data aggregation.

- **Documenting Large Webtext Corpora: A Case Study on the Colossal Clean Crawled Corpus (C4)**  
  **Authors:** Dodge et al.  
  **Year/Venue:** 2021, EMNLP  
  **URL:** https://aclanthology.org/2021.emnlp-main.98/  
  **Summary:** Shows hidden properties and biases in large corpora used in pretraining. While not only about benchmark contamination, it highlights provenance and filtering limitations that make leakage hard to rule out.

- **Deduplicating Training Data Makes Language Models Better**  
  **Authors:** Lee et al.  
  **Year/Venue:** 2022, ACL  
  **URL:** https://aclanthology.org/2022.acl-long.577/  
  **Summary:** Demonstrates that near-duplicate memorization harms model quality and can inflate benchmark-like pattern matching. Supports deduplication as both quality and reliability intervention.

- **Quantifying Memorization Across Neural Language Models**  
  **Authors:** Carlini et al.  
  **Year/Venue:** 2023, ICLR  
  **URL:** https://openreview.net/forum?id=TatRHT_1cK  
  **Summary:** Measures memorization in language models and provides methodology for extraction risk analysis. Relevant to contamination because benchmark items present in pretraining can be memorized rather than reasoned.

- **Do Models Explain Themselves? Counterfactual Simulatability of Natural Language Explanations** *(contamination-adjacent reliability warning)*  
  **Authors:** Wiegreffe et al.  
  **Year/Venue:** 2022, ACL  
  **URL:** https://aclanthology.org/2022.acl-long.44/  
  **Summary:** Not a contamination paper per se, but important for reliability: apparent benchmark success can arise from spurious shortcuts. Helps frame why leakage and shortcut learning can be hard to distinguish.

## Prompt Sensitivity in Evaluation

- **Holistic Evaluation of Language Models (HELM)**  
  **Authors:** Liang et al.  
  **Year/Venue:** 2022, arXiv/CRFM  
  **URL:** https://arxiv.org/abs/2211.09110  
  **Summary:** Introduces standardized scenarios and emphasizes that results vary substantially with prompting choices and metrics. HELM formalized robustness and calibration dimensions beyond single-score reporting.

- **Beyond the Imitation Game Benchmark (BIG-bench)**  
  **Authors:** Srivastava et al.  
  **Year/Venue:** 2022, TMLR  
  **URL:** https://arxiv.org/abs/2206.04615  
  **Summary:** Massive benchmark showing high variance across task formats and prompting. Highlights that aggregate rankings can obscure instability at task-level.

- **Fantastically Ordered Prompts and Where to Find Them**  
  **Authors:** Lu et al.  
  **Year/Venue:** 2022, ACL  
  **URL:** https://aclanthology.org/2022.acl-long.556/  
  **Summary:** Shows that prompt/example ordering strongly affects in-context learning accuracy. This directly threatens reproducibility when benchmark prompts are not fully specified.

- **On the Stability of In-Context Learning**  
  **Authors:** Zhao et al.  
  **Year/Venue:** 2021, arXiv  
  **URL:** https://arxiv.org/abs/2108.04041  
  **Summary:** Demonstrates dramatic variance from demonstration selection and order. Suggests multi-seed/multi-prompt reporting is necessary for stable model comparison.

- **MMLU-Pro: A More Robust and Challenging Multi-Task Language Understanding Benchmark**  
  **Authors:** Wang et al.  
  **Year/Venue:** 2024, arXiv  
  **URL:** https://arxiv.org/abs/2406.01574  
  **Summary:** Built partly as a response to saturation and prompt brittleness in MMLU-style evaluation. Uses harder, cleaner items to improve discriminative reliability.

## LLM-as-Judge Issues

- **Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena**  
  **Authors:** Zheng et al.  
  **Year/Venue:** 2023, NeurIPS Datasets and Benchmarks  
  **URL:** https://arxiv.org/abs/2306.05685  
  **Summary:** Popularized LLM-as-judge methodology but also documents biases and disagreement with humans. Shows pairwise protocols reduce (but do not eliminate) grading artifacts.

- **G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment**  
  **Authors:** Liu et al.  
  **Year/Venue:** 2023, EMNLP  
  **URL:** https://arxiv.org/abs/2303.16634  
  **Summary:** Demonstrates strong correlation with human judgments for some generation tasks. Also reveals dependence on rubric and prompt design, raising consistency concerns for leaderboard use.

- **Large Language Models are not Fair Evaluators**  
  **Authors:** Wang et al.  
  **Year/Venue:** 2023, arXiv  
  **URL:** https://arxiv.org/abs/2305.17926  
  **Summary:** Finds systematic evaluator bias related to style, verbosity, and position. Important evidence that LLM judges can encode non-task factors into scores.

- **Position Bias in LLM-as-a-Judge**  
  **Authors:** (multiple follow-up studies; e.g., PandaLM and later audits)  
  **Year/Venue:** 2023–2025, arXiv/ACL workshops  
  **URL:** https://arxiv.org/search/?query=position+bias+LLM+judge&searchtype=all  
  **Summary:** A recurring finding across papers: candidate order affects preferences, even under symmetric prompts. Practical mitigation includes order randomization and bidirectional scoring.

## Multiple-Choice & Format Biases

- **Measuring Massive Multitask Language Understanding (MMLU)**  
  **Authors:** Hendrycks et al.  
  **Year/Venue:** 2020, ICLR  
  **URL:** https://arxiv.org/abs/2009.03300  
  **Summary:** Core MCQ benchmark widely used for frontier model ranking. Subsequent work has shown option-order, answer-letter priors, and formatting differences can materially affect scores.

- **TruthfulQA: Measuring How Models Mimic Human Falsehoods**  
  **Authors:** Lin, Hilton, Evans  
  **Year/Venue:** 2021, ACL  
  **URL:** https://arxiv.org/abs/2109.07958  
  **Summary:** Includes both multiple-choice and generation settings, exposing dependence on evaluation mode. Helps illustrate how format choices can change measured “truthfulness.”

- **A Survey of Multiple Choice Question Answering in NLP** *(background methodology reference)*  
  **Authors:** Rogers et al. (survey-style resources vary by subfield)  
  **Year/Venue:** 2019–2023  
  **URL:** https://aclanthology.org/search/?q=multiple+choice+question+answering+survey  
  **Summary:** Broader MCQ QA literature documents option artifacts and annotation biases that continue in LLM-era benchmarks.

- **HellaSwag: Can a Machine Really Finish Your Sentence?**  
  **Authors:** Zellers et al.  
  **Year/Venue:** 2019, ACL  
  **URL:** https://aclanthology.org/P19-1472/  
  **Summary:** Classic example of adversarial filtering to reduce superficial artifacts in multiple-choice style evaluation. Useful baseline for understanding format-induced shortcuting.

## Leaderboard & Reproducibility

- **Dynabench: Rethinking Benchmarking in NLP**  
  **Authors:** Kiela et al.  
  **Year/Venue:** 2021, NAACL  
  **URL:** https://aclanthology.org/2021.naacl-main.324/  
  **Summary:** Argues static leaderboards quickly become stale and gameable. Proposes dynamic human-and-model-in-the-loop benchmarking to reduce overfitting to fixed test sets.

- **Holistic Evaluation of Language Models (HELM)**  
  **Authors:** Liang et al.  
  **Year/Venue:** 2022, arXiv/CRFM  
  **URL:** https://arxiv.org/abs/2211.09110  
  **Summary:** Strong reproducibility contribution: standardized settings, multi-metric reporting, and explicit scenario metadata. Shows that single-number leaderboards are insufficient for robust model comparison.

- **EleutherAI Language Model Evaluation Harness**  
  **Authors:** Gao et al. (project maintainers)  
  **Year/Venue:** ongoing  
  **URL:** https://github.com/EleutherAI/lm-evaluation-harness  
  **Summary:** Widely used reproducible framework for benchmark runs and exact prompt templates. Still sensitive to versioning, tokenizer choices, and task implementation details.

- **Chatbot Arena / LMSYS Leaderboard**  
  **Authors:** LMSYS Org  
  **Year/Venue:** ongoing  
  **URL:** https://lmarena.ai/  
  **Summary:** Pairwise human preferences give higher ecological validity than static QA benchmarks, but rankings can move with matchup sampling, judge composition, and prompt distribution shifts.

- **Open LLM Leaderboard (Hugging Face)**  
  **Authors:** Hugging Face + community  
  **Year/Venue:** ongoing  
  **URL:** https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard  
  **Summary:** Valuable for transparent open-model comparison, but illustrates ranking instability across benchmark suites and prompt/eval versions.

- **GPQA: A Graduate-Level Google-Proof Q&A Benchmark**  
  **Authors:** Rein et al.  
  **Year/Venue:** 2023, arXiv  
  **URL:** https://arxiv.org/abs/2311.12022  
  **Summary:** Developed because earlier benchmarks were saturating. A clear case of “ceiling effects” forcing new benchmark design to preserve discrimination.

- **SWE-bench: Can Language Models Resolve Real-World GitHub Issues?**  
  **Authors:** Jimenez et al.  
  **Year/Venue:** 2024, ICLR  
  **URL:** https://arxiv.org/abs/2310.06770  
  **Summary:** Moves evaluation toward harder, execution-grounded tasks after text-only benchmark saturation. Shows reliability gains from realistic environments.

## Key Benchmarks for Studying Evaluation

- **HELM (2022):** broad multi-scenario evaluation with calibration/robustness metrics — https://crfm.stanford.edu/helm/latest/
- **BIG-bench (2022):** diverse task suite exposing distributional brittleness — https://github.com/google/BIG-bench
- **MMLU (2020):** broad MCQ knowledge benchmark; strong but saturation-prone — https://arxiv.org/abs/2009.03300
- **MMLU-Pro (2024):** harder MMLU successor addressing contamination/saturation concerns — https://arxiv.org/abs/2406.01574
- **TruthfulQA (2021):** factuality under misconception priors — https://arxiv.org/abs/2109.07958
- **BBQ (2021):** bias benchmark with controlled social dimensions — https://arxiv.org/abs/2110.08193
- **GSM8K (2021):** grade-school math reasoning, now partially saturated for top models — https://arxiv.org/abs/2110.14168
- **HumanEval (2021):** code synthesis with unit tests; vulnerable to contamination concerns — https://arxiv.org/abs/2107.03374
- **MBPP (2021):** Python programming benchmark — https://arxiv.org/abs/2108.07732
- **SWE-bench (2024):** repo-grounded software engineering tasks — https://www.swebench.com/
- **Chatbot Arena (2023-):** live pairwise preference ranking — https://lmarena.ai/
- **Open LLM Leaderboard:** community leaderboard over standardized task set — https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard

## Blog Posts & Resources

- **The Leaderboard Illusion** — Sayash Kapoor & Arvind Narayanan, 2024, https://www.aisnakeoil.com/ (essay on benchmark/leaderboard misinterpretation and Goodhart pressure).
- **HELM launch posts (CRFM)** — Stanford CRFM blog, 2022, https://crfm.stanford.edu/ (why multi-metric holistic evaluation matters).
- **LMSYS Arena methodology posts** — LMSYS blog/docs, 2023–2025, https://lmsys.org/blog/ (pairwise human eval strengths and limitations).
- **Hugging Face Open LLM Leaderboard docs** — Hugging Face, ongoing, https://huggingface.co/docs/leaderboards/open_llm_leaderboard/about (evaluation versioning and caveats).
- **Anthropic model evaluations and safety reports** — Anthropic, ongoing, https://www.anthropic.com/news (documents benchmark limitations and eval evolution).

## Key Takeaways

- Benchmark contamination risk is structural in web-scale pretraining and cannot be dismissed without explicit overlap audits.
- Prompt templates, demonstration order, and decoding settings can change absolute scores and sometimes model rankings.
- Multiple-choice evaluation remains artifact-prone (option order, answer priors, formatting effects), so robustness checks are necessary.
- LLM-as-judge is useful but biased; positional/verbosity effects require randomized, bidirectional, rubric-controlled protocols.
- Static leaderboards are vulnerable to Goodhart’s Law: optimizing to benchmark specifics can outpace real capability gains.
- Reproducible evaluation requires versioned prompts, exact model identifiers, seeds, and full run metadata.
- Saturation is now common (e.g., older QA/math/code sets), motivating harder, dynamic, and more realistic benchmarks.
- Reliable model assessment increasingly needs portfolio evaluation: static tests + interactive human preference + task-grounded execution.

## BibTeX

```bibtex
@inproceedings{brown2020gpt3,
  title={Language Models are Few-Shot Learners},
  author={Brown, Tom and Mann, Benjamin and Ryder, Nick and et al.},
  booktitle={NeurIPS},
  year={2020},
  url={https://arxiv.org/abs/2005.14165}
}

@article{liang2022helm,
  title={Holistic Evaluation of Language Models},
  author={Liang, Percy and Bommasani, Rishi and Lee, Tony and et al.},
  journal={arXiv preprint arXiv:2211.09110},
  year={2022},
  url={https://arxiv.org/abs/2211.09110}
}

@article{srivastava2022bigbench,
  title={Beyond the Imitation Game: Quantifying and Extrapolating the Capabilities of Language Models},
  author={Srivastava, Aarohi and Rastogi, Abhishek and Rao, Abhishek and et al.},
  journal={Transactions on Machine Learning Research},
  year={2022},
  url={https://arxiv.org/abs/2206.04615}
}

@inproceedings{lu2022fantastically,
  title={Fantastically Ordered Prompts and Where to Find Them},
  author={Lu, Yao and Bartolo, Max and Moore, Alistair and et al.},
  booktitle={ACL},
  year={2022},
  url={https://aclanthology.org/2022.acl-long.556/}
}

@article{zheng2023judging,
  title={Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena},
  author={Zheng, Lianmin and Chiang, Wei-Lin and Sheng, Ying and et al.},
  journal={arXiv preprint arXiv:2306.05685},
  year={2023},
  url={https://arxiv.org/abs/2306.05685}
}

@article{liu2023geval,
  title={G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment},
  author={Liu, Yang and Iter, Dan and Xu, Yichong and et al.},
  journal={arXiv preprint arXiv:2303.16634},
  year={2023},
  url={https://arxiv.org/abs/2303.16634}
}

@article{wang2023notfair,
  title={Large Language Models are not Fair Evaluators},
  author={Wang, X. and et al.},
  journal={arXiv preprint arXiv:2305.17926},
  year={2023},
  url={https://arxiv.org/abs/2305.17926}
}

@inproceedings{kiela2021dynabench,
  title={Dynabench: Rethinking Benchmarking in NLP},
  author={Kiela, Douwe and Bartolo, Max and Nie, Yixin and et al.},
  booktitle={NAACL},
  year={2021},
  url={https://aclanthology.org/2021.naacl-main.324/}
}

@article{rein2023gpqa,
  title={GPQA: A Graduate-Level Google-Proof Q\&A Benchmark},
  author={Rein, David and et al.},
  journal={arXiv preprint arXiv:2311.12022},
  year={2023},
  url={https://arxiv.org/abs/2311.12022}
}

@article{jimenez2023swebench,
  title={SWE-bench: Can Language Models Resolve Real-World GitHub Issues?},
  author={Jimenez, Carlos and Yang, John and Wettig, Alexander and et al.},
  journal={arXiv preprint arXiv:2310.06770},
  year={2023},
  url={https://arxiv.org/abs/2310.06770}
}
```