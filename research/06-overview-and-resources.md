# Overview, Existing Taxonomies & Resources

## Existing Survey Papers on LLM Reliability/Consistency

- **A Survey of Large Language Models**  
  **Authors:** Zhao et al.  
  **Year/Venue:** 2023, arXiv  
  **URL:** https://arxiv.org/abs/2303.18223  
  **Summary:** Broad survey of LLM foundations, training, alignment, and evaluation.  
  **Scope:** General LLM landscape; useful umbrella context for consistency discussions.

- **A Survey of Hallucination in Natural Language Generation**  
  **Authors:** Ji et al.  
  **Year/Venue:** 2023, ACM Computing Surveys  
  **URL:** https://arxiv.org/abs/2202.03629  
  **Summary:** Canonical survey of hallucination definitions, causes, and mitigation in NLG systems.  
  **Scope:** Pre-LLM to early-LLM hallucination taxonomy and measurement.

- **A Survey on Hallucination in Large Language Models: Principles, Taxonomy, Challenges, and Open Questions**  
  **Authors:** Huang et al.  
  **Year/Venue:** 2023, arXiv  
  **URL:** https://arxiv.org/abs/2311.05232  
  **Summary:** LLM-specific hallucination survey with expanded taxonomy and mitigation map.  
  **Scope:** Hallucination mechanisms and interventions in instruction-tuned/chat models.

- **Trustworthy Large Language Models: A Survey and Guideline for Evaluating Large Language Models’ Alignment**  
  **Authors:** (commonly cited as Guo et al. / multi-author trustworthy-LLM survey line)  
  **Year/Venue:** 2023–2024, arXiv  
  **URL:** https://arxiv.org/search/?query=trustworthy+large+language+models+survey&searchtype=all  
  **Summary:** Survey family addressing reliability, safety, robustness, and alignment evaluation.  
  **Scope:** Trustworthiness dimensions beyond pure task accuracy.

- **Towards Trustworthy Large Language Models: A Survey**  
  **Authors:** CUI et al. / related trustworthy-LLM survey line  
  **Year/Venue:** 2023, arXiv  
  **URL:** https://arxiv.org/search/?query=towards+trustworthy+large+language+models+a+survey&searchtype=all  
  **Summary:** Synthesizes risks and mitigation practices for dependable deployment.  
  **Scope:** High-level trust framework across ethics, robustness, and reliability.

- **On the Evaluation of Large Language Models**  
  **Authors:** Chang et al.  
  **Year/Venue:** 2024, arXiv  
  **URL:** https://arxiv.org/abs/2307.03109  
  **Summary:** Comprehensive review of LLM evaluation protocols and pitfalls.  
  **Scope:** Benchmark validity, metric mismatch, reproducibility, and dynamic evaluation.

- **Survey of Robustness in NLP** *(representative robustness survey line)*  
  **Authors:** Multiple (e.g., adversarial robustness surveys in NLP)  
  **Year/Venue:** 2020–2024  
  **URL:** https://aclanthology.org/search/?q=robustness+survey+nlp  
  **Summary:** Collectively maps adversarial and distribution-shift fragility in language systems.  
  **Scope:** Robustness techniques directly relevant to consistency under perturbation.

## Existing Taxonomies of Hallucination

- **Ji et al. (2023) taxonomy:** intrinsic vs extrinsic hallucination; model-, data-, and decoding-driven causes — https://arxiv.org/abs/2202.03629
- **Huang et al. (2023) taxonomy:** factuality errors across knowledge boundaries, instruction following, and reasoning chains — https://arxiv.org/abs/2311.05232
- **TruthfulQA framing (Lin et al., 2021):** misconception-consistent vs truth-consistent generations — https://arxiv.org/abs/2109.07958
- **SelfCheckGPT framing (Manakul et al., 2023):** self-consistency divergence as hallucination proxy — https://arxiv.org/abs/2303.08896
- **FActScore framing (Min et al., 2023):** atomic fact precision for long-form outputs — https://arxiv.org/abs/2305.14251
- **HaluEval (Li et al., 2023):** benchmark taxonomy across QA/dialogue/summarization hallucination cases — https://arxiv.org/abs/2305.11747

## Trustworthy AI / Reliable LLM Frameworks

- **HELM (Holistic Evaluation of Language Models)** — Liang et al., 2022, https://arxiv.org/abs/2211.09110  
  Multi-metric framework covering accuracy, calibration, robustness, fairness, and efficiency.

- **TrustLLM** — Huang et al., 2024, https://arxiv.org/abs/2401.05561  
  Benchmark/framework for trustworthiness dimensions (truthfulness, safety, fairness, robustness, privacy, etc.).

- **OpenAI Preparedness Framework** — OpenAI, 2023–2024, https://openai.com/safety  
  Capability/risk-tiered evaluation philosophy for high-impact model release decisions.

- **Anthropic Responsible Scaling Policy (RSP)** — Anthropic, ongoing, https://www.anthropic.com/news  
  Governance + eval framework for capability thresholds and mitigations.

- **DeepMind Frontier Safety Framework** — Google DeepMind, 2025, https://deepmind.google/discover/blog/  
  Structured model risk assessment and deployment controls.

## Evaluation Frameworks & Tools

- **HELM** — https://crfm.stanford.edu/helm/latest/  
  Scenario-based multi-metric LLM evaluation.

- **lm-evaluation-harness (EleutherAI)** — https://github.com/EleutherAI/lm-evaluation-harness  
  Reproducible task suite with standardized prompts/metrics.

- **BIG-bench / BIG-bench Hard** — https://github.com/google/BIG-bench  
  Broad capability stress-testing across many tasks.

- **PromptBench** — https://github.com/microsoft/promptbench  
  Benchmarking prompt robustness and attack sensitivity.

- **OpenAI Evals** — https://github.com/openai/evals  
  Extensible eval framework with custom datasets and model-graded checks.

- **LangChain Benchmarks / LangSmith evals** — https://docs.smith.langchain.com/evaluation  
  Application-level evaluation for LLM pipelines and agents.

- **TruLens** — https://www.trulens.org/  
  LLM app instrumentation with groundedness/relevance feedback functions.

- **DeepEval** — https://github.com/confident-ai/deepeval  
  Unit-test style LLM evaluation (hallucination, answer relevancy, bias tests).

- **Ragas** — https://github.com/explodinggradients/ragas  
  RAG-focused metrics (faithfulness, context precision/recall, answer relevance).

- **lighteval (Hugging Face)** — https://github.com/huggingface/lighteval  
  Fast, modular evaluation pipelines for open models.

- **Inspect (UK AISI)** — https://github.com/UKGovernmentBEIS/inspect_ai  
  Safety and capability eval framework with protocolized tasks.

- **HELM Lite / Stanford CRFM evaluation resources** — https://crfm.stanford.edu/  
  Practical guidance for standardized evaluation setup.

## Key Benchmarks (Cross-Category)

- **TruthfulQA (2021)** — https://arxiv.org/abs/2109.07958 — truthfulness under misconception pressure.
- **MMLU (2020)** — https://arxiv.org/abs/2009.03300 — broad knowledge/MCQ competence.
- **MMLU-Pro (2024)** — https://arxiv.org/abs/2406.01574 — harder, less saturated MMLU variant.
- **BBQ (2021)** — https://arxiv.org/abs/2110.08193 — social bias under ambiguous/disambiguated contexts.
- **HellaSwag (2019)** — https://aclanthology.org/P19-1472/ — adversarial commonsense completion.
- **ARC (2018)** — https://arxiv.org/abs/1803.05457 — science QA reasoning.
- **GSM8K (2021)** — https://arxiv.org/abs/2110.14168 — arithmetic reasoning with chain-of-thought relevance.
- **DROP (2019)** — https://aclanthology.org/N19-1246/ — discrete reasoning over passages.
- **HumanEval (2021)** — https://arxiv.org/abs/2107.03374 — code generation correctness via tests.
- **MBPP (2021)** — https://arxiv.org/abs/2108.07732 — beginner-level coding tasks.
- **SWE-bench (2024)** — https://arxiv.org/abs/2310.06770 — real-world GitHub issue resolution.
- **FActScore (2023)** — https://arxiv.org/abs/2305.14251 — factual precision in long-form generations.
- **SelfCheckGPT (2023)** — https://arxiv.org/abs/2303.08896 — hallucination detection via sample consistency.
- **HaluEval (2023)** — https://arxiv.org/abs/2305.11747 — hallucination benchmark for instruction-following.
- **MT-Bench (2023)** — https://arxiv.org/abs/2306.05685 — multi-turn chat quality; often with LLM judges.
- **Chatbot Arena (2023-)** — https://lmarena.ai/ — live human pairwise preference ranking.

## GitHub Repos (Curated)

- **EleutherAI/lm-evaluation-harness** — https://github.com/EleutherAI/lm-evaluation-harness — canonical open LLM benchmark runner.
- **openai/evals** — https://github.com/openai/evals — general-purpose eval framework.
- **google/BIG-bench** — https://github.com/google/BIG-bench — broad benchmark collection.
- **stanford-crfm/helm** — https://github.com/stanford-crfm/helm — holistic eval implementation.
- **microsoft/promptbench** — https://github.com/microsoft/promptbench — prompt robustness testing.
- **lm-sys/FastChat** — https://github.com/lm-sys/FastChat — MT-Bench and Arena infrastructure.
- **huggingface/lighteval** — https://github.com/huggingface/lighteval — lightweight eval engine.
- **explodinggradients/ragas** — https://github.com/explodinggradients/ragas — RAG eval toolkit.
- **truera/trulens** — https://github.com/truera/trulens — LLM app eval/observability.
- **confident-ai/deepeval** — https://github.com/confident-ai/deepeval — LLM testing framework.
- **stanfordnlp/dspy** — https://github.com/stanfordnlp/dspy — optimization framework with evaluation loops for LM programs.
- **UKGovernmentBEIS/inspect_ai** — https://github.com/UKGovernmentBEIS/inspect_ai — evaluation suite for capability/safety testing.

## Influential Blog Posts & Essays

- **The Leaderboard Illusion** — Sayash Kapoor & Arvind Narayanan, AI Snake Oil, 2024, https://www.aisnakeoil.com/p/the-leaderboard-illusion  
  Why benchmark rankings can be unstable and misleading.

- **AI Snake Oil (ongoing reliability essays)** — Narayanan & Kapoor, https://www.aisnakeoil.com/  
  Strong critique of eval misuse and weak claims.

- **HELM: Holistic Evaluation of Language Models** — Stanford CRFM, 2022, https://crfm.stanford.edu/2022/11/17/helm.html  
  Explains multidimensional evaluation philosophy.

- **LMSYS Chatbot Arena posts** — LMSYS, https://lmsys.org/blog/  
  Method notes for pairwise human preference benchmarking.

- **Anthropic safety/evals posts** — Anthropic News, https://www.anthropic.com/news  
  Frontier model evaluation and policy transparency.

- **OpenAI system cards and safety updates** — OpenAI, https://openai.com/index  
  Practical examples of capability/risk evaluation artifacts.

- **DeepMind blog on responsible AGI and evaluations** — Google DeepMind, https://deepmind.google/discover/blog/  
  Frontier evaluation framing and safeguards.

- **The Gradient (evaluation/reliability essays)** — https://thegradient.pub/  
  Research-explainer articles on model reliability and benchmarking.

- **Interconnects (Nathan Lambert)** — https://www.interconnects.ai/  
  Frequent analysis of eval trends, arenas, and open-model progress.

- **Sebastian Ruder NLP News** — https://newsletter.ruder.io/  
  High-signal curation of new papers/tools, including eval reliability.

- **Bounded Regret (Ethan Mollick-adjacent ecosystem and eval commentary references)** — https://www.boundedregret.com/  
  Practitioner-focused reflections on model behavior and testing.

## Video Talks

- **Holistic Evaluation of Language Models (HELM talk)** — Percy Liang / CRFM, 2022, https://www.youtube.com/results?search_query=Holistic+Evaluation+of+Language+Models+HELM
- **Judging LLM-as-a-Judge / MT-Bench** — LMSYS talks, 2023–2024, https://www.youtube.com/results?search_query=MT-Bench+Chatbot+Arena+talk
- **Trustworthy/Responsible LLMs tutorials (ACL/EMNLP)** — 2023–2025, https://www.youtube.com/results?search_query=ACL+tutorial+trustworthy+LLMs
- **FActScore / factuality evaluation talks** — 2023–2024, https://www.youtube.com/results?search_query=FActScore+LLM+evaluation
- **SWE-bench presentations** — 2024, https://www.youtube.com/results?search_query=SWE-bench+ICLR

## Newsletters & Ongoing Coverage

- **NLP News (Sebastian Ruder)** — https://newsletter.ruder.io/ — weekly research curation.
- **Import AI (Jack Clark)** — https://importai.substack.com/ — policy + technical trend synthesis.
- **The Batch (DeepLearning.AI)** — https://www.deeplearning.ai/the-batch/ — practical AI developments.
- **Interconnects newsletter** — https://www.interconnects.ai/ — eval/open-model ecosystem analysis.
- **AI Snake Oil newsletter** — https://www.aisnakeoil.com/ — critical reliability and deployment analysis.
- **Latent Space newsletter/podcast** — https://www.latent.space/ — practitioner interviews and eval discourse.

## Useful Twitter/X Thread Sources (Researchers to Track)

- **Percy Liang (CRFM)** — https://x.com/percyliang — HELM/benchmark methodology discussions.
- **LMSYS Org** — https://x.com/lmsysorg — arena methodology, ranking caveats, release notes.
- **Andrej Karpathy** — https://x.com/karpathy — practical model behavior/evaluation commentary.
- **Nathan Lambert** — https://x.com/natolambert — open-model benchmarking analysis.
- **Sayash Kapoor** — https://x.com/sayashk — benchmark/AI claims critique threads.
- **Arvind Narayanan** — https://x.com/random_walker — methodological rigor and evaluation skepticism.
- **Yejin Choi** — https://x.com/YejinChoinka — reliability/safety/reasoning commentary.

## Key Takeaways

- The field has many benchmark papers but fewer deeply standardized reliability protocols.
- Hallucination taxonomies are maturing; measurement quality still depends heavily on task and annotation design.
- LLM evaluation is shifting from static single-score leaderboards to multi-metric and dynamic systems.
- LLM-as-judge is useful for scale, but must be audited for position/style/verbosity biases.
- “Trustworthy LLM” frameworks increasingly combine technical metrics with governance/process controls.
- Reproducibility remains fragile without strict reporting of prompts, versions, seeds, and test-time settings.
- For real reliability, teams should combine: benchmark suites + live/user eval + task-grounded execution eval.
- Ongoing blogs/newsletters are now essential because benchmark practice changes faster than formal survey cycles.
