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

**ξ Dark Energy · BAO MCMC** is an independent exploratory project in computational cosmology, applying Bayesian Markov Chain Monte Carlo (MCMC) inference to constrain dark energy model parameters using two independent datasets: the [Pantheon+SH0ES](https://pantheonplussh0es.github.io/) Type Ia supernova compilation and the [DESI DR2](https://www.desi.lbl.gov/) Baryon Acoustic Oscillation (BAO) measurements.

Three dark energy models are compared:

| Model | Description | Parameters |
|---|---|---|
| **ΛCDM** | Cosmological constant | Ω_m, H₀ |
| **CPL** | Chevallier-Polarski-Linder | Ω_m, H₀, w₀, wₐ |
| **Ξosc** | Oscillating dark energy | Ω_m, H₀, ε, ω_osc |

## Methodology

The analysis uses `emcee` (affine-invariant ensemble MCMC sampler) to explore the posterior distributions of cosmological parameters. The likelihood function combines:

- **Type Ia supernovae:** distance modulus μ(z) computed from the luminosity distance d_L(z), with Pantheon+SH0ES covariance matrix
- **BAO:** ratio d_V(z)/r_d compared to DESI DR2 measurements at 7 effective redshifts

Model comparison uses the Akaike Information Criterion (AIC) and Bayesian Information Criterion (BIC) to penalize model complexity.

## Known Limitations

This project is released as `v0.1.0-exploratory` with explicit documentation of its technical limitations:

1. **Fixed reference cosmology for t(z) mapping** — introduces a self-consistency bias in the oscillating dark energy model
2. **Boundary prior on ε** — the ~2.26σ preference for non-zero oscillation amplitude is statistically fragile due to one-sided prior truncation
3. **Fixed sound horizon r_d** — implicitly imports a CMB constraint, breaking full BAO self-consistency

These limitations are documented in the repository and will be addressed in v0.2.

## Results

- ΛCDM and CPL remain consistent with current data
- Ξosc shows a marginal (~2.26σ) preference for non-zero oscillation amplitude — insufficient to claim detection given the prior boundary effects
- Posterior distributions are well-sampled (convergence confirmed via Gelman-Rubin diagnostic)
- Median preferred over mean for skewed posterior distributions

## Technical Stack

Python · emcee · NumPy · SciPy · Matplotlib · corner · Astropy

## Links

- 📁 [GitHub Repository](https://github.com/PhD-Brown/xi-dark-energy-bao-mcmc)
- 🏷️ [Release v0.1.0-exploratory](https://github.com/PhD-Brown/xi-dark-energy-bao-mcmc/releases/tag/v0.1.0)

*This is an independent exploratory project. A v0.2 correcting the self-consistency bias and prior issues is planned.*
