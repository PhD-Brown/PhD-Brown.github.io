---
layout: page
title: ξ Dark Energy · BAO MCMC
description: Bayesian MCMC analysis comparing dark energy models using Pantheon+SH0ES supernovae and DESI DR2 BAO data
img: assets/img/projects/xi_bao_preview.png
importance: 3
category: work
related_publications: false
---

## Overview

**ξ Dark Energy · BAO MCMC** is an independent exploratory project in computational cosmology. The project implements a Bayesian Markov Chain Monte Carlo workflow to compare several dark-energy parameterisations using Type Ia supernovae and baryon acoustic oscillation data.

The analysis combines the [Pantheon+SH0ES](https://pantheonplussh0es.github.io/) supernova compilation with [DESI DR2](https://www.desi.lbl.gov/) BAO measurements. The goal is not to claim evidence for new physics, but to build a transparent and reproducible inference pipeline for testing how different dark-energy models behave under current observational constraints.

Three model families are considered:

| Model | Description | Parameters |
|---|---|---|
| **ΛCDM** | Cosmological constant baseline | \(\Omega_m, H_0\) |
| **CPL** | Chevallier–Polarski–Linder evolving equation of state | \(\Omega_m, H_0, w_0, w_a\) |
| **Ξosc** | Exploratory oscillating dark-energy parameterisation | \(\Omega_m, H_0, \epsilon, \omega_{\mathrm{osc}}\) |

## Scientific Motivation

The standard ΛCDM model remains highly successful, but current cosmology is increasingly shaped by precision tensions, model comparison, and the need for transparent statistical workflows. This project explores how alternative dark-energy parameterisations behave when fitted to combined supernova and BAO distance measurements.

The oscillating dark-energy model is treated as a deliberately exploratory extension. The goal is to test the inference pipeline, inspect posterior structure, and identify which modelling assumptions matter most before making stronger physical claims.

## Methodology

The inference workflow uses `emcee`, an affine-invariant ensemble MCMC sampler, to explore posterior distributions over cosmological parameters. The likelihood combines:

- **Type Ia supernovae:** distance modulus \(\mu(z)\), computed from the luminosity distance \(d_L(z)\), using the Pantheon+SH0ES covariance matrix;
- **BAO measurements:** distance-ratio observables compared against DESI DR2 BAO constraints;
- **Model comparison:** AIC and BIC are used as first-order criteria to penalise additional model complexity.

The project includes diagnostic plots, posterior summaries, corner plots, reproducibility scripts, and explicit documentation of known limitations.

## Current Results

The current exploratory release suggests that:

- ΛCDM and CPL remain consistent with the combined distance data;
- the oscillating model can produce a marginal preference for a non-zero oscillation amplitude, but this is not sufficient to claim detection;
- posterior asymmetries make median-based summaries more robust than relying only on means;
- the apparent preference for the oscillating component is sensitive to modelling assumptions and prior boundaries;
- a more self-consistent treatment is required before the model can be interpreted physically.

The project is therefore best understood as a reproducible computational-cosmology experiment rather than a finished cosmological result.

## Known Limitations

The `v0.1.0-exploratory` release explicitly documents several limitations that must be addressed in future versions:

1. **Fixed reference cosmology for \(t(z)\) mapping**  
   The oscillating model currently uses a reference mapping that can introduce a self-consistency bias.

2. **Boundary prior on \(\epsilon\)**  
   The preference for non-zero oscillation amplitude is statistically fragile because of one-sided prior truncation.

3. **Fixed sound horizon \(r_d\)**  
   The current treatment implicitly imports external information and does not yet provide a fully self-consistent BAO analysis.

These limitations are intentionally documented because they are part of the scientific value of the project: the pipeline is designed to expose where an exploratory model becomes statistically or physically fragile.

## Technical Stack

Python · emcee · NumPy · SciPy · Astropy · Matplotlib · corner

## Links

- 📁 [GitHub Repository](https://github.com/PhD-Brown/xi-dark-energy-bao-mcmc)
- 🏷️ [Release v0.1.0-exploratory](https://github.com/PhD-Brown/xi-dark-energy-bao-mcmc/releases/tag/v0.1.0)

*Status: exploratory computational cosmology project. A future version will focus on improving model self-consistency, prior treatment, BAO modelling, and convergence diagnostics.*