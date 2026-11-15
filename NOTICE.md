# Licensing and third-party notices

## This repository

The generated programs (`generations/`) and the results (`results/`) are released under the **MIT License**
(see `LICENSE`), Copyright (c) 2026 Muhammad Saqib Saeed.

## External-benchmark verdicts

`results/external/<benchmark>/` (MMLU: the full 14,042-question test) holds one verdict per task of twelve
public benchmarks (HumanEval+, MBPP+, BigCodeBench, DS-1000, LiveCodeBench, CRUXEval-O, MultiPL-E C++, McEval-C,
xCodeEval-C, IFEval, GSM8K, MMLU). Ten benchmarks were graded with their official evaluators, GSM8K and MMLU with
lm-evaluation-harness. Each row holds the task identifier, the pass/fail decision and status, and a `detail`
field with the grader's message; depending on the benchmark this message quotes part of the model's answer, the
expected answer or a failing test input. BigCodeBench and DS-1000 rows also carry an `excluded_by_us` flag, which
the paper does not use (every row enters Table 6). The benchmark problems, the full model replies and the
evaluators are not included; each benchmark keeps its own licence.

## Training corpora

The Original and Modernized training corpora are not part of this repository.

## Model weights

Not included: neither the 21 evaluated models, nor the three judge models, nor the LoRA adapters trained in this
study. Each base model carries its own licence, and the adapters are covered by the licence of their base model.
