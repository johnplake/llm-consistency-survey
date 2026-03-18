# RankAlign Follow-up Map

Based on RankAlign (Rodriguez et al., COLM 2025), likely next questions and related papers:

## What the authors would likely want to find out next

1. **Mechanism:** Why exactly does generator–validator disagreement happen at representation level?
2. **Directionality:** When should we align generator to validator vs validator to generator?
3. **Generalization:** Does rank-based alignment transfer across tasks, domains, and model scales?
4. **Evaluation design:** How much of the measured gap is true inconsistency vs task-demand/interface artifact?
5. **Training targets:** Are pairwise ranking losses sufficient, or do we need process supervision and verifier traces?
6. **Inference-time compute:** How much can voting/reranking/search close the gap without retraining?
7. **Judge reliability:** Can validators themselves be trusted/calibrated across settings?

## Papers added to Zotero subcollection

Subcollection: **LLM-inconsistency / RankAlign-followups**

- RankAlign: A Ranking View of the Generator-Validator Gap in Large Language Models (Rodriguez et al., 2025)
- Benchmarking and Improving Generator-Validator Consistency of Language Models (Xiang Lisa Li et al., 2023)
- Large Language Models Cannot Self-Correct Reasoning Yet (Huang et al., 2023)
- Large Language Models are Better Reasoners with Self-Verification (Weng, Lu, Hu et al., 2022)
- Self-Consistency Improves Chain of Thought Reasoning in Language Models (Wang et al., 2022)
- Training Verifiers to Solve Math Word Problems (Cobbe et al., 2021)
- Let’s Verify Step by Step (Lightman et al., 2023)
- Math-Shepherd: Verify and Reinforce LLMs Step-by-step without Human Annotations (2023)
- Chain-of-Verification Reduces Hallucination in Large Language Models (Dhuliawala et al., 2023)
- G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment (Liu et al., 2023)
- RankGen: Improving Text Generation with Large Ranking Models (Krishna et al., 2023)
- LLM-Blender: Ensembling Large Language Models with Pairwise Ranking and Generative Fusion (Jiang et al., 2023)
- Auxiliary task demands mask the capabilities of smaller language models (Hu & Frank, 2024)
