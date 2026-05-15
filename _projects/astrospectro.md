---
layout: page
title: AstroSpectro
description: Interpretable ML pipeline for stellar spectral classification on LAMOST DR5 × Gaia DR3
img: assets/img/projects/astrospectro_preview.png
importance: 1
category: work
related_publications: false
---

## Overview

**AstroSpectro** is an open-source research project at the intersection of stellar spectroscopy, machine learning, and astronomical survey analysis. The project focuses on building physically grounded and interpretable pipelines for analysing large collections of stellar spectra, using data from [LAMOST DR5](http://www.lamost.org/) cross-matched with [Gaia DR3](https://www.cosmos.esa.int/web/gaia/dr3).

The current pipeline works on a cleaned dataset of more than 43,000 spectra and combines raw FITS ingestion, preprocessing, continuum normalisation, physics-based feature extraction, supervised classification, dimensionality reduction, clustering, and SHAP-based interpretability. Rather than treating classification accuracy as the final objective, AstroSpectro is designed to ask a broader scientific question:

> What physical information is actually being learned from stellar spectra by modern machine-learning models?

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/projects/astrospectro_umap.png" title="UMAP projection of stellar spectra" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/projects/astrospectro_shap.png" title="SHAP feature importance" class="img-fluid rounded z-depth-1" %}
  </div>
</div>

<div class="caption">
  Left: UMAP projection of the stellar spectral feature space, showing structured separation between stellar populations. Right: SHAP interpretability analysis highlighting the relative importance of metallicity-sensitive and temperature-sensitive spectral features.
</div>

## Scientific Motivation

Classical stellar classification is historically built around the visual strength of spectral lines, especially the Balmer sequence as a temperature indicator. In large survey datasets, however, machine-learning models may learn a more complex combination of temperature, metallicity, surface gravity, evolutionary state, and survey selection effects.

AstroSpectro explores this question by extracting physically motivated spectroscopic descriptors and testing which features actually drive classification decisions. A central result of the current pipeline is that metallicity-sensitive features, including Ca II H&K and Mg b, often rank above Balmer-line temperature proxies in SHAP-based feature importance analyses.

This does not replace the classical MK framework. Instead, it suggests that data-driven classifiers trained on large heterogeneous surveys may encode stellar population structure in ways that are not reducible to temperature alone.

## Pipeline

| Stage | Description |
|---|---|
| Data acquisition | Robust download and management of LAMOST DR5 FITS spectra |
| Catalogue construction | FITS-header metadata extraction and Gaia DR3 cross-matching |
| Preprocessing | Wavelength reconstruction, flux normalisation, inverse-variance cleaning |
| Feature engineering | Physics-based spectroscopic descriptors: Balmer lines, metallic lines, molecular bands, continuum indices, line profiles |
| Supervised learning | XGBoost and related classifiers for stellar spectral classification |
| Dimensionality reduction | PCA, UMAP, t-SNE, and autoencoder-based latent-space exploration |
| Interpretability | SHAP analysis to connect model decisions back to physical spectral features |

## Current Results

Current experiments show that:

- physically motivated spectral features can recover strong classification performance without relying on instrumental or positional metadata;
- dimensionality-reduction methods reveal a structured spectral manifold consistent with known stellar-population gradients;
- SHAP analysis identifies both expected features, such as Balmer lines, and less obvious discriminants, such as metallicity-sensitive Ca and Mg features;
- removing potentially leaky or non-physical metadata improves the scientific interpretability of the model;
- F/G/K transitions appear as continuous structures in the learned representation rather than sharply separated categories.

These results support the main goal of the project: developing a workflow where machine learning is not only predictive, but also interpretable in terms of stellar astrophysics.

## Technical Stack

Python · Astropy · NumPy · pandas · scikit-learn · XGBoost · PyTorch · UMAP · HDBSCAN · SHAP · Weights & Biases · Docusaurus

## Links

- 📁 [GitHub Repository](https://github.com/PhD-Brown/AstroSpectro)
- 📖 [Full Documentation](https://phd-brown.github.io/AstroSpectro/)
- 📊 Experiment tracking with Weights & Biases

*Status: active research and development project. The current focus is on scientific validation, interpretability, dimensionality reduction, and preparation of reproducible research outputs.*