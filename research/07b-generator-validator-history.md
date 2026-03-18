# Generator–Validator Gap: Historical & Pre-LLM Foundations

## Purpose
This note expands the historical grounding for the modern **generator–validator gap**: systems are often better at **evaluating/ranking/verifying** candidate outputs than at **producing** the best output directly in one shot.

---

## A. Discriminative vs Generative Modeling (Core Statistical Ancestor)

### 1) Classic statistical tradeoff (sample efficiency vs asymptotic boundary quality)
1. **Ng & Jordan (2002)**, *On Discriminative vs. Generative Classifiers*  
   Canonical: https://proceedings.neurips.cc/paper/2001/hash/7b7a53e239400a13bd6be6c91c4f6c4e-Abstract.html  
   Key result: generative models can converge faster with little data, but discriminative objectives often win asymptotically in classification error.

2. **Lafferty, McCallum, Pereira (2001)**, *Conditional Random Fields*  
   Canonical: https://repository.upenn.edu/cis_papers/159  
   CRFs model \(p(y\mid x)\) directly, avoiding strong generative assumptions and becoming a foundational discriminative structured prediction approach.

3. **Taskar, Guestrin, Koller (2003)**, *Max-Margin Markov Networks*  
   Canonical: https://proceedings.neurips.cc/paper/2003/hash/9fb4651c05b2ed70fba5afe0b039a550-Abstract.html  
   Pushes discriminative training into structured outputs, reinforcing the “score/rank structures” paradigm.

4. **Collins (2002)**, *Discriminative Training Methods for Hidden Markov Models*  
   Canonical: https://aclanthology.org/W02-1001/  
   Demonstrates strong performance gains from discriminative updates (perceptron-style) over likelihood-centric generative training in sequence tasks.

**Modern mapping to LLM gap:** these lines prefigure the idea that **decision boundaries / ranking functions** can outperform direct likelihood-driven generation for end-task correctness.

---

## B. Reranking / Verify-after-Generate in NLP (Direct Procedural Ancestor)

### B1) Parsing: generate candidates, then discriminatively rerank
5. **Collins & Koo (2005)**, *Discriminative Reranking for Natural Language Parsing*  
   Canonical: https://aclanthology.org/J05-4002/  
   Two-stage pattern: produce n-best parses, then rerank with richer features.

6. **Charniak & Johnson (2005)**, *Coarse-to-Fine n-Best Parsing and MaxEnt Discriminative Reranking*  
   Canonical: https://aclanthology.org/P05-1022/  
   Canonical early demonstration that rerankers exploit features too costly for first-pass search.

### B2) Machine translation: decoding, then better scoring criteria
7. **Och (2003)**, *Minimum Error Rate Training in Statistical Machine Translation*  
   Canonical: https://aclanthology.org/P03-1021/  
   Tunes model weights toward task metrics (e.g., BLEU) over candidate sets, explicitly separating generation from downstream selection objective.

8. **Kumar & Byrne (2004)**, *Minimum Bayes-Risk Decoding for Statistical Machine Translation*  
   Canonical: https://aclanthology.org/N04-1022/  
   Picks hypotheses minimizing expected loss under a posterior over candidates; quintessential “choose best from many” framing.

9. **Shen, Sarkar, Och (2004)**, *Discriminative Reranking for Machine Translation*  
   Canonical: https://aclanthology.org/N04-1023/  
   Explicit MT reranking result: better final quality from second-pass discriminative scoring.

10. **Chiang (2007)**, *Hierarchical Phrase-Based Translation*  
    Canonical: https://aclanthology.org/P07-1019/  
    Practical SMT search/scoring architecture where decoding approximations plus later scoring decisions matter; reinforces stage-separated inference.

### B3) QA / evidence aggregation: confidence-weighted verification
11. **Ferrucci et al. (2010)**, *Building Watson: An Overview of the DeepQA Project*  
    Canonical: https://ojs.aaai.org/aimagazine/index.php/aimagazine/article/view/2303  
    Watson’s pipeline generated many candidate answers/evidence paths, then used confidence estimation for final selection.

12. **Ittycheriah, Franz, Zhu (2001)**, *Question Answering Using Maximum Entropy Components*  
    Canonical: https://aclanthology.org/N01-1005/  
    Early QA architecture combining candidate extraction with discriminative scoring components.

**Modern mapping to LLM gap:** the contemporary “sample many CoTs / tool calls / drafts, then verify or rerank” is structurally the same as classical n-best reranking and risk-minimizing decision layers.

---

## C. Why Verification Can Be Easier than Open-Ended Generation (Computational View)

13. **Cook (1971)**, *The Complexity of Theorem-Proving Procedures*  
    Canonical: https://www.cs.toronto.edu/~sacook/homepage/cook71.pdf  
    NP framing captures the asymmetry: checking a proposed witness is typically easier than finding one.

14. **Garey & Johnson (1979)**, *Computers and Intractability*  
    Canonical: https://www.wiley.com/en-us/Computers+and+Intractability%3A+A+Guide+to+the+Theory+of+NP-Completeness-p-9780716710455  
    Standard reference for search-vs-verification complexity distinctions.

15. **Blum & Kannan (1995)**, *Designing Programs That Check Their Work*  
    Canonical: https://dl.acm.org/doi/10.1145/227683.227684  
    Formalizes checker programs: validate outputs more cheaply/reliably than reproducing full computation.

**Modern mapping to LLM gap:** generator/verifier pipelines align with this old algorithmic pattern—use expensive/unstable search to propose, then apply comparatively reliable checking/ranking.

---

## D. Calibration, Confidence, and Energy-Based Links

16. **LeCun, Chopra, Hadsell, Ranzato, Huang (2006)**, *A Tutorial on Energy-Based Learning*  
    Canonical: http://yann.lecun.com/exdb/publis/pdf/lecun-06.pdf  
    Energy functions provide a general framework for scoring/ranking structured hypotheses without full normalized generation.

17. **Niculescu-Mizil & Caruana (2005)**, *Predicting Good Probabilities with Supervised Learning*  
    Canonical: https://dl.acm.org/doi/10.1145/1102351.1102430  
    Shows many strong classifiers are poorly calibrated out of the box; calibration changes decision reliability.

18. **Guo, Pleiss, Sun, Weinberger (2017)**, *On Calibration of Modern Neural Networks*  
    Canonical: https://arxiv.org/abs/1706.04599  
    Deep models are often overconfident; simple post-hoc temperature scaling helps confidence quality.

19. **Hendrycks & Gimpel (2017)**, *A Baseline for Detecting Misclassified and OOD Examples*  
    Canonical: https://arxiv.org/abs/1610.02136  
    Confidence scores can support reject/abstain behavior—an important precursor to verifier-gated generation.

20. **Grathwohl et al. (2020)**, *Your Classifier is Secretly an Energy Based Model*  
    Canonical: https://arxiv.org/abs/1912.03263  
    Connects discriminative classifiers and energy-based scoring, strengthening “judge model as energy/ranker” interpretation.

21. **Lakshminarayanan, Pritzel, Blundell (2017)**, *Simple and Scalable Predictive Uncertainty Estimation using Deep Ensembles*  
    Canonical: https://arxiv.org/abs/1612.01474  
    Ensemble disagreement is useful for confidence-aware selection, akin to modern multi-sample consensus and validator confidence.

**Modern mapping to LLM gap:** validators are only useful if their confidence/ranking signal is calibrated enough to separate true from fluent-but-wrong candidates.

---

## E. Bridging Map: Historical Lines → Current LLM Methods

- **Discriminative vs generative classifiers (Ng & Jordan; CRF/MMN/Collins)**  
  → **LLM best-of-N + verifier / reward model reranking**.  
  Historical lesson: direct generation likelihood is not identical to decision-optimal scoring.

- **n-best reranking in parsing/MT (Collins & Koo; Charniak & Johnson; MERT/MBR)**  
  → **self-consistency, process reward reranking, candidate selection over sampled traces**.  
  Historical lesson: split hard search from richer second-pass evaluation.

- **DeepQA confidence aggregation (Watson)**  
  → **tool-augmented agent pipelines with judge models and confidence thresholds**.  
  Historical lesson: final answer quality depends heavily on evidence-weighted adjudication.

- **Complexity-theoretic search-vs-check asymmetry (Cook; Blum-Kannan)**  
  → **generate-then-verify architectures** as a principled computational strategy, not just an empirical hack.

- **Calibration/energy scoring literature**  
  → **LLM-as-judge reliability work, rejection mechanisms, uncertainty-aware routing**.  
  Historical lesson: better scoring is not enough; score interpretability/calibration is critical.

---

## F. Implications for the Modern Generator–Validator Gap

1. **The gap is historically expected**, not an LLM anomaly: older NLP systems already gained from multi-pass generation + discriminative reranking.
2. **Verifier quality, not just generator quality, is a bottleneck**: weak calibration can invert gains.
3. **Process-level checks are historically consistent** with richer-feature second-pass scoring in parsing/MT.
4. **Inference-time compute scaling** (more candidates + stronger validation) has deep precedent in n-best, MBR, and confidence aggregation pipelines.
5. **Failure mode continuity:** when candidate sets are low-diversity or verifier criteria misaligned, reranking saturates or amplifies systematic errors.

---

## G. Recommended “Top Additions” BibTeX

```bibtex
@inproceedings{ng2002discriminative,
  title={On Discriminative vs. Generative Classifiers: A comparison of logistic regression and naive Bayes},
  author={Ng, Andrew Y. and Jordan, Michael I.},
  booktitle={Advances in Neural Information Processing Systems},
  year={2001},
  url={https://proceedings.neurips.cc/paper/2001/hash/7b7a53e239400a13bd6be6c91c4f6c4e-Abstract.html}
}

@inproceedings{lafferty2001crf,
  title={Conditional Random Fields: Probabilistic Models for Segmenting and Labeling Sequence Data},
  author={Lafferty, John and McCallum, Andrew and Pereira, Fernando},
  booktitle={Proceedings of ICML},
  year={2001},
  url={https://repository.upenn.edu/cis_papers/159}
}

@inproceedings{collins2002discriminative,
  title={Discriminative Training Methods for Hidden Markov Models: Theory and Experiments with Perceptron Algorithms},
  author={Collins, Michael},
  booktitle={Proceedings of EMNLP},
  year={2002},
  url={https://aclanthology.org/W02-1001/}
}

@article{collinskoo2005reranking,
  title={Discriminative Reranking for Natural Language Parsing},
  author={Collins, Michael and Koo, Terry},
  journal={Computational Linguistics},
  volume={31},
  number={1},
  pages={25--70},
  year={2005},
  doi={10.1162/0891201053630273},
  url={https://aclanthology.org/J05-4002/}
}

@inproceedings{charniak2005coarse,
  title={Coarse-to-Fine N-Best Parsing and MaxEnt Discriminative Reranking},
  author={Charniak, Eugene and Johnson, Mark},
  booktitle={Proceedings of ACL},
  year={2005},
  url={https://aclanthology.org/P05-1022/}
}

@inproceedings{och2003mert,
  title={Minimum Error Rate Training in Statistical Machine Translation},
  author={Och, Franz Josef},
  booktitle={Proceedings of ACL},
  year={2003},
  url={https://aclanthology.org/P03-1021/}
}

@inproceedings{kumar2004mbr,
  title={Minimum Bayes-Risk Decoding for Statistical Machine Translation},
  author={Kumar, Shankar and Byrne, William},
  booktitle={Proceedings of HLT-NAACL},
  year={2004},
  url={https://aclanthology.org/N04-1022/}
}

@inproceedings{shen2004mt,
  title={Discriminative Reranking for Machine Translation},
  author={Shen, Libin and Sarkar, Anoop and Och, Franz Josef},
  booktitle={Proceedings of HLT-NAACL},
  year={2004},
  url={https://aclanthology.org/N04-1023/}
}

@article{ferrucci2010watson,
  title={Building Watson: An Overview of the DeepQA Project},
  author={Ferrucci, David and Brown, Eric and Chu-Carroll, Jennifer and others},
  journal={AI Magazine},
  volume={31},
  number={3},
  pages={59--79},
  year={2010},
  doi={10.1609/aimag.v31i3.2303},
  url={https://ojs.aaai.org/aimagazine/index.php/aimagazine/article/view/2303}
}

@article{cook1971complexity,
  title={The Complexity of Theorem-Proving Procedures},
  author={Cook, Stephen A.},
  journal={Proceedings of the Third Annual ACM Symposium on Theory of Computing},
  pages={151--158},
  year={1971},
  doi={10.1145/800157.805047},
  url={https://www.cs.toronto.edu/~sacook/homepage/cook71.pdf}
}

@article{blum1995checking,
  title={Designing Programs That Check Their Work},
  author={Blum, Manuel and Kannan, Sampath},
  journal={Journal of the ACM},
  volume={42},
  number={1},
  pages={269--291},
  year={1995},
  doi={10.1145/200836.200880},
  url={https://dl.acm.org/doi/10.1145/200836.200880}
}

@article{lecun2006energy,
  title={A Tutorial on Energy-Based Learning},
  author={LeCun, Yann and Chopra, Sumit and Hadsell, Raia and Ranzato, Marc'Aurelio and Huang, Fu-Jie},
  journal={Predicting Structured Data},
  year={2006},
  url={http://yann.lecun.com/exdb/publis/pdf/lecun-06.pdf}
}

@inproceedings{niculescu2005predicting,
  title={Predicting Good Probabilities with Supervised Learning},
  author={Niculescu-Mizil, Alexandru and Caruana, Rich},
  booktitle={Proceedings of ICML},
  year={2005},
  url={https://dl.acm.org/doi/10.1145/1102351.1102430}
}

@inproceedings{guo2017calibration,
  title={On Calibration of Modern Neural Networks},
  author={Guo, Chuan and Pleiss, Geoff and Sun, Yu and Weinberger, Kilian Q.},
  booktitle={Proceedings of ICML},
  year={2017},
  url={https://arxiv.org/abs/1706.04599}
}

@inproceedings{grathwohl2020ebm,
  title={Your Classifier is Secretly an Energy Based Model and You Should Treat it Like One},
  author={Grathwohl, Will and Wang, Kuan-Chieh and Jacobsen, J{"o}rn-Henrik and others},
  booktitle={Proceedings of ICLR},
  year={2020},
  url={https://arxiv.org/abs/1912.03263}
}
```

---

## H. Suggested integration into survey narrative

A compact storyline for `generator-validator-gap.qmd`:
1. **Theory anchor:** search-vs-check asymmetry (Cook; Blum-Kannan).
2. **NLP engineering anchor:** n-best reranking in parsing/MT and confidence aggregation in QA.
3. **Statistical learning anchor:** discriminative objectives often better aligned with selection decisions than raw generative likelihood.
4. **Modern LLM consequence:** test-time scaling works best when generation and validation are explicitly separated and validator calibration is monitored.
