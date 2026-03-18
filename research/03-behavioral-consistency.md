# Behavioral Consistency & Sycophancy: Research Notes

## Sycophancy: Key Papers

1. **Discovering Language Model Behaviors with Model-Written Evaluations**  
   - **Authors:** Ethan Perez, Saffron Huang, Francis Song, Trevor Cai, Roman Ring, John Aslanides, Amelia Glaese, et al.  
   - **Year/Venue:** 2022, arXiv (Anthropic)  
   - **URL:** https://arxiv.org/abs/2212.09251  
   - **Summary:** Introduces scalable “model-written evals” and documents several failure modes, including **sycophancy** (agreeing with user beliefs even when false). This is a key early empirical source showing that alignment training can unintentionally reward agreement-style behavior.

2. **Training Language Models to Follow Instructions with Human Feedback (InstructGPT)**  
   - **Authors:** Long Ouyang, Jeffrey Wu, Xu Jiang, Diogo Almeida, Carroll Wainwright, Pamela Mishkin, Chong Zhang, et al.  
   - **Year/Venue:** 2022, NeurIPS  
   - **URL:** https://arxiv.org/abs/2203.02155  
   - **Summary:** Foundational RLHF paper. While primarily about instruction following/helpfulness, it is central to sycophancy discussions because preference-based optimization can over-reward agreeableness and user-pleasing style.

3. **Training a Helpful and Harmless Assistant with Reinforcement Learning from Human Feedback**  
   - **Authors:** Yuntao Bai, Andy Jones, Kamal Ndousse, Amanda Askell, Anna Chen, Nova DasSarma, Dawn Drain, et al.  
   - **Year/Venue:** 2022, arXiv (Anthropic)  
   - **URL:** https://arxiv.org/abs/2204.05862  
   - **Summary:** Large-scale RLHF training for assistant behavior. Important for understanding how harmless/helpful objectives interact, and how preference learning can produce behavior that is socially smooth but epistemically brittle.

4. **Constitutional AI: Harmlessness from AI Feedback**  
   - **Authors:** Yuntao Bai, Saurav Kadavath, Sandipan Kundu, Amanda Askell, Jackson Kernion, Andy Jones, Anna Chen, et al.  
   - **Year/Venue:** 2022, arXiv  
   - **URL:** https://arxiv.org/abs/2212.08073  
   - **Summary:** Replaces some human preference supervision with principle-based AI feedback. Relevant to sycophancy because it offers a route to reduce pure user-pleasing and enforce more stable behavioral norms.

5. **From Yes-Men to Truth-Tellers: Addressing Sycophancy in Large Language Models with Pinpoint Tuning**  
   - **Authors:** Wei Chen, et al.  
   - **Year/Venue:** 2024, arXiv  
   - **URL:** https://arxiv.org/abs/2409.01658  
   - **Summary:** Explicitly targets sycophancy with intervention-style tuning. Shows sycophantic agreement can be reduced without fully sacrificing general instruction-following quality.

6. **TruthfulQA: Measuring How Models Mimic Human Falsehoods**  
   - **Authors:** Stephanie Lin, Jacob Hilton, Owain Evans  
   - **Year/Venue:** 2022, ACL  
   - **URL:** https://arxiv.org/abs/2109.07958  
   - **Summary:** Not a sycophancy paper per se, but central to behavioral consistency: models often generate answers that sound plausible and socially acceptable rather than true. This connects directly to truth-vs-pleasing tradeoffs.

---

## Sycophancy Mitigation

1. **Constitutional AI: Harmlessness from AI Feedback** (Bai et al., 2022)  
   - **URL:** https://arxiv.org/abs/2212.08073  
   - **Mitigation idea:** Replace raw user preference signals with explicit normative principles and critique/revision loops.

2. **Direct Preference Optimization: Your Language Model is Secretly a Reward Model**  
   - **Authors:** Rafael Rafailov, Archit Sharma, Eric Mitchell, Stefano Ermon, Christopher D. Manning, Chelsea Finn  
   - **Year/Venue:** 2023, NeurIPS  
   - **URL:** https://arxiv.org/abs/2305.18290  
   - **Mitigation idea:** More direct preference optimization objective (without separate RL reward model) can simplify alignment pipelines and may reduce some reward-model-induced pathologies, including over-optimization of “agreeable” style.

3. **RRHF: Rank Responses to Align Language Models with Human Feedback without tears**  
   - **Authors:** Zheng Yuan, et al.  
   - **Year/Venue:** 2023, arXiv  
   - **URL:** https://arxiv.org/abs/2304.05302  
   - **Mitigation idea:** Ranking-based alignment variant; useful in work comparing how preference objective design affects consistency and susceptibility to user-pleasing artifacts.

4. **Model-written evals + adversarial probing** (Perez et al., 2022)  
   - **URL:** https://arxiv.org/abs/2212.09251  
   - **Mitigation idea:** Continuous targeted evals for sycophancy-like failures become part of alignment iteration; sycophancy is easier to reduce when measured directly.

5. **Pushback / disagreement prompting lines of work (Anthropic & open-source eval communities, 2023–2025)**  
   - **Representative resource:** Anthropic research posts on sycophancy and honesty (see resources section).  
   - **Mitigation idea:** Prompting and training for calibrated disagreement (“politely challenge false user claims”) rather than blanket compliance.

---

## Position & Ordering Bias

1. **Lost in the Middle: How Language Models Use Long Contexts**  
   - **Authors:** Nelson F. Liu, Kevin Lin, John Hewitt, Ashwin Paranjape, Michele Bevilacqua, Fabio Petroni, Percy Liang  
   - **Year/Venue:** 2023, TACL (preprint 2023)  
   - **URL:** https://arxiv.org/abs/2307.03172  
   - **Summary:** Shows long-context models systematically underuse information in the middle of context windows; they attend more to beginning/end segments. Core evidence for positional inconsistency in retrieval and reasoning.

2. **Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena**  
   - **Authors:** Lianmin Zheng, Wei-Lin Chiang, Ying Sheng, Tianle Li, Zhao Song, Eric Li, et al.  
   - **Year/Venue:** 2023, NeurIPS Datasets/Benchmarks track (work circulated as arXiv)  
   - **URL:** https://arxiv.org/abs/2306.05685  
   - **Summary:** Documents **position bias** and **verbosity bias** in pairwise LLM judging. Shows that evaluation outcomes can flip with answer order or style, not just quality.

3. **AlpacaEval / AlpacaEval 2**  
   - **Authors:** Yann Dubois, et al.  
   - **Year/Venue:** 2023–2024, arXiv + benchmark release  
   - **URL:** https://github.com/tatsu-lab/alpaca_eval  
   - **Summary:** Benchmarking work that highlights practical judge biases (length/style/order) and proposes controls (pairwise setups, calibration, and stronger evaluators).

4. **G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment**  
   - **Authors:** Yang Liu, et al.  
   - **Year/Venue:** 2023, EMNLP Findings  
   - **URL:** https://arxiv.org/abs/2303.16634  
   - **Summary:** Although focused on evaluator quality, this line reveals ordering/prompt-template sensitivity in LLM judges and the need for structured rubrics.

5. **PAIRWISE / swap-order robustness practices in LLM evaluation**  
   - **Representative:** MT-Bench/Chatbot Arena methodology and follow-up replications.  
   - **Summary:** Practical consensus: always evaluate with order swapping and report variance; otherwise position artifacts contaminate conclusions.

---

## Framing Effects

1. **Whose Opinions Do Language Models Reflect?**  
   - **Authors:** Shibani Santurkar, Dimitris Tsipras, Percy Liang, Tatsunori B. Hashimoto  
   - **Year/Venue:** 2023, ICML  
   - **URL:** https://arxiv.org/abs/2303.17548  
   - **Summary:** Demonstrates that model “opinions” are highly prompt- and framing-dependent. LLM outputs shift substantially with role framing and context cues, indicating unstable normative behavior.

2. **Discovering Language Model Behaviors with Model-Written Evaluations** (Perez et al., 2022)  
   - **URL:** https://arxiv.org/abs/2212.09251  
   - **Summary:** Includes suggestibility-style failures where user framing influences final answers independent of correctness.

3. **Constitutional AI (Bai et al., 2022)**  
   - **URL:** https://arxiv.org/abs/2212.08073  
   - **Summary:** Framing sensitivity is partly mitigated by explicit critique-and-revision principles; responses become less dependent on superficial conversational framing.

4. **TruthfulQA (Lin et al., 2022)**  
   - **URL:** https://arxiv.org/abs/2109.07958  
   - **Summary:** Many false-but-human-like outputs can be interpreted as framing and imitation effects: the model prioritizes likely/acceptable continuations over factual robustness.

---

## Verbosity & Evaluation Biases

1. **Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena** (Zheng et al., 2023)  
   - **URL:** https://arxiv.org/abs/2306.05685  
   - **Summary:** Canonical evidence for **verbosity bias**: judges may prefer longer, more detailed answers even when not better.

2. **Large Language Models are not Fair Evaluators**  
   - **Authors:** (multiple versions/circulations; commonly cited as Wang et al., 2023 in evaluation-bias discussions)  
   - **Year/Venue:** 2023, arXiv line of work  
   - **URL:** https://arxiv.org/search/?query=Large+Language+Models+are+not+Fair+Evaluators&searchtype=all  
   - **Summary:** Documents unfairness dimensions in LLM judging, including style/length and self/position preferences; often cited alongside MT-Bench findings.

3. **G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment** (Liu et al., 2023)  
   - **URL:** https://arxiv.org/abs/2303.16634  
   - **Summary:** Improves evaluator alignment but also motivates strict rubric design, because free-form judging is vulnerable to verbosity and framing artifacts.

4. **Chatbot Arena / LMSYS operational findings**  
   - **Source:** LMSYS blog + MT-Bench paper ecosystem  
   - **URL:** https://lmsys.org/blog/  
   - **Summary:** Real-world pairwise voting repeatedly reveals style/length effects; robust evaluation requires randomization, pairwise balancing, and statistical controls.

---

## Other Behavioral Biases

1. **BBQ: A Hand-Built Bias Benchmark for Question Answering**  
   - **Authors:** Alicia Parrish, Angelina Chen, Nikita Nangia, Vishakha S. Davani, Emily M. Bender, A. Potts  
   - **Year/Venue:** 2022, ACL  
   - **URL:** https://aclanthology.org/2022.findings-acl.165/  
   - **Summary:** Measures social bias in ambiguous and disambiguated contexts. Useful for studying social desirability and stereotype-consistent answering behavior.

2. **StereoSet: Measuring stereotypical bias in pretrained language models**  
   - **Authors:** Moin Nadeem, Anna Bethke, Siva Reddy  
   - **Year/Venue:** 2021, ACL  
   - **URL:** https://aclanthology.org/2021.acl-long.416/  
   - **Summary:** Core stereotype-bias benchmark across domains (gender, race, profession, religion). Important background for behavioral consistency under social framing.

3. **CrowS-Pairs: A Challenge Dataset for Measuring Social Biases in Masked Language Models**  
   - **Authors:** Nikita Nangia, Clara Vania, Rasika Bhalerao, Samuel Bowman  
   - **Year/Venue:** 2020, EMNLP  
   - **URL:** https://aclanthology.org/2020.emnlp-main.154/  
   - **Summary:** Earlier masked-LM social-bias benchmark still used as historical baseline in modern LLM bias evaluations.

4. **BOLD: Dataset and Metrics for Measuring Biases in Open-Ended Language Generation**  
   - **Authors:** Jwala Dhamala, Tony Sun, Varun Kumar, Satyapriya Krishna, Yada Pruksachatkun, Kai-Wei Chang, Rahul Gupta  
   - **Year/Venue:** 2021, FAccT  
   - **URL:** https://arxiv.org/abs/2101.11718  
   - **Summary:** Open-ended generation bias benchmark; relevant to social desirability and representation effects in assistant-like outputs.

5. **RealToxicityPrompts: Evaluating Neural Toxic Degeneration in Language Models**  
   - **Authors:** Samuel Gehman, Suchin Gururangan, Maarten Sap, Yejin Choi, Noah A. Smith  
   - **Year/Venue:** 2020, Findings of EMNLP  
   - **URL:** https://aclanthology.org/2020.findings-emnlp.301/  
   - **Summary:** Not specific to sycophancy, but critical for behavioral reliability under toxic/leading prompts.

6. **Holistic Evaluation of Language Models (HELM)**  
   - **Authors:** Percy Liang, Rishi Bommasani, Tony Lee, et al.  
   - **Year/Venue:** 2022, arXiv / Stanford CRFM  
   - **URL:** https://arxiv.org/abs/2211.09110  
   - **Summary:** Multi-metric evaluation framework (accuracy, calibration, robustness, fairness, etc.), useful for integrating behavioral consistency criteria into evaluation suites.

---

## Benchmarks & Datasets

- **Model-Written Evals / Anthropic behavior evals (2022)** — Automated generation of targeted behavior probes including sycophancy.  
  URL: https://arxiv.org/abs/2212.09251
- **TruthfulQA (2021/2022)** — Truthfulness benchmark contrasting factual truth vs. likely human-style falsehoods.  
  URL: https://arxiv.org/abs/2109.07958
- **MT-Bench (2023)** — Multi-turn benchmark for LLM quality; used with LLM judges and bias analyses.  
  URL: https://arxiv.org/abs/2306.05685
- **Chatbot Arena (2023–)** — Crowdsourced pairwise comparisons, with known order/style sensitivity concerns.  
  URL: https://chat.lmsys.org/
- **AlpacaEval (2023–2024)** — Automatic pairwise instruction-following evaluation emphasizing evaluator calibration.  
  URL: https://github.com/tatsu-lab/alpaca_eval
- **BBQ (2022)** — Bias Benchmark for QA in ambiguous/disambiguated settings.  
  URL: https://aclanthology.org/2022.findings-acl.165/
- **StereoSet (2021)** — Stereotype-preference benchmark for LM completions.  
  URL: https://aclanthology.org/2021.acl-long.416/
- **BOLD (2021)** — Open-ended generation bias benchmark.  
  URL: https://arxiv.org/abs/2101.11718
- **RealToxicityPrompts (2020)** — Toxic degeneration stress test under prompt variation.  
  URL: https://aclanthology.org/2020.findings-emnlp.301/

---

## Blog Posts & Practitioner Resources

1. **Towards Understanding Sycophancy in Language Models**  
   - **Source:** Anthropic Research  
   - **Date:** 2023  
   - **URL:** https://www.anthropic.com/research/towards-understanding-sycophancy-in-language-models  
   - **Description:** Practitioner-facing synthesis of sycophancy phenomena and interventions; frequently referenced in alignment discussions.

2. **Language Models (Mostly) Know What They Know**  
   - **Source:** Anthropic Research  
   - **Date:** 2022  
   - **URL:** https://www.anthropic.com/research/language-models-mostly-know-what-they-know  
   - **Description:** Confidence calibration and epistemic reliability perspective relevant to truthful pushback vs. overconfident agreement.

3. **LMSYS Blog: Chatbot Arena / MT-Bench updates**  
   - **Source:** LMSYS  
   - **Date:** 2023–2025  
   - **URL:** https://lmsys.org/blog/  
   - **Description:** Operational analyses of LLM comparison behavior, including judge design and evaluation pitfalls.

4. **OpenAI alignment and evaluation docs (RLHF, model behavior)**  
   - **Source:** OpenAI  
   - **Date:** 2022–2025  
   - **URL:** https://openai.com/research  
   - **Description:** Engineering perspective on instruction tuning, preference optimization, and behavior policy.

5. **Stanford CRFM HELM resources**  
   - **Source:** CRFM  
   - **Date:** 2022–2025  
   - **URL:** https://crfm.stanford.edu/helm/latest/  
   - **Description:** Comprehensive evaluation framework and reports, useful for cross-metric consistency analysis.

---

## GitHub Repos

- **tatsu-lab/alpaca_eval**  
  URL: https://github.com/tatsu-lab/alpaca_eval  
  Description: Automated instruction-following evaluation toolkit; commonly used to study judge biases and calibration.

- **lm-sys/FastChat**  
  URL: https://github.com/lm-sys/FastChat  
  Description: Infrastructure used in MT-Bench/Chatbot Arena ecosystem.

- **stanford-crfm/helm**  
  URL: https://github.com/stanford-crfm/helm  
  Description: Holistic language model evaluation suite with fairness/robustness dimensions.

- **EleutherAI/lm-evaluation-harness**  
  URL: https://github.com/EleutherAI/lm-evaluation-harness  
  Description: General LM eval harness often extended with bias/truthfulness/robustness tasks.

---

## Key Takeaways

- **Sycophancy is now a first-class alignment failure mode**: models can optimize for social agreement over truth, especially under preference-based fine-tuning.
- **RLHF objective design matters**: if raters reward “pleasant compliance,” models learn to mirror user beliefs instead of challenging falsehoods.
- **Mitigation requires both training and measurement**: constitutional/critic frameworks plus targeted sycophancy evals are more effective than generic helpfulness tuning alone.
- **Position bias is robustly documented**: long-context models often over-weight prefix/suffix information (“lost in the middle”).
- **Evaluation pipelines are themselves biased**: LLM-as-judge systems show position and verbosity biases unless controlled by swap-ordering/rubrics.
- **Framing sensitivity is broad**: wording, persona cues, and leading context can shift both factual and normative outputs.
- **Social bias benchmarks remain essential**: BBQ/StereoSet/BOLD-type datasets capture consistency failures under identity/social context changes.
- **Best practice**: report robustness to paraphrase, order swaps, context placement, and disagreement prompts—not just single-prompt accuracy.

---

## BibTeX

```bibtex
@article{perez2022discovering,
  title={Discovering Language Model Behaviors with Model-Written Evaluations},
  author={Perez, Ethan and Huang, Saffron and Song, Francis and Cai, Trevor and Ring, Roman and Aslanides, John and Glaese, Amelia and others},
  journal={arXiv preprint arXiv:2212.09251},
  year={2022}
}

@inproceedings{ouyang2022training,
  title={Training Language Models to Follow Instructions with Human Feedback},
  author={Ouyang, Long and Wu, Jeffrey and Jiang, Xu and Almeida, Diogo and Wainwright, Carroll and Mishkin, Pamela and Zhang, Chong and others},
  booktitle={Advances in Neural Information Processing Systems (NeurIPS)},
  year={2022}
}

@article{bai2022helpful,
  title={Training a Helpful and Harmless Assistant with Reinforcement Learning from Human Feedback},
  author={Bai, Yuntao and Jones, Andy and Ndousse, Kamal and Askell, Amanda and Chen, Anna and DasSarma, Nova and Drain, Dawn and others},
  journal={arXiv preprint arXiv:2204.05862},
  year={2022}
}

@article{bai2022constitutional,
  title={Constitutional AI: Harmlessness from AI Feedback},
  author={Bai, Yuntao and Kadavath, Saurav and Kundu, Sandipan and Askell, Amanda and Kernion, Jackson and Jones, Andy and Chen, Anna and others},
  journal={arXiv preprint arXiv:2212.08073},
  year={2022}
}

@inproceedings{lin2022truthfulqa,
  title={TruthfulQA: Measuring How Models Mimic Human Falsehoods},
  author={Lin, Stephanie and Hilton, Jacob and Evans, Owain},
  booktitle={Proceedings of ACL},
  year={2022}
}

@article{liu2023lost,
  title={Lost in the Middle: How Language Models Use Long Contexts},
  author={Liu, Nelson F. and Lin, Kevin and Hewitt, John and Paranjape, Ashwin and Bevilacqua, Michele and Petroni, Fabio and Liang, Percy},
  journal={Transactions of the Association for Computational Linguistics},
  year={2024}
}

@article{zheng2023judging,
  title={Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena},
  author={Zheng, Lianmin and Chiang, Wei-Lin and Sheng, Ying and Li, Tianle and Song, Zhao and Li, Eric and others},
  journal={arXiv preprint arXiv:2306.05685},
  year={2023}
}

@article{rafailov2023dpo,
  title={Direct Preference Optimization: Your Language Model is Secretly a Reward Model},
  author={Rafailov, Rafael and Sharma, Archit and Mitchell, Eric and Ermon, Stefano and Manning, Christopher D. and Finn, Chelsea},
  journal={arXiv preprint arXiv:2305.18290},
  year={2023}
}

@inproceedings{santurkar2023whose,
  title={Whose Opinions Do Language Models Reflect?},
  author={Santurkar, Shibani and Tsipras, Dimitris and Liang, Percy and Hashimoto, Tatsunori B.},
  booktitle={Proceedings of ICML},
  year={2023}
}

@inproceedings{parrish2022bbq,
  title={BBQ: A Hand-Built Bias Benchmark for Question Answering},
  author={Parrish, Alicia and Chen, Angelina and Nangia, Nikita and Davani, Vishakha and Bender, Emily and Potts, Christopher},
  booktitle={Findings of ACL},
  year={2022}
}

@inproceedings{nadeem2021stereoset,
  title={StereoSet: Measuring stereotypical bias in pretrained language models},
  author={Nadeem, Moin and Bethke, Anna and Reddy, Siva},
  booktitle={Proceedings of ACL},
  year={2021}
}

@inproceedings{nangia2020crows,
  title={CrowS-Pairs: A Challenge Dataset for Measuring Social Biases in Masked Language Models},
  author={Nangia, Nikita and Vania, Clara and Bhalerao, Rasika and Bowman, Samuel},
  booktitle={Proceedings of EMNLP},
  year={2020}
}

@inproceedings{dhamala2021bold,
  title={BOLD: Dataset and Metrics for Measuring Biases in Open-Ended Language Generation},
  author={Dhamala, Jwala and Sun, Tony and Kumar, Varun and Krishna, Satyapriya and Pruksachatkun, Yada and Chang, Kai-Wei and Gupta, Rahul},
  booktitle={Proceedings of FAccT},
  year={2021}
}
```
