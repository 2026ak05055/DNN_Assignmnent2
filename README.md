# DNN Programming Assignment 2

## Chosen Configuration

- Shared seeds: **(17, 42, 2026)**.
- Problem 1: **h=64**; all recurrent runs use Adam with **lr=1e-3**, batch size **128**, and **20 epochs** per experiment. The adding lengths are **(50, 100, 200, 400)**; data sizes are **10,000/1,000/1,000** with seeds **0/1/2**. The selected ablation compares LSTM forget-gate bias **0 versus 1** at **T=200**. The gradient diagnostic uses **T=100**, the solved threshold is **MSE < 0.05**, and the hidden-size sweep is **(16, 32, 64, 128)**.
- Problem 2: **d=64**, **4 heads**, **4 layers**, **context 128**. The width 64 is divisible by the **1, 4, and 8** head counts used in the ablation. HAR uses **20 epochs** and batch size **64**; the base language model uses **1,000 steps**, head/mask ablations use **500 steps**, and language-model batch size is **8**.
- Both notebooks select `cuda` when available and otherwise `cpu`. CPU and CUDA T4 use the same model sizes and experiment grids.

## Runtime and completion

- Total Run All time on a T4: **not measured yet**. This workspace has no T4 execution; record the elapsed time after completing both notebooks on a T4 rather than treating CPU time as a substitute.
- The Problem 2 full workflow has not completed in this workspace. Run both notebooks from a fresh kernel to generate the required current-configuration results and figures. A `report.pdf` and submission zip have not been created; do not submit this workspace as complete until they are added and checked.
- Some saved Problem 1 cell outputs still show the earlier **h=32** run; regenerate notebook outputs after applying the current **h=64** configuration.

## Run All

Install the pinned environment with `pip install -r requirements.txt`. Open each notebook, restart its kernel, and use **Run All** in this order:

1. `problem1/problem1.ipynb`
2. `problem2/problem2.ipynb`

Runs append missing evidence to `results.csv` and skip existing matching run keys. Existing rows from older configurations remain in the file but are excluded from current reports by seed, model, sequence-length, and parameter/configuration filters.

The final Problem 2 analysis rebuilds the HAR comparison figure from both problems' current results without retraining. If either three-seed HAR inventory is missing or duplicated, it lists the exact model/seed keys; copy the completed Problem 1 results into the same shared `results.csv`, preserving Problem 2 rows, then rerun analysis. Old seeds (0/1/2) do not replace the chosen seeds (17/42/2026).

## Outputs

HAR data is under `data/`; Tiny Shakespeare is downloaded to `data/tinyshakespeare.txt`. Figures are written to `problem1/figures/` and `problem2/figures/`. Configuration- and budget-specific checkpoints are written to `problem2/checkpoints/` for resuming experiments; exclude checkpoints from the submission zip. Generated text and attention analysis are written to `problem2/generated_samples.txt`, `problem2/mask_ablation_samples.txt`, and `problem2/attention_heatmap_analysis.txt`.

CUDA T4 is recommended for full experiments. CPU Run All is supported but may take several hours, especially the language-model training and matched ablations.
