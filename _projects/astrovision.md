---
layout: page
title: AstroVision
description: Deep-learning pipeline for galaxy morphological classification with multi-modal fusion and uncertainty quantification
img: assets/img/projects/astrovision_preview.png
importance: 2
category: astrophysics
related_publications: false
---

## Overview

**AstroVision** is an open-source deep-learning pipeline for automated galaxy morphological classification on the [Galaxy10 DECaLS](https://zenodo.org/record/10845026) dataset — 17,736 RGB galaxy images across ten GalZoo-style morphological classes derived from the Dark Energy Camera Legacy Survey (DECaLS).

The pipeline benchmarks four architectures (SimpleCNN, EfficientNet-B0, DINOv2 zero-shot probe, DINOv2 fine-tuned), culminating in a late-fusion multi-modal classifier that combines visual foundation-model features, non-parametric morphometrics, and SDSS DR16 photometry.

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/projects/astrovision_confusion.png" title="Confusion matrix — late-fusion classifier" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/projects/astrovision_umap.png" title="UMAP of DINOv2 feature space" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Left: Confusion matrix for the best late-fusion classifier (balanced accuracy = 0.8631). Edge-on and smooth classes are recovered with high reliability; the Disturbed class exhibits an irreducible recall ceiling (~0.53). Right: UMAP projection of the 768-dimensional DINOv2 feature space, coloured by SDSS photometric colour g−r, showing spontaneous segregation of the Blue Cloud and Red Sequence.
</div>

## Scientific Finding

A central result of this work concerns the physical content of self-supervised visual representations: **the second principal component of the DINOv2 feature space (PC2) simultaneously encodes both morphological concentration (Gini, ρS = 0.53) and stellar population colour (g−r, ρS = 0.30), without any explicit tabular photometric supervision during feature learning.**

A Lasso regression from DINOv2 features predicts photometric colour g−r with R² = 0.536, demonstrating that the ImageNet-pretrained visual representation captures more than half the variance in stellar population colour — a cross-domain correlation consistent with the Hubble morphology–colour sequence.

## Architecture

| Component | Method | Result |
|---|---|---|
| Backbone | DINOv2 ViT-B/14 fine-tuned | Balanced acc. = 0.839 |
| Fusion | DINOv2 + CAS/Gini/M₂₀ + SDSS photometry | Balanced acc. = **0.8631** |
| Segmentation | U-Net on Otsu pseudo-labels | mIoU = 0.938 |
| Uncertainty | Monte Carlo Dropout (T=30) | Calibrated ECE = 0.049 |
| Coverage | Conformal prediction (α=0.10) | 90.5% coverage, 91% singleton rate |

## Key Results

- **0.8631 balanced accuracy** on a 10-class galaxy morphology benchmark
- DINOv2 zero-shot (0.555) **underperforms** SimpleCNN (0.595) — domain gap; fine-tuning recovers +28.4%
- Morphometric descriptors (CAS/Gini/M₂₀) add complementary geometric information not encoded in the ViT CLS token
- SDSS photometry adds marginal gain due to implicit colour encoding in DINOv2 features
- The **Disturbed class recall ceiling (~0.53) is physically irreducible** — confirmed by highest MC Dropout entropy and conformal coverage (0.62 vs 0.90 target)
- U-Net trained on Otsu weak labels improves aggregate pseudo-label agreement (mIoU 0.904 → 0.938)

## Technical Stack

Python · PyTorch · DINOv2 · EfficientNet · UMAP · scikit-learn · astroquery · Weights & Biases

**Compute:** AMD Ryzen 9 5950X · NVIDIA RTX 5060 Ti 16GB · CUDA 12.8 · PyTorch 2.7

## Links

- 📁 [GitHub Repository](https://github.com/PhD-Brown/AstroVision)

*Manuscript in preparation. Preprint to be released on arXiv.*
