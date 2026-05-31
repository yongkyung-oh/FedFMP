# Benchmark Landscape

This page documents the rating scale and short rationale for the 12 x 6 benchmark matrix in [`../data/benchmark_matrix.csv`](../data/benchmark_matrix.csv).

## Rating Question

For each benchmark and silent failure mode, we ask: **does the benchmark, as designed and distributed, let a practitioner measure this failure mode?**

We rate the benchmark's released evaluation surface, not what could be added by a new extension.

## Rating Scale

| Symbol | CSV value | Meaning |
|---|---|---|
| ✓ | `direct` | The failure-mode metric is reported by the benchmark's official evaluation scripts or standard outputs. |
| △ | `proxy` | The metric can be derived from standard outputs with limited post-processing, or it applies only to part of the benchmark. |
| — | `none` | The benchmark's design does not directly address the failure mode. |

These ratings involve judgment, especially near the `proxy` / `none` boundary. Coverage is also not quality: a `direct` rating means the behavior is measured, not that it is measured well or under federated privacy constraints.

## Benchmark Notes

### Federated Benchmarks

**[LEAF](https://arxiv.org/abs/1812.01097).** Captures client imbalance and statistical heterogeneity in federated settings, but behavioral failures such as alignment erosion or confidence miscalibration are outside its scope.

**[FedScale](https://proceedings.mlr.press/v162/lai22a.html).** Provides scalable federated workloads and system-level measurements; trustworthiness appears only through proxies such as heterogeneity and robustness.

**[FLamby](https://proceedings.neurips.cc/paper_files/paper/2022/hash/232eee8ef411a0a316efa298d7be3c2b-Abstract-Datasets_and_Benchmarks.html).** Uses realistic cross-silo healthcare splits that expose site-level fairness and out-of-domain risks, but it does not test foundation-model alignment or safety behavior.

**[FedLLM-Bench](https://proceedings.neurips.cc/paper_files/paper/2024/hash/c8cdab0e890c59255c27977072fdb0f0-Abstract-Datasets_and_Benchmarks_Track.html).** Covers federated LLM tuning and preference-alignment settings, but its metrics center on training outcomes rather than privacy-preserving behavioral monitoring.

**[FLHetBench](https://openaccess.thecvf.com/content/CVPR2024/html/Zhang_FLHetBench_Benchmarking_Device_and_State_Heterogeneity_in_Federated_Learning_CVPR_2024_paper.html).** Studies device and state heterogeneity; its relevance to silent failures is system-level because availability and resource variation can mask behavioral problems.

**[PFLlib](https://www.jmlr.org/papers/v26/23-1634.html).** Supports personalized federated learning and cross-client generalization experiments, but its reported outcomes remain algorithmic rather than behavioral.

### Centralized Trustworthiness Benchmarks

**[HELM](https://openreview.net/forum?id=iO4LZibEqW).** Measures broad language-model behavior, including accuracy, calibration, robustness, fairness, bias, and toxicity, but assumes centralized access to inputs and outputs.

**[BIG-bench](https://openreview.net/forum?id=uyTL5Bvosj).** Probes language-model capabilities and reasoning, but does not target federated heterogeneity, personalization, or deployment-time trustworthiness failures.

**[DecodingTrust](https://proceedings.neurips.cc/paper_files/paper/2023/hash/63cb9921eecf51bfad27a99b2c53dd6d-Abstract-Datasets_and_Benchmarks.html).** Covers many behavioral risks in GPT models, including toxicity, stereotype bias, fairness, privacy, and robustness, but does not model federated aggregation or limited client observability.

**[JailbreakBench](https://proceedings.neurips.cc/paper_files/paper/2024/hash/63092d79154adebd7305dfd498cbff70-Abstract-Datasets_and_Benchmarks_Track.html).** Standardizes jailbreak attack and defense evaluation; it informs alignment-erosion analysis but focuses on adversarial safety rather than federated personalization.

**[TrustLLM](https://proceedings.mlr.press/v235/huang24x.html).** Spans truthfulness, safety, fairness, robustness, privacy, and ethics, but evaluates centralized model behavior rather than federated privacy constraints.

**[HarmBench](https://proceedings.mlr.press/v235/mazeika24a.html).** Evaluates automated red teaming and refusal behavior across harmful behavior categories, but does not study how failures arise or stay hidden during federated personalization.
