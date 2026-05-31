# Silent Failures in Federated Personalization of Foundation Models

**A taxonomy of "silent failures" in Federated Foundation Model Personalization (FedFMP), and why privacy-preserving training is not, by itself, evidence of trustworthy deployment.**

Companion repository for the ACM SIGKDD 2026 (KDD '26) Blue Sky Ideas paper by **YongKyung Oh** and **Alex Bui** (Medical & Imaging Informatics, UCLA).

[![DOI](https://img.shields.io/badge/DOI-10.1145%2F3770855.3818661-blue)](https://doi.org/10.1145/3770855.3818661)
&nbsp;arXiv: _coming soon_ &nbsp;·&nbsp; License: [MIT](LICENSE) (code & docs)

---

## What is Federated Foundation Model Personalization (FedFMP)?

**Federated Foundation Model Personalization (FedFMP)** is the setting where a shared **foundation model** is **personalized on decentralized, private client data through federated learning** — typically by training small parameter-efficient adapters locally and aggregating them, without centralizing the data.

> **FedFMP, in one sentence.** FedFMP is the personalization of a pretrained foundation model across many clients' private data via federated learning, so that the model adapts to each client without the raw data ever leaving the device or institution.

This pairing is increasingly common: privacy regulation pushes training toward federated learning, while foundation models are deployed at scale under growing expectations for post-deployment monitoring. FedFMP sits at that intersection.

## What is a "Silent Failure"?

We introduce **silent failures** as a named category of trustworthiness problem in FedFMP.

> **Silent failure (definition).** A *silent failure* is a behavioral degradation of a federated-personalized foundation model — such as amplified bias, fairness collapse, miscalibration, out-of-domain degradation, or alignment erosion — that standard, system-level federated metrics do **not** surface because federated privacy constraints hide the model behavior needed to detect it.

The key word is **silent**: the failure is not only hard to *fix* — it is hard to *see*. Federated learning protects privacy by limiting visibility into local data and model behavior, and that same limited visibility lets behavioral degradations accumulate without tripping a performance alarm. Our central claim:

> **Privacy-preserving training is not, by itself, evidence of trustworthy deployment.**

## The six silent failure modes

A taxonomy organized by causal layer (data → model → system):

| Layer | Failure mode | What goes wrong |
|---|---|---|
| Data | **Amplified Bias** | Personalizing on skewed local data amplifies group disparities; privacy hinders central auditing. |
| Data | **Confidence Miscalibration** | Confidence decouples from accuracy under shift; aggregation masks localized overconfident errors. |
| Model | **Fairness Collapse** | Aggregating adapters tuned to divergent client distributions widens cross-client performance gaps. |
| Model | **Adaptation Misalignment** | Overfitting narrow local objectives degrades general capability and safety within a round. |
| System | **Out-of-Domain Degradation** | Over-specialization to a local domain weakens cross-client and zero-shot generalization. |
| System | **Alignment Erosion** | Small per-round safety/persona degradations accumulate across aggregation rounds and stay hidden. |

## Why current benchmarks miss them: a structural divide

A landscape analysis of **12 benchmarks** finds a **structural divide** between two evaluation paradigms that do not currently meet:

- **Federated benchmarks** measure system-level performance but give limited visibility into model *behavior*.
- **Centralized trustworthiness benchmarks** measure behavior but assume **direct model access** that federated privacy restricts.

No single framework in this set spans both paradigms, so the monitoring gap is *structural* rather than a gap in any one benchmark. The full 12 x 6 rating matrix is in [`data/benchmark_matrix.csv`](data/benchmark_matrix.csv), and the rating scale plus short benchmark notes are in [`docs/benchmark.md`](docs/benchmark.md).

## How is this different from adversarial robustness / red-teaming?

Adversarial robustness and red-teaming study failures triggered by an **external attacker** with probing access to the model. **Silent failures are different**: they arise from system dynamics during federated personalization (skewed local data, adapter aggregation, concept drift), and they surface precisely when probing access is **unavailable** because federated privacy restricts observability. That lack of visibility is the monitoring gap this work names.

## Repository contents

```
.
├── README.md                       # this file
├── CITATION.cff                    # machine-readable citation metadata
├── LICENSE                         # MIT (code & docs)
├── data/
│   └── benchmark_matrix.csv        # 12 benchmarks × 6 failure modes rating matrix
└── docs/
    └── benchmark.md                # rating scale, benchmark notes, and main landscape pattern
```

## Key terms

Federated learning · foundation models · large language models · personalization · parameter-efficient fine-tuning (PEFT) · federated fine-tuning of LLMs · trustworthy machine learning · trustworthy federated learning · fairness · calibration · alignment · out-of-distribution generalization · concept drift · post-deployment monitoring · behavioral evaluation · silent failures · FedFMP.

## Citation

Machine-readable metadata is in [`CITATION.cff`](CITATION.cff). To cite the paper:

```bibtex
@inproceedings{oh2026silent,
  title     = {Silent Failures in Federated Personalization of Foundation Models},
  author    = {Oh, YongKyung and Bui, Alex},
  booktitle = {Proceedings of the 32nd ACM SIGKDD Conference on Knowledge Discovery and Data Mining V.2 (KDD '26)},
  year      = {2026},
  publisher = {Association for Computing Machinery},
  address   = {Jeju Island, Republic of Korea},
  doi       = {10.1145/3770855.3818661},
  isbn      = {979-8-4007-2259-2},
  note      = {Blue Sky Ideas Track}
}
```

## License

Code and documentation in this repository are released under the [MIT License](LICENSE).
The paper text is governed by its publication license (CC BY 4.0 via ACM). Please cite
the paper using the metadata above.
