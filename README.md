# Specialization–Generalization Trade-off in Open-Weight LLMs for Hardware-Aware Embedded Code Generation — data

Data for the paper *Specialization–Generalization Trade-off in Open-Weight LLMs for Hardware-Aware Embedded Code
Generation: A Large-Scale Evaluation* by Muhammad Saqib Saeed, Benaoumeur Senouci and Boualem Benatallah.

This first release contains the data only:

- the 163,800 programs that 21 open-weight models generated on the three test sets, before and after fine-tuning;
- the per-program results with which these programs were scored;
- the per-task verdicts of every model version on twelve external benchmarks;
- the pinned Python environment.

The scoring and analysis scripts, the test-set files and the reproduction guide will be added in a later release.
Each generated program already carries the prompt it answers.

## Conditions and test sets

Each model is evaluated as **Base** (the released checkpoint) and after fine-tuning on the **Original** or the
**Modernized** corpus; in file names these are `base`, `ft_original` and `ft_grounded`. On the external
benchmarks every model has five versions: `base` and four adapters, fine-tuned on embedded Python or embedded C
code: `ft_original_py`, `ft_grounded_py`, `ft_original_c` and `ft_grounded_c`.

The three test sets, each in C and Python, are `E1` (300 tasks per language), `E2` (500 tasks, interface library
named) and `E3` (the same 500 tasks, library not named).

## Layout

    generations/
      E1/, E2/, E3/          {c,python}/<model>__<condition>.jsonl: the generated programs, one file per model,
                             condition and language (378 files); each row holds the task id, the prompt, the
                             model's raw reply (raw), the program extracted from it (code) and generation details
    results/
      E1/, E2/, E3/          per-program rows for each test set:
                               checks/{c,python}/      static checks: structural validity, compilation, code quality
                               dependency/             Python dependency resolution
                               execution/{c,python}/   emulated execution (QEMU with a Raspberry Pi OS root file
                                                       system); the .jsonl.done files only mark finished runs
                               judge/<judge model>/    LLM-judge ratings of functional relevance
                             composite_{c,python}.json: composite scores per model and condition (Tables 4 and 5)
                             tool_versions.json: gcc, cppcheck and pylint versions of the static checks
      summary/               paired statistics: stats_E1.txt, E2_E3_summary.json
      analysis/              table7.json: Table 6 of the paper (the file keeps an earlier table number);
                             G4.json: the regeneration check of Section 6
      external/              <benchmark>/<model>__<version>.jsonl: one verdict per task of twelve external
                             benchmarks (Tables 3 and 6)
    environment/             pip-freeze.lock: the pinned Python environment
    CHECKSUMS.sha256         SHA-256 of every file

## External-benchmark verdicts

`results/external/` has one folder per benchmark: HumanEval+, MBPP+, BigCodeBench, DS-1000, LiveCodeBench,
McEval-C, xCodeEval-C, MultiPL-E C++, CRUXEval-O, IFEval, GSM8K and MMLU. Each file holds one row per task:

    {"id": ..., "official_pass": true | false, "official_status": ..., "detail": ...}

`official_pass` is the verdict of the benchmark's official evaluator (GSM8K and MMLU: lm-evaluation-harness);
`official_status` is the evaluator's own label and `detail` its message. BigCodeBench and DS-1000 rows also carry
an `excluded_by_us` flag, which the paper does not use. MMLU covers all 14,042 test questions.
The HumanEval+ files include HumanEval/32, which the paper excludes. The model replies on the external benchmarks
are not included.

## Checking the files

    sha256sum -c CHECKSUMS.sha256                # Linux
    shasum -a 256 -c CHECKSUMS.sha256            # macOS

## Not included

The model weights and the LoRA adapters, the training corpora, and the model replies on the external benchmarks.

## Licence

MIT (see `LICENSE`). Third-party material and model licences are described in `NOTICE.md`.
