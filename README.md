# CISC7021 — Assignment 1 (Tiny Llama-2, 42M parameters)

Submission for CISC7021 Assignment 1: decoding strategies, perplexity evaluation (English / Chinese) and continued pre-training of a 42M-parameter Llama-2 model.

Author: **Fong Chin Wai (Vivi)** — MC653748 — B.Sc. Computer Science, Honours College, University of Macau

## Contents

| Path | Description |
|---|---|
| `CISC7021_Assignment1.ipynb` | The deliverable notebook, with all cells executed and outputs saved |
| `CISC7021_Assignment1_report.pdf` | The ACL-format report |
| `overleaf_upload.zip` | Report source: `main.tex` (ACL template) + the four training-curve figures |
| `assignment1_artifacts/train_A.json`, `train_B.json`, `train_C.json`, `train_C_seed123.json`, `train_D.json` | Raw training logs for every run (loss steps, learning rates, timings) |
| `assignment1_artifacts/runs/<run>/checkpoint-*/trainer_state.json` | Per-checkpoint training state (log history, best metric, epoch) |
| `assignment1_artifacts/final_summary.json` / `.csv`, `seed_study.json`, `task1_metrics.csv`, `task4_qc.json` | Result summaries: decoding metrics, per-group PPL, Run D results, second-seed study, Task 4 QC output |
| `assignment1_artifacts/task4_extra_zh.jsonl` | Task 4 extra Chinese material |
| `assignment1_artifacts/*.png`, `curve_run_*.png` | Training curves, decoding trade-off and PPL summary figures |
| `Model and Datasets/data/*.jsonl` | The evaluation and pre-training corpora (`en_test`, `pt_train/dev/test`, `zh_train/dev/test`) |
| `Model and Datasets/llama-42m/` | Tokenizer and model configuration files |

## Not included

The model weights (`*.safetensors`, `pytorch_model.bin`) are **not** in this repository: 16 of them are about 159 MB each and GitHub rejects any file above 100 MB. The folder holding the full run set is 2.57 GB in total, which is also why the work cannot be uploaded through the course platform (200 MB / 20-file limit). The weights are available on request.

## Environment

- Local machine, single NVIDIA RTX 4070
- Python 3.11, PyTorch (CUDA cu124), Transformers 4.46.3, Datasets, Accelerate, SentencePiece

## Note on reproducibility

The training runs were launched as background processes and resumed from checkpoints, because a single notebook kernel could not survive the long GPU jobs. Re-running a training cell whose final model already exists therefore prints `final exists / skip training` and skips the job instead of retraining; the raw logs listed above are the full record of those runs, and the notebook's saved outputs are the record of the executed session.

One helper that resolves the working directory relies on `__file__`, which a standard Jupyter kernel does not define; the notebook therefore has to be run with the repository root as the working directory. Replacing that helper with a notebook-safe path is a known open item.
