# Qwen3-0.6B Inference Experiments

This repository contains my inference work for a team LLM course project. I designed and ran a KV cache benchmark to measure how caching affects generation time, throughput, GPU memory, and answer quality. The benchmark uses the published Qwen3-0.6B checkpoint with a LoRA adapter and the SQuAD 1.1 test split from our [team repository](https://github.com/sunweiyi2026-ship-it/LLM-project).

## Notebook

[`inference_experiments.ipynb`](inference_experiments.ipynb) contains the benchmark code, output charts, and a short analysis.

## KV Cache Results

I ran the same 900 questions three times per setting on an NVIDIA T4 in FP16, using greedy decoding and a batch size of 4.

| Metric | Cache off | Cache on |
| --- | ---: | ---: |
| Throughput (questions/s) | 2.06 | 2.51 |
| Total generation time (s) | 1312.48 | 1074.25 |
| Peak allocated GPU memory (MiB) | 1,349.72 | 1698.24 |
| Peak extra allocated GPU memory (MiB) | 161.54 | 510.05 |
| Exact match (%) | 77.00 | 76.89 |

Caching increased throughput by about **22%** and raised peak extra GPU memory by **348.51 MiB**. The decoded answers matched on **899 of 900 questions**.

## Reproduce the Benchmark

1. Open the notebook in Google Colab with a GPU runtime and Python 3.12.
2. Run the notebook cells in order. The benchmark generates the charts and exports the per-batch timings and summary as CSV files.

