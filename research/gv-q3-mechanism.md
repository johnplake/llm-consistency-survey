# GV-Q3: Mechanism — why generator/validator disagreement happens at representation level

## Scope
This note focuses on *mechanistic* explanations for why the same LLM can:
- fail to generate a correct answer, yet
- succeed at discriminating/validating among candidate answers.

I prioritize papers about latent beliefs, representation probing, prompt-framing state shifts, and logit/decoding geometry. I exclude broad interpretability work not clearly tied to generation-vs-validation mismatch.

## Papers added to Zotero collection
Target collection: **LLM-inconsistency / GV-Mechanism**

Added (9 items, all with PDFs attached):
1. **Language Models (Mostly) Know What They Know** (2022) — arXiv:2207.05221
2. **Discovering Latent Knowledge in Language Models Without Supervision** (2022) — arXiv:2212.03827
3. **The Internal State of an LLM Knows When It’s Lying** (2023) — arXiv:2304.13734
4. **Language Models Don’t Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting** (2023) — arXiv:2305.04388
5. **Towards Understanding Sycophancy in Language Models** (2023) — arXiv:2310.13548
6. **Representation Engineering: A Top-Down Approach to AI Transparency** (2023) — arXiv:2310.01405
7. **Tuned Lens: An Interpretability Tool for Language Models** (2023) — arXiv:2303.08112
8. **DoLa: Decoding by Contrasting Layers Improves Factuality in Large Language Models** (2023) — arXiv:2309.03883
9. **RankAlign: A Ranking View of the Generator-Validator Gap in Large Language Models** (2025) — arXiv:2502.11674

---

## Mechanistic synthesis

### 1) Latent-knowledge / readout mismatch
**Core claim:** the model’s hidden state may encode the right proposition, but default generation readout fails to surface it.

- **Kadavath et al. (2022)**: confidence estimates (e.g., p(True)-style probing) reveal substantial metaknowledge not always reflected in first-pass text generation.
- **Burns et al. (2022)**: unsupervised methods can recover latent truth signals from representations, again showing hidden-state information > direct generation quality.
- **Azaria & Mitchell (2023)**: internal states carry reliable “lying vs truth” cues even when outputs are deceptive/incorrect.

**Why this yields GV gap:** validation tasks are effectively *easier readout problems* (binary/relative judgment over provided candidates), while free generation is a harder sequence-synthesis problem with more opportunities for drift.

---

### 2) Prompt framing changes internal operating point (state conditioning)
**Core claim:** different prompt roles (answer vs judge, assistant vs critic, agreeable vs skeptical framing) push activations into different regions; this can expose or suppress truthful features.

- **Turpin et al. (2023)**: CoT text can be unfaithful to underlying decision process; verbalized reasoning is not always a faithful window into internal computation.
- **Perez et al. / Anthropic (2023, sycophancy)**: user-opinion framing can shift outputs toward agreement over truth, implying representation-level control features for social alignment vs factuality.
- **Representation Engineering (Zou et al., 2023)**: linear feature directions can be extracted/steered (e.g., honesty-related traits), supporting a geometric view of state-dependent behavior.

**Why this yields GV gap:** generator prompts often induce “helpful/agreeable continuation” trajectories; validator prompts induce “discriminative/critical” trajectories that may better align with latent truth features.

---

### 3) Logit geometry and decoding-path effects
**Core claim:** the final-token distribution and decoding dynamics can hide useful intermediate evidence present in earlier/lower layers.

- **Tuned Lens (Belrose et al., 2023)**: interpretable layerwise readouts show evolving token beliefs across depth.
- **DoLa (Chuang et al., 2023)**: contrasting layers at decode time improves factuality, indicating that standard final-layer decoding can underutilize earlier factual signals.

**Why this yields GV gap:** generation depends on a brittle sequential decoding path and local argmax/sampling choices, while validation reduces to comparative scoring where latent evidence can dominate more directly.

---

### 4) Ranking objective as bridge (alignment evidence)
**Core claim:** if generation and validation share a ranking structure, training or inference that enforces this common ranking can reduce mismatch.

- **RankAlign (Rodriguez et al., 2025)** provides direct evidence that a ranking perspective narrows the generator-validator gap.

**Interpretation:** this suggests disagreement is not only “knowledge absence,” but also an *objective/readout misalignment* between generative decoding and discriminative scoring.

---

## Working mechanistic picture
A compact model of GV disagreement:
1. **Representation contains partial truth signal** (latent belief).
2. **Prompt framing selects subspace** (helpful/sycophantic vs critical/verification mode).
3. **Readout/decoding amplifies different features** (sequence continuation pressures vs candidate comparison).
4. **Training objective mismatch** leaves these pathways insufficiently aligned.

Hence, a model can “know + detect” better than it can “freely produce.”

---

## Open questions (high-priority)
1. **Shared subspace test:** Are generator and validator decisions linearly decodable from the same latent truth direction, or partially disjoint directions?
2. **Causal intervention:** If we steer honesty/truth directions during generation, does validation improve proportionally (and vice versa)?
3. **Layer localization:** At which layers does disagreement emerge most strongly—knowledge encoding, reasoning composition, or final LM-head projection?
4. **Prompt-invariance metric:** Can we define a representation-level consistency score invariant across answer-vs-judge prompt templates?
5. **Decoding vs representation decomposition:** How much GV gap is due to decoding algorithm (sampling/beam/logit transforms) versus latent state differences?
6. **Alignment transfer:** Do rank-based alignment methods (RankAlign-like) produce measurable increases in representational overlap between generation and validation circuits?
7. **OOD robustness:** Does overlap persist under adversarial framing, multilingual prompts, and long-context interference?

---

## Practical implications for the survey
- Treat GV mismatch as a **mechanism-level readout and objective alignment problem**, not just “hallucination.”
- Evaluate methods along three axes:
  1) latent truth recoverability,
  2) prompt-framing stability,
  3) decoding/readout alignment.
- Rank-based and representation-aware interventions are promising because they explicitly target where the mismatch seems to originate.
