---
layout: page
title: AstroSpectro
description: Interpretable ML pipeline for stellar spectral classification on LAMOST DR5 × Gaia DR3
img: assets/img/projects/astrospectro_preview.png
importance: 1
category: astrophysics
related_publications: false
---

## Overview

**AstroSpectro** is an open-source machine learning pipeline for automated stellar spectral classification, built on 43,019 spectra from the [LAMOST DR5](http://www.lamost.org/) survey cross-matched with [Gaia DR3](https://www.cosmos.esa.int/web/gaia/dr3) astrometric and photometric data.

The pipeline covers the full research workflow: data acquisition from raw FITS files, preprocessing and continuum normalization, physics-based feature engineering (183 spectroscopic descriptors), supervised classification, dimensionality reduction, clustering, and SHAP-based interpretability analysis.

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/projects/astrospectro_umap.png" title="UMAP projection of stellar spectra" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/projects/astrospectro_shap.png" title="SHAP feature importance" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Left: UMAP projection of 43,019 stellar spectra coloured by spectral class, showing clear morphological separation between stellar populations. Right: SHAP analysis revealing that metallicity-sensitive features (Ca II H&K, Mg b) systematically outrank Balmer temperature proxies as classification discriminants.
</div>

## Scientific Finding

A central result validated via SHAP analysis challenges a classical assumption in stellar classification: **metallicity-sensitive spectral features (Ca II H&K at 3933/3968 Å, Mg b at 5167–5183 Å) consistently rank above Balmer temperature proxies (Hα, Hβ, Hγ, Hδ) as discriminants of MK spectral class**.

This finding implies that stellar classification models trained on large heterogeneous surveys are primarily encoding metallicity and evolutionary state rather than photospheric temperature alone — a result with implications for the interpretation of ML-based classifiers applied to spectroscopic surveys such as LAMOST, SDSS, and the forthcoming 4MOST.

## Architecture

| Component | Method | Result |
|---|---|---|
| Feature extraction | 183 physics-based spectroscopic descriptors | `spectro_only=True` mode |
| Classifier | XGBoost (gradient boosting) | 87% balanced accuracy |
| ROC-AUC | Multi-class one-vs-rest | 0.964 |
| Dimensionality reduction | PCA, UMAP, Autoencoder | Trustworthiness > 0.95 |
| Clustering | HDBSCAN (20 clusters) | Physically interpretable |
| Interpretability | SHAP (TreeExplainer) | 97.9% physical features in top-30 |

## Key Results

- **87% balanced accuracy** on a 7-class stellar classification problem (OBAFGKM + QSO + Galaxy)
- **ROC-AUC = 0.964** (multi-class, macro-averaged)
- Removing non-physical metadata features (RA, Dec, redshift, instrument) *increased* performance — validating the physically grounded feature design
- F/G class confusion is physically irreducible (continuous stellar sequence) — confirmed by UMAP topology
- HDBSCAN clustering of the latent space recovers astrophysically meaningful stellar sub-populations

## Technical Stack

Python · XGBoost · PyTorch · UMAP · HDBSCAN · SHAP · Astropy · Weights & Biases · Docusaurus

**Compute:** AMD Ryzen 9 5950X · NVIDIA RTX 5060 Ti 16GB · CUDA 12.8 · PyTorch 2.7

## Links

- 📁 [GitHub Repository](https://github.com/PhD-Brown/AstroSpectro)
- 📖 [Full Documentation](https://phd-brown.github.io/AstroSpectro/)
- 📊 [W&B Experiment Tracking](https://wandb.ai) (85+ runs logged)

*Target venue: Astronomy & Astrophysics (A&A) or Monthly Notices of the Royal Astronomical Society (MNRAS).*
