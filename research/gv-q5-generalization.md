# GV Q5 — Generalization Across Tasks / Domains / Scales

## Scope
Focus: transfer/generalization evidence for generator–validator (or sample-then-rank/verify) methods.
Collection target: `LLM-inconsistency / GV-Generalization`.

## Papers added to Zotero subcollection
Added **12** high-relevance papers (all with PDFs already attached in Zotero):
- RankAlign (Rodriguez et al., 2025)
- Benchmarking and Improving Generator-Validator Consistency (Li et al., 2023)
- LLMs Cannot Self-Correct Reasoning Yet (Huang et al., 2023)
- LLMs are Better Reasoners with Self-Verification (Weng et al., 2022)
- Self-Consistency Improves CoT (Wang et al., 2022)
- Training Verifiers to Solve Math Word Problems (Cobbe et al., 2021)
- Let’s Verify Step by Step (Lightman et al., 2023)
- Math-Shepherd (Wang et al., 2023)
- Chain-of-Verification (Dhuliawala et al., 2023)
- RankGen (Krishna & Wieting, 2022)
- LLM-Blender (Jiang et al., 2023)
- Solving Math Word Problems with Process- and Outcome-Based Feedback (Uesato et al., 2022)

---

## Method × transfer setting × outcome

| Paper / method | Transfer setting tested | Tasks/domains & model scale | Outcome | Where transfer fails / weakens |
|---|---|---|---|---|
| **RankAlign (2025)** rank-based generator–validator alignment | Train on subset settings, test across unseen benchmarks/models | Multiple LLMs and benchmarks; explicit cross-model/cross-task ranking perspective | Partial transfer of ranking signal; improves alignment metrics in-distribution | OOD shift leaves residual misranking; gains are uneven across benchmark families and model scales |
| **Benchmarking & Improving GV Consistency (2023)** | Evaluate consistency under diverse prompt/eval regimes | Broad LM benchmarks; multiple prompting conditions | Consistency can be improved with eval design/interventions | Part of “gap” is artifact-sensitive; transfer across prompt/interface regimes is brittle |
| **Training Verifiers (2021)** best-of-N + verifier | Verifier trained on one distribution used to rerank sampled solutions | GSM8K-style math reasoning; GPT-era model sizes | Strong gains over generator-only via reranking | Verifier overfits style/format; cross-domain transfer outside similar math distributions degrades |
| **Let’s Verify Step by Step (2023)** process reward model (PRM) | Step-level reward model applied to new problem instances / decoders | Math reasoning (PRM800K, MATH-like settings), large models | PRM generalizes better than pure outcome-only scoring in many settings | Transfer drops when reasoning style shifts; step labels can be noisy/OOD-sensitive |
| **Uesato et al. (2022)** process vs outcome feedback | Compare process-supervised vs outcome-supervised transfer | Math word problems; several model scales | Process feedback usually more robust under shift than outcome-only | Still weak under larger distribution shift; annotation quality bottlenecks transfer |
| **Math-Shepherd (2023)** synthetic process verification | Human-free/synthetic verifier signals transferred to new tasks | Math reasoning, open LLMs | Scalable gains from verifier-guided reinforcement | Synthetic labels propagate bias; transfer to very different domains remains limited |
| **Self-Consistency (2022)** sample-many then vote | Transfer of voting heuristic across reasoning tasks | GSM8K, SVAMP, AQuA, StrategyQA, ARC-style reasoning; large LMs | Consistent boosts across many reasoning datasets | Gains shrink when sampled traces are correlated/wrong for same reason; not true verifier learning |
| **Self-Verification (2022)** generate then check | Prompted verification transferred across datasets | Arithmetic/commonsense-style reasoning, few model sizes | Often better than single-pass CoT | Same-model verifier inherits generator errors; weak OOD reliability |
| **LLMs Cannot Self-Correct (2023)** intrinsic self-critique loop | Self-correction across tasks without external new signal | Multiple reasoning benchmarks and LLMs | Minimal/negative transfer for intrinsic self-correction | Strong failure mode: same-model critiques do not generalize reliably and can degrade correct answers |
| **Chain-of-Verification (2023)** explicit verify steps for factual QA | Verification prompting transferred across QA contexts | Factual QA / hallucination reduction settings | Improves factuality on many QA-style tasks | Transfer weaker for complex multi-hop/knowledge-sparse cases; verifier depends on available evidence |
| **RankGen (2022)** LM reranker | Train reranker on one corpus style, apply to generation tasks | Open-ended text generation/reranking | Better selection than likelihood-only decoding | Cross-domain stylistic shift reduces ranking quality |
| **LLM-Blender (2023)** pairwise rank + fusion | Transfer across base model families and benchmarks | Multi-model ensembling across tasks | Robust aggregate improvements from ranking/fusion | Gains depend on candidate diversity and calibration; weak when models share same blind spots |

---

## Cross-paper synthesis (Q5)

### What generalizes reasonably well
- **Inference-time selection heuristics** (self-consistency, reranking, ensembling) often transfer across related tasks without retraining.
- **Process-aware validation** tends to transfer better than outcome-only scoring in math/reasoning.
- **Relative ranking signals** are often more portable than absolute correctness scoring.

### Main transfer bottlenecks
- **Domain shift** (math -> factual QA -> open-ended generation) causes verifier/ranker drift.
- **Scale shift** (validator and generator at different capability levels) can invert or flatten ranking quality.
- **Shared-model bias** in self-verification/self-correction leads to correlated failures.
- **Interface/prompt artifacts** can masquerade as “generalization gains,” then disappear under changed evaluation design.

### Practical implication
For GV closure methods, transfer is strongest when:
1. Candidate pool is diverse,
2. Validation signal is process-aware,
3. Validator is externally grounded or at least architecturally decoupled from generator,
4. Evaluation is stress-tested across prompt/interface variants.

Otherwise, apparent closure often remains in-distribution only.
