# mRNA-ribosome-model
Code for "The proportional scaling of mRNA and ribosome concentrations controls eukaryotic cell growth"

# Yeast Growth Modeling — Coupled Transcription–Translation Mass-Action Framework

## Overview
This repository contains two MATLAB Live Scripts implementing **mass-action based models** that quantitatively connect transcription and translation capacities to cell growth rate in *Saccharomyces cerevisiae* under different nutrient conditions.

The models link measured **RNAPII**, **mRNA**, and **ribosome** concentrations to the **active ribosome fraction** and overall **growth rate**, providing a mechanistic framework for how cell growth under different environments. All required datasets are included.

---

## Files

### 1. `RNAPII_transcription_model.mlx`
**Purpose:**  
Predict **mRNA concentration** from measured **RNAPII abundance** and **DNA accessibility** using a **mass-action transcription model**.

**Model concept:**  
RNAPII binds to DNA promoters according to an equilibrium constant (*Kd*), determining the bound fraction of polymerases actively transcribing.  
By fitting *Kd* from experimental RNAPII occupancy data, the model estimates the kinetic scaling factor (*para_km*) that links transcriptional capacity to mRNA output.

**Key features:**
- Integrates nuclear RNAPII level, nuclear volume fraction, and DNA content per cell.  
- Fits *Kd* via nonlinear regression (`fitnlm`) on bound-fraction data with 90% confidence intervals.  
- Predicts steady-state mRNA concentration normalized to spike-in RNA-seq data.  
- Generates publication-quality plots comparing experimental vs. predicted mRNA levels.

**Inputs required:**
- `growth&ribo data.mat` — growth rates and related parameters.  
- `color_rgb.mat` — color definitions for figure aesthetics.  
- `adjust_fig_nogrid.m` — optional helper for consistent figure styling.

---

### 2. `mRNA_ribosome_translation_model.mlx`
**Purpose:**  
Using measured **mRNA** and **ribosome** concentrations, this model applies a **mass-action steady-state formulation** to compute the **active ribosome fraction** (translation-competent pool).  
Assuming the **peptide elongation rate** is conserved, the model then infers **growth rate** as a function of translational capacity.

**Key features:**
- Fits mRNA and ribosome concentration scaling with growth rate (linear or Hill form).  
- Calculates active/inactive ribosome fractions and visualizes their contributions to total proteome.  
- Predicts growth rate from translational efficiency using a single conserved elongation rate constant.  
- Provides full figure generation with confidence intervals and experimental comparisons.

**Inputs required:**
- `growth&ribo data.mat` — growth rate, ribosome proteome fractions, active ribosome measurements.  
- `color_rgb.mat` — color palette for plots.  
- `lfst_ss_x.m` — steady-state solution for active ribosome fraction.  
- `adjust_fig_nogrid.m` — helper for clean figure output.

---

## Dependencies
- MATLAB R2020b or newer  
- Curve Fitting Toolbox  
- Statistics and Machine Learning Toolbox  
- All `.mat` data and helper functions must be in the MATLAB path.

---

## Usage
1. Clone or download this repository (<1min).  
2. Place all required `.mat` and helper `.m` files in the same folder.  
3. Open the Live Scripts in MATLAB:  
   - Run `RNAPII_transcription_model.mlx` to model transcriptional scaling (<1min).  
   - Run `mRNA_ribosome_translation_model.mlx` to model translational scaling (<1min).  
4. Each script will automatically reproduce figures for:
   - RNAPII–DNA binding and mRNA prediction  
   - Active/inactive ribosome partitioning  
   - Predicted vs. measured growth rate
5. All simulation figures in our paper can be reproducted by this code.
---

## Scientific Rationale
- **Transcription layer:**  
  Nuclear RNAPII concentration and DNA binding govern the initiation rate of mRNA synthesis.  

- **Translation layer:**  
  The active ribosome fraction depends on mRNA availability and total ribosome abundance.  
  The mass-action steady-state between free and bound ribosomes defines the *active ribosome fraction*, which, under a conserved elongation rate, directly predicts growth rate.

Together, these two models quantitatively bridge **transcriptional supply** and **translational demand**, revealing how yeast cells allocate resources to sustain balanced growth.


---

## Contact
**Author:** Xin Gao  
**Affiliation:** Department of Biology, Stanford University  
**Email:** gaox@stanford.edu
**Last updated:** October 2025
