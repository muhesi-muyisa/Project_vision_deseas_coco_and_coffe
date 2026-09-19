# Source code — Coffee & Cocoa Disease Diagnosis

Author: **[Kambale Muhesi Muyisa]**

This repository contains the source code accompanying the paper *A Unified, Leakage-Aware
Deep-Learning Framework for Coffee and Cocoa Disease Diagnosis*. All results, tables and
figures in the paper are produced by these notebooks. The datasets are stored in Google
Drive; mount Drive and adjust the path variables at the top of each notebook before running.

## Contents

| File | Task | Reproduces |
|------|------|------------|
| `coffee_classification_dinov2.ipynb` | Coffee leaf disease **classification** (main pipeline) | Tables 1–6, Figures 1–11 |
| `coffee_baseline_efficientnet_elm.ipynb` | Coffee **lightweight baseline** (EfficientNet-B0 + ELM) | Section 5.7 |
| `cocoa_detection_yolov11.ipynb` | Cocoa pod disease **detection** (YOLOv11) | Table 7, Figures 12–14 |

## How the code maps to the paper

### `coffee_classification_dinov2.ipynb`
- **Cross-dataset deduplication (MD5 + 272-bit dHash)** → Table 1, Figure 1 (per-source reduction).
- **Deduplication audit on JMuBEN** (pairwise Hamming, duplicate clusters) → Figure 3, Figure 4.
- **Stratified 70/15/15 split** and EDA → Table 2, Figure 2.
- **DINOv2 ViT-L/14 CLS feature extraction** (frozen) → Section 4.3.
- **Handcrafted HSV + Gabor descriptor (136-D)** → Section 4.4.
- **Fusion (α = 0.95) + PCA (95% variance → 344-D)** → Section 4.5.
- **Classifier comparison** (ELM, ELM ensemble, SVM, Random Forest, XGBoost) with 95% bootstrap CIs → Table 3, Figure 5.
- **Confusion matrix and per-class metrics** → Figure 6, Figure 7, Table 4.
- **Five-fold fine-tuned ensemble + multi-scale TTA** → Table 3 (best row), Section 4.8–4.9.
- **Ablation studies** (no-HC, ViT-B vs ViT-L, single vs K-fold) → Table 5, Figure 8.
- **Temperature-scaling calibration** → Figure 9 (ECE 0.0846 → 0.0058).
- **Inference-speed benchmark** → Table 6, Figure 10, Figure 11.
- **McNemar significance tests** → Sections 5.2, 5.4.

### `coffee_baseline_efficientnet_elm.ipynb`
- Frozen **EfficientNet-B0 (1280-D)** + handcrafted (368-D) fusion + **ELM** on a single 2,000-image set.
- Produces the lightweight-baseline numbers of **Section 5.7** (accuracy 85.75%, macro-F1 85.31%).

### `cocoa_detection_yolov11.ipynb`
- Loads the annotated cocoa-pod dataset, builds a **stratified 80/20 split**.
- Fine-tunes **YOLOv11-nano** (25 epochs, 640 px) → per-class mAP in **Table 7** and **Figure 12**.
- Runs inference on a dataset image and an external internet image → **Figure 13**, **Figure 14**.

## Requirements
See `requirements.txt`. Core stack: PyTorch, timm/transformers (DINOv2), scikit-learn,
scikit-image, xgboost, ultralytics (YOLOv11), matplotlib, numpy, pandas, opencv-python,
Pillow. A GPU is recommended (the paper used an NVIDIA T4 for DINOv2 and a P100 for the
EfficientNet baseline).

## Reproducibility notes
- Random seeds are fixed for the data splits and the ELM initialisation; deduplication is
  deterministic given the input files, so the exact splits are reproducible.
- Set the Google Drive path variables at the top of each notebook to match your own folder
  layout before running.

## Attribution
This code is the author's own work. Where a block was adapted from a public source
(a library tutorial or a public notebook), that source should be cited in the corresponding
cell and listed here, in line with good academic-integrity practice.
