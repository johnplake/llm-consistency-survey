# GV-Q8: Inference-time compute for reducing generation–validation mismatch

## Scope
Question: *How much can inference-time compute (without retraining) close the generation–validation gap via voting, reranking, search, or critique/debate loops?*

I prioritized quantitative papers and added them to Zotero subcollection:
**`LLM-inconsistency / GV-Inference-time-compute`**.

---

## Papers added to Zotero (10)

1. **Self-Consistency Improves Chain of Thought Reasoning in Language Models** (Wang et al., 2022)  
   - Zotero key: `FA2MV8GU`  
   - Method: multi-sample reasoning + majority vote (self-consistency)

2. **Tree of Thoughts: Deliberate Problem Solving with Large Language Models** (Yao et al., 2023)  
   - Zotero key: `P4CSZPVW`  
   - Method: test-time tree search over thought states

3. **Language Agent Tree Search Unifies Reasoning, Acting, and Planning in Language Models** (Zhou et al., 2023)  
   - Zotero key: `PN3PMAWR`  
   - Method: MCTS-style search for agent trajectories

4. **Training Verifiers to Solve Math Word Problems** (Cobbe et al., 2021)  
   - Zotero key: `JM8XUC93`  
   - Method: generate candidates + verifier rerank/select

5. **Let’s Verify Step by Step** (Lightman et al., 2023)  
   - Zotero key: `D6A3F9EI`  
   - Method: process-level verifier scoring/reranking at inference

6. **Self-Refine: Iterative Refinement with Self-Feedback** (Madaan et al., 2023)  
   - Zotero key: `STUNPD4E`  
   - Method: iterative self-critique and revision loop

7. **Constitutional AI: Harmlessness from AI Feedback** (Bai et al., 2022)  
   - Zotero key: `B9MM52I2`  
   - Method: critique-revision style decoding/evaluation loop (plus training)

8. **Improving Factuality and Reasoning in Language Models through Multiagent Debate** (Du et al., 2023)  
   - Zotero key: `7ZFEBG78`  
   - Method: multi-agent debate + aggregation

9. **Reflexion: Language Agents with Verbal Reinforcement Learning** (Shinn et al., 2023)  
   - Zotero key: `4DW2JUUE`  
   - Method: trial-time self-reflection/critique memory loop

10. **Large Language Monkeys: Scaling Inference Compute with Repeated Sampling** (Brown et al., 2024)  
    - Zotero key: `ICKQRMSG`  
    - Method: repeated sampling / best-of-N scaling laws

All were added with PDF attachments where available (arXiv PDFs attached).

---

## Quantitative takeaways (rough effect sizes reported in papers)

> Note: numbers below are approximate headline effects as reported by each paper; exact values vary by model/task split.

### 1) Voting / self-consistency gives large gains in reasoning tasks
- **Self-Consistency (Wang et al.)** reports substantial improvements over greedy CoT decoding; canonical headline is roughly **+18 points on GSM8K** and sizable gains across SVAMP/AQuA/StrategyQA/ARC-type sets.
- Interpretation for GV mismatch: when generation is noisy but validator is simple (majority answer), extra sampling reduces single-trajectory failure modes.

### 2) Verifier reranking can outperform pure voting when candidate quality is decent
- **Training Verifiers (Cobbe et al.)** and **Let’s Verify Step by Step** show that selecting among many candidates with learned verifiers can produce large jumps versus single-sample generation; improvements are often **double-digit absolute** at fixed base model size when enough candidates are sampled.
- Process-level verifiers (stepwise scoring) generally beat outcome-only checks for hard math reasoning.
- GV lens: stronger validators + candidate diversity reduce mismatch by rejecting plausible-but-wrong traces.

### 3) Search over thoughts/actions yields very large gains on combinatorial tasks
- **Tree of Thoughts** reports dramatic jumps on search-heavy tasks (e.g., Game of 24 from very low single-path success to much higher with branching/search, often cited as near **order-of-magnitude** relative gain).
- **LATS** similarly shows better task success for agentic settings by allocating compute to trajectory exploration and value-guided selection.
- GV lens: search externalizes validation at intermediate states, reducing commitment to early wrong branches.

### 4) Critique/refinement/debate loops improve quality without weight updates
- **Self-Refine** reports broad gains across multiple generation tasks (often **~5–40% relative**, task-dependent).
- **Multiagent Debate** shows improved factuality/reasoning against single-agent baselines, with notable gains on math/QA benchmarks.
- **Reflexion** reports stronger pass rates in coding/decision tasks through iterative self-feedback memory.
- GV lens: these methods repeatedly re-align generator outputs with internal/external checks, shrinking one-shot inconsistency.

### 5) Inference scaling laws: repeated sampling continues to buy performance
- **Large Language Monkeys** supports that simply increasing test-time sampling/selection budget can yield predictable improvements, reinforcing a compute-performance tradeoff even without retraining.
- GV lens: mismatch can be partially “bought down” by compute, though diminishing returns appear and validator quality becomes bottleneck.

---

## Synthesis for the survey question

- **How much gap can be closed without retraining?** Often **a lot** on reasoning-heavy tasks: commonly **double-digit absolute gains** versus single-pass decoding when moving to self-consistency, verifier reranking, or search.
- **Best performers** typically combine:
  1. candidate diversity (N samples / branching), and
  2. nontrivial validation (verifier/process checks/search value).
- **Main limitation:** if validator is weak or correlated with generator errors, extra compute saturates quickly.
- **Practical implication:** inference-time compute is a strong short-run lever for GV mismatch, but long-run gains depend on validator calibration and robustness.

---

## Suggested coding tags for this subquestion

- `inference-time-compute`
- `self-consistency`
- `best-of-n`
- `verifier-reranking`
- `tree-search`
- `debate`
- `self-critique`
- `generation-validation-gap`
