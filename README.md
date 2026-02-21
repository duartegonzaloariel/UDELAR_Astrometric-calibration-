🛰️ Astrometric Calibration with Neural Networks

This repository contains the source code for a neural-network–based astrometric calibration framework developed for all-sky camera systems within the BOCOSUR network.

The goal of this work is to map pixel coordinates from all-sky images to physical sky coordinates (azimuth and zenith) using deep learning models, providing a robust alternative to classical calibration methods, especially under optical distortions and multi-station configurations.


🔍 Overview

The calibration pipeline includes:

📊 Data preprocessing and feature engineering (e.g., cyclical encoding of angular variables)

🧹 Outlier and noise removal using DBSCAN clustering

🧠 Training and evaluation of neural network models
(dense, Bayesian dense, and convolutional architectures)

📈 Performance analysis for both single-station and multi-station datasets

The methodology is designed to be scalable and adaptable to different camera setups and observing conditions.


🔒 Data Availability

⚠️ The dataset used in this study is not included in this repository.

Due to access and ownership restrictions, the observational database cannot be publicly shared.

This repository provides only the code required to:

Preprocess compatible datasets

Train and evaluate the astrometric calibration models

Reproduce the methodology and workflow described in the associated scientific work, using external or private data with the same structure


📁 Repository Contents

Data preprocessing and feature construction scripts

DBSCAN-based filtering utilities

Neural network model definitions and training routines

Evaluation and visualization tools for calibration performance
