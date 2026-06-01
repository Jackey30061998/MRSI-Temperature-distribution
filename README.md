# MRSI-Temperature-distribution
MATLAB pipeline for reconstruction, spectral analysis, LCModel fitting, and brain temperature mapping of 7T SLOW-EPSI MRSI data acquired at the Otto von Guericke University Magdeburg (OVGU).

# Mapping Cerebral Temperature Distributions using 7T MR Spectroscopic Imaging (MRSI)

## Overview

This repository contains the MATLAB code developed during my Master's Thesis in Medical Systems Engineering at the **Otto von Guericke University Magdeburg (OVGU)**.

The project focuses on the reconstruction, processing, simulation, and analysis of **7 Tesla MR Spectroscopic Imaging (MRSI)** data acquired using a **SLOW-EPSI (Echo Planar Spectroscopic Imaging)** sequence for non-invasive brain temperature mapping.

Temperature estimation is based on the **Proton Resonance Frequency (PRF) shift** between water and metabolite resonances (primarily NAA).

---

## Thesis Objectives

* Reconstruction of raw Siemens TWIX MRSI data
* Sorting of acquisition data into multidimensional k-space
* Odd-even echo correction, phase correction
* Coil combination using water reference data
* Spectral reconstruction and processing
* Simulation of custom RF pulses and sequence behavior of SLOW pulse sequence developed by Dr. Weng (DOI: 10.1002/mrm.29220)
* Generation of LCModel-compatible basis datasets using FID-A toolkit (https://github.com/CIC-methods/FID-A/tree/master/simulationTools) - a simulation was adapted from the MEGA simulation which was already found in the toolkit, the runskript was also adapted accordingly
* Brain temperature estimation from spectroscopic data
* Visualization of cerebral temperature distributions

---

## Data Acquisition

The MRSI datasets were acquired at the **7 Tesla MRI facility of the Otto von Guericke University Magdeburg (OVGU), Germany**.
The adaptation of the new SLOW-EPSI pulse sequences was done by Prof. Mattern with help of the original developer Dr. Weng and the MTR assistants in the Research group in Magdeburg. For further information please contact these people.

Example datasets include:

* High-resolution SLOW-EPSI acquisitions
* Low-resolution SLOW-EPSI acquisitions
* Phantom measurements
* External Siemens Prisma datasets for comparison (from University in Bern, by Dr. Weng)

---

# Repository Structure

## pipeline4.mlx

Main reconstruction and processing pipeline.

### Features

* Import Siemens TWIX raw data using `mapVBVD_Gannet`
* Sort raw acquisitions into multidimensional k-space `partially by Dr.Weng` 
* Handle repeated acquisitions
* Correct odd-even echo inconsistencies
* Perform spectral and spatial Fourier transforms `with help of Dr. Weng and Prof. Mattern`
* Generate metabolite and water images
* Save intermediate reconstruction results
* LCModel fitting using simulated Basisspektra `FID-A Master`
* Prepare data for spectral fitting and temperature calculation
  

### Input

* Siemens `.dat` raw data files

### Output

* Reconstructed MRSI datasets
* Metabolite spectra
* Water spectra
* Temperature maps

---

## weng_create_csap_full.m

Generates a full-passage **CSAP (Complex Secant Adiabatic Pulse)** RF pulse waveform.

### Features

* Hyperbolic secant RF pulse generation
* Amplitude and phase modulation
* Instantaneous frequency analysis
* Export of Siemens-compatible `.pta` pulse files

### Output

* `CSAP_DrWeng_full.pta`

---

## weng_create_csap_par.m

Generates a partial-passage CSAP RF pulse waveform used for the SLOW-EPSI sequence.

### Features

* Partial adiabatic pulse design
* Amplitude and phase modulation
* RF trajectory visualization
* Siemens `.pta` pulse export

### Output

* `CSAP2DrWeng_par.pta`

---

## sim_slowepsi_shaped.m

Simulation engine for shaped RF pulse experiments.

Based on the FID-A simulation framework originally developed by Jamie Near.

### Features

* Density matrix simulations
* Shaped RF pulse modeling
* Spatially resolved simulations
* Gradient effects
* Metabolite spin-system simulation

### Applications

* Sequence verification
* RF pulse optimization
* Basis-set generation

---

## run_simSLOWEpsiShaped.m

Simulation wrapper used to execute complete SLOW-EPSI sequence simulations.

### Features

* Spatially resolved simulations
* Parallel processing support
* Phase cycling
* Metabolite-specific simulations
* Generation of synthetic spectra

### Typical Use

Used to generate simulated spectra for:

* NAA
* Creatine
* Choline
* Glutamate
* Glutamine
* GABA
* Water

and other metabolites required for spectral fitting.

---

# Methods

## Reconstruction Workflow

1. Siemens TWIX Import
2. k-space Sorting
3. Duplicate Acquisition Handling
4. Odd-Even Echo Correction
5. Fourier Transformation
6. Coil Combination
7. Spectral Processing
8. Peak Detection
9. Temperature Calculation
10. Visualization

---

## Temperature Estimation

Brain temperature is estimated using the chemical shift difference between water and NAA resonances:

[
T = 37 + \frac{\Delta ppm - 1.565}{-0.01}
]

where

* ( \Delta ppm ) = chemical shift difference between water and NAA
* ( T ) = estimated temperature in °C

---

# Software Requirements

* MATLAB R2023a or newer
* FID-A Toolbox
* mapVBVD / mapVBVD_Gannet
* Signal Processing Toolbox
* Parallel Computing Toolbox (optional)
* LCModel (optional)

---

# Author

**Jackey Junxian Chen**

M.Sc. Medical Systems Engineering

Otto von Guericke University Magdeburg

Master's Thesis:
**Mapping Cerebral Temperature Distributions using MR Spectroscopic Imaging (MRSI) at 7 Tesla**

---

# Disclaimer

This code was developed for research purposes as part of a master's thesis. It is provided without warranty and should not be used for clinical decision making.
