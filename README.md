# Calibration-Efficient and Uncertainty-Aware Gradient Boosting for Deployable Mental-Workload Detection on Consumer-Grade EEG

Reproducible code for the paper of the same name (submitted to *International Journal of Medical Informatics*).

**Authors (equal contribution / co-first):** Ananya Sharma, Amogh Kale, Aditi Pattanashetti.

## What this does
A lightweight gradient-boosting pipeline for mental-workload detection from consumer-grade EEG (STEW, 14-channel Emotiv EPOC), evaluated honestly with leave-one-subject-out (LOSO). Includes:
- Band-power / ratio / frontal-asymmetry feature extraction (theta, alpha, beta) from 4 s windows.
- XGBoost / LightGBM / CatBoost vs SVM and Random Forest, under 10-fold **and** LOSO.
- Calibration-efficiency analysis (how few labelled windows a new user needs).
- Split-conformal selective prediction (confidence-aware abstention).
- SHAP interpretability and a channel-montage ablation (down to a 4-channel Muse-class subset).
- Automatic assembly of the manuscript `.docx` with all tables and figures.

## Key results (LOSO, subject-independent)
- XGBoost: **82.1%** accuracy, F1 0.783, at ~0.08 ms/window on CPU (7.2 pts above SVM).
- ~80 s of one-time calibration lifts accuracy from **82.1% to 88.6%**.
- Conformal selective prediction gives confidence-controlled abstention.
- 4-channel Muse-class montage retains **0.72** accuracy (vs 0.82 full headset).

## Data
The **STEW** dataset is **not** included here (see its own license). Download it from IEEE DataPort:
https://ieee-dataport.org/open-access/stew-simultaneous-task-eeg-workload-dataset
Place the per-subject files (`sub01_hi.txt`, `sub01_lo.txt`, …) so the notebook can find them (the notebook unzips `STEW Dataset.zip` from Google Drive, or reads `./data/STEW/`).

## How to run
1. Open `EEG_Workload_GradientBoosting.ipynb` in Google Colab.
2. Put `STEW Dataset.zip` in your Google Drive (the load cell mounts Drive and finds it), **or** adapt the load cell to a local path.
3. `Runtime → Run all`. The final cell writes `EEG_paper_COMPLETE.docx` and the figures.

Runtime: ~15–25 min on a standard Colab CPU instance (the calibration/conformal/montage sweeps are the slow part).

## Requirements
See `requirements.txt`. Core: numpy, scipy, scikit-learn, xgboost, lightgbm, catboost, shap, scikit-posthocs, matplotlib, pandas.

## Reproducibility notes
- All random seeds fixed (`RNG = 42`).
- Standardisation is fit on training folds only (no test leakage).
- Feature groups are fixed a priori from EEG physiology (no data-driven feature selection).

## Citation
If you use this code, please cite the paper (details to be added on publication).

## Declaration of AI assistance
Generative AI tools assisted with drafting and editing of the manuscript text and code scaffolding. All study design, analysis, results and interpretation were performed and verified by the authors.

## License
MIT (see `LICENSE`).
