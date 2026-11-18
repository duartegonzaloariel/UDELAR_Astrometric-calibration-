# 🛰️ Astrometric Calibration with Neural Networks

This repository contains the source code for the astrometric calibration framework developed for the all-sky cameras of the **BOCOSUR** network (Uruguay). It maps pixel coordinates on the detector to horizontal coordinates on the sky (azimuth and zenith angle), as a preliminary step to meteor and fireball trajectory reconstruction.

The method is **hybrid**: a classical geometric model is first fit to each calibration campaign, and a neural network is then trained to learn only the **residual, non-linear correction** to that fit.

---

## 🔍 Overview

The pipeline consists of three notebooks, run in order:

| Notebook | What it does |
|---|---|
| `01_ajuste_clasico_por_campana.ipynb` | Per-campaign classical geometric fit (free projection center, cubic radial polynomial, rotation, image parity and camera tilt) and removal of misidentified stars (records more than 60 arcmin from the fit). |
| `02_calibracion_red_single_multi.ipynb` | Fixed train/validation/test split (stratified by campaign), classical fit on the training split only, and training of the neural network on the residuals in the plane tangent to the sky. Runs in **single-station** mode (one station) or **multi-station** mode (all stations pooled, with one-hot station encoding). |
| `03_ensemble_todas_las_estaciones.ipynb` | Trains the single-station model for every station, combines it with the multi-station model in a weighted ensemble (weight chosen on validation), and runs bootstrap and control tests. Produces the network-wide tables and figures. |

**Neural network architectures:** dense, Bayesian dense and convolutional (1D, kernel size 1).

**Evaluation:** sky angular separation between predicted and catalogue directions (median, MAE, RMSE, P90), by station and by zenith distance, with paired bootstrap confidence intervals. All configurations are evaluated on exactly the same held-out test stars.

The method uses only the **measured pixel positions** and the **catalogue positions** of reference stars. It does not depend on any external calibration software.

---

## 📥 Input data format

A CSV table (`df_global.csv`) with one row per reference star:

| Column | Description |
|---|---|
| `station` | Station identifier |
| `año`, `mes` | Year and month of the calibration frame (define the calibration campaign) |
| `Posicion_X`, `Posicion_Y` | Measured pixel position of the star |
| `azimuth`, `altitude` | Catalogue horizontal coordinates of the star (degrees) |

---

## 🔒 Data Availability

⚠️ The dataset used in this study is **not included** in this repository.

Due to the data-sharing policies of the BOCOSUR network, the observational database cannot be publicly shared. Representative data samples can be provided by the corresponding author upon reasonable request.

This repository provides the code required to:

- Fit the per-campaign classical model and clean misidentified stars
- Train and evaluate the single-station, multi-station and ensemble calibration models
- Reproduce the methodology and workflow of the associated scientific work, using external or private data with the same structure

---

## ⚙️ Requirements

Python 3 with `numpy`, `pandas`, `scipy`, `scikit-learn`, `torch` and `matplotlib`. The notebooks were developed and run in Google Colab.

---

## 🤖 AI tools disclosure

Portions of the Python code in this repository were generated and reviewed with the assistance of AI tools (ChatGPT, GPT-5, OpenAI; and Claude, Anthropic). All code was executed, and all results were checked and interpreted, by the authors.
