---
layout: page
title: AstroVision
description: Deep-learning pipeline for galaxy morphological classification with multi-modal fusion and uncertainty quantification
img: assets/img/projects/astrovision_preview.png
importance: 2
category: work
related_publications: false
---

## Overview

**AstroVision** is an open-source deep-learning project for galaxy morphological classification. The project explores how modern computer-vision models, especially self-supervised visual foundation models, can be adapted to astronomical imaging data.

The current pipeline is built around the [Galaxy10 DECaLS](https://zenodo.org/record/10845026) dataset, containing 17,736 RGB galaxy images across ten morphology classes derived from the Dark Energy Camera Legacy Survey (DECaLS). The project compares several modelling strategies, including a simple convolutional neural network, EfficientNet-B0, DINOv2 visual features, fine-tuned DINOv2 representations, and late-fusion models combining image features with non-parametric morphology and photometric information.

The broader goal of AstroVision is not only to classify galaxies, but to understand what physical information is encoded in learned visual representations.

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/projects/astrovision_confusion.png" title="Confusion matrix — late-fusion classifier" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/projects/astrovision_umap.png" title="UMAP of DINOv2 feature space" class="img-fluid rounded z-depth-1" %}
  </div>
</div>

<div class="caption">
  Left: Confusion matrix for the best late-fusion classifier, highlighting which galaxy morphologies are reliably recovered and which remain ambiguous. Right: UMAP projection of the DINOv2 feature space, coloured by photometric information, showing that visual representations partly organise galaxies along physically meaningful trends.
</div>

## Scientific Motivation

Galaxy morphology is closely connected to stellar populations, star-formation history, colour, environment, and dynamical evolution. A central question in AstroVision is whether deep visual representations trained outside astronomy can still capture physically meaningful structure when applied to galaxy images.

The current results suggest that DINOv2 representations encode more than low-level image texture. In particular, principal components of the learned feature space correlate with non-parametric morphology indicators such as Gini and with photometric colour such as \(g-r\). This suggests that self-supervised visual features may partially recover the classical relationship between morphology and stellar population colour.

Rather than treating the model as a black-box classifier, AstroVision uses dimensionality reduction, morphometric diagnostics, photometric correlations, and uncertainty estimation to interpret what the network is learning.

## Pipeline

| Stage | Description |
|---|---|
| Image classification | Baseline CNN, EfficientNet-B0, DINOv2 probing, and DINOv2 fine-tuning |
| Representation learning | Analysis of high-dimensional DINOv2 visual embeddings |
| Morphometrics | CAS, Gini, \(M_{20}\), and related non-parametric galaxy structure descriptors |
| Photometry | SDSS photometric features used for comparison and late-fusion experiments |
| Fusion model | Combination of visual, morphometric, and photometric features |
| Uncertainty | Monte Carlo Dropout and conformal prediction for reliability analysis |
| Segmentation | Weakly supervised U-Net experiments based on Otsu pseudo-labels |

## Current Results

Current experiments show that:

- fine-tuning DINOv2 substantially improves performance over zero-shot visual probing;
- late fusion of visual embeddings, morphometric descriptors, and photometric information gives the strongest classification results;
- some classes, such as smooth and edge-on galaxies, are recovered more reliably than visually ambiguous or disturbed systems;
- the disturbed class remains difficult, suggesting that part of the error is tied to genuine morphological ambiguity rather than only model weakness;
- DINOv2 features show measurable correlations with both morphology and colour, suggesting that the learned visual representation contains physically relevant information.

This makes AstroVision a complementary project to AstroSpectro: both projects ask how machine-learning models organise astrophysical data, and whether their internal representations can be connected back to physical structure.

## Technical Stack

Python · PyTorch · DINOv2 · EfficientNet · scikit-learn · UMAP · astroquery · Weights & Biases

## Links

- 📁 [GitHub Repository](https://github.com/PhD-Brown/AstroVision)

*Status: active research and development project. The current focus is on improving robustness, uncertainty calibration, physical interpretation of learned representations, and preparation of a reproducible public release.*