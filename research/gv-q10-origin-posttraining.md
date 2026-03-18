# GV-Q10: Origin of the generator-validator gap and post-training effects

Date: 2026-03-18  
Collection: `LLM-inconsistency / GV-Origin-and-posttraining` (`Z5B4DIE3`)

## Scope
Question: where does the generator-validator (GV) gap come from, and how is it changed by instruction tuning / RLHF / post-training objectives?

Focus areas:
1. **Pretraining data/objective effects** (imitation of text distribution vs truth-conditional behavior)
2. **Calibration/readout mismatch** (latent knowledge not stably surfaced in free generation)
3. **Post-training shifts** (SFT, RLHF/RLAIF, DPO, verifier/process supervision)

Excluded: broad alignment papers without direct relevance to inconsistency or generator-vs-validator mismatch.

## Papers added (13; all with PDFs)
Added to `LLM-inconsistency / GV-Origin-and-posttraining`:

1. Li et al. (2023), *Benchmarking and Improving Generator-Validator Consistency of Language Models* [`UFKAC9B7`]
2. Rodriguez et al. (2025), *RankAlign: A Ranking View of the Generator-Validator Gap in Large Language Models* [`ECXF5XFM`]
3. Ouyang et al. (2022), *Training Language Models to Follow Instructions with Human Feedback* [`DCMM3AE4`]
4. Bai et al. (2022), *Constitutional AI: Harmlessness from AI Feedback* [`CSXN6PSQ`]
5. Rafailov et al. (2023), *Direct Preference Optimization* [`BNDQ5TB5`]
6. Kadavath et al. (2022), *Language Models (Mostly) Know What They Know* [`K8MWVJ89`]
7. Kadavath et al. (2022), *Teaching Models to Express Their Uncertainty in Words* [`A9IRKI92`]
8. Kuhn et al. (2023), *Semantic Uncertainty* [`MZEPR8EX`]
9. Lin et al. (2022), *TruthfulQA* [`46BIRPAA`]
10. Perez et al. (2022), *Discovering Language Model Behaviors with Model-Written Evaluations* [`EW9CHGJM`]
11. Uesato et al. (2022), *Process- and Outcome-Based Feedback* [`GE494TQJ`]
12. Lightman et al. (2023), *Let’s Verify Step by Step* [`3PPIHRBX`]
13. Cobbe et al. (2021), *Training Verifiers to Solve Math Word Problems* [`TVH86FXC`]

---

## Synthesis: plausible origins of the GV gap

### A) Pretraining induces imitation-first behavior (not explicit truth optimization)
- **TruthfulQA (Lin et al.)** supports the view that next-token imitation can reproduce common human falsehoods.
- This implies a structural source of GV gap: the model may assign high likelihood to plausible-but-wrong continuations while still having enough latent signal to recognize better alternatives in discriminative settings.

### B) Calibration/readout mismatch: “knowing” vs “saying”
- **Kadavath et al. (LMs mostly know what they know)**: confidence/readout probes reveal useful metaknowledge not always reflected in first-pass generation.
- **Kadavath et al. (uncertainty in words)** + **Kuhn et al. (semantic uncertainty)**: output format and uncertainty elicitation method materially change reliability of confidence signals.
- Interpretation: validator-style tasks can exploit latent comparative signal; generator-style free decoding may fail to expose it consistently.

### C) Objective mismatch between generation and validation heads/tasks
- **Li et al. (2023)** and **RankAlign (2025)** directly frame GV mismatch as a ranking/alignment problem.
- Generator decoding optimizes local continuation likelihood; validator tasks optimize comparative correctness among candidates. These are related but not equivalent objectives.

### D) Post-training can both help and distort consistency
- **InstructGPT / Constitutional AI / DPO**: post-training shifts model behavior toward preference-following and instruction compliance.
- These shifts can improve some user-facing quality and safety dimensions, but may also introduce mode changes (verbosity, agreeableness, stylistic priors) that decouple fluent generation from strict correctness.
- **Perez et al.** provides broad evidence that behavior profiles shift substantially across model variants and training recipes.

### E) Process supervision narrows the gap by improving credit assignment
- **Cobbe; Uesato; Lightman**: verifier/process-based signals improve reasoning reliability relative to coarse outcome/preference-only targets.
- Mechanistically, step-level supervision reduces ambiguity about *where* correctness comes from, making generator behavior more compatible with validator judgments.

---

## Base vs instruction/post-trained comparisons (what we can say from this set)

Most direct evidence in this set:
- **Ouyang et al. (InstructGPT)**: compares base GPT-3 vs instruction-tuned/RLHF models on preference-following and related quality dimensions.
- **Perez et al.**: compares behavior patterns across multiple model families/versions, capturing post-training-sensitive effects.
- **Li et al. / RankAlign**: compare pipelines before/after ranking-style interventions targeting GV mismatch.
- **Uesato / Lightman / Cobbe**: compare objective families (outcome vs process/verifier), showing objective choice strongly affects consistency.

Caveat: not every paper runs clean “same-base before/after post-training” controls on the exact GV metric; evidence is strongest when triangulated across these studies.

---

## Causal hypothesis map (literature-grounded)

```text
[Pretraining on internet text + NTP objective]
            |
            v
  (imitative continuation pressure)
            |
            +-----------------------> [Plausible-but-wrong generations]
            |
            v
[Latent knowledge partially present but weakly read out]
            |
            +-----------------------> [Calibration/readout mismatch]
            |                             (Kadavath; Kuhn)
            v
[Generator task: open-ended sequence decoding]
            |
            +--> exposure bias / decoding path errors
            |
            v
       [Generator errors]

[Validator task: candidate discrimination/ranking]
            |
            v
[Uses comparative signal more efficiently]
            |
            v
[Validator > Generator on same underlying question]
            = GV gap (Li; RankAlign)

Post-training branch:
[SFT/RLHF/RLAIF/DPO]
      |                    
      +--> [better instruction-following / style alignment]
      |
      +--> [possible over-optimization to preference proxies]
      |         |
      |         v
      |   [agreeableness/verbosity shifts; potential truth drift]
      |
      +--> [if process/verifier supervision added]
                |
                v
      [better credit assignment] -> [reduced GV gap] (Cobbe/Uesato/Lightman)
```

---

## Bottom line
The literature supports a **multi-cause account**:
1. **Pretraining objective mismatch** (imitation vs truth),
2. **Readout/calibration mismatch** (latent knowledge not reliably surfaced),
3. **Task/objective mismatch** (generation likelihood vs validation ranking), and
4. **Post-training mode shifts** that can either widen or narrow the gap depending on whether supervision is coarse preference-style vs process/verifier-style.

Most promising route to reduce GV inconsistency: combine post-training alignment with **explicit ranking/process supervision** and evaluate with base-vs-post-trained controlled comparisons on shared GV metrics.
