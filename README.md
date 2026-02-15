# MATSCI465_KittichatWiratkapun
# MATSCI465 – Assignment 01

This repository contains Assignment 01 for MATSCI 465 (Advanced Electron Microscopy).

## Environment
- Python 3.10
- NumPy
- SciPy
- Matplotlib
- HyperSpy

The notebook was run locally using Anaconda on Windows.

# MATSCI465 – Assignment 02
Virtual Detectors and Post-Acquisition Imaging

In 4D-STEM, a full diffraction pattern is recorded at every probe scan position. This means that all scattered electron information is stored during acquisition, rather than being limited by a fixed physical detector geometry.

Virtual detectors allow post-acquisition imaging by digitally defining regions of interest in reciprocal space (such as a central disk for Bright Field or an annular region for Annular Dark Field). By integrating the diffraction intensity within these regions after data collection, different imaging modes can be reconstructed from the same dataset.

This approach enables flexible contrast generation (e.g., diffraction contrast in BF and Z-contrast in ADF) without re-acquiring data, and allows detector geometries to be optimized during data analysis rather than during the experiment.

# MATSCI465 – Assignment 03&04
Particle Detection and Segmentation: Classical vs ML vs Deep Learning
Overview

This project implements and compares three pipelines for particle detection and segmentation:

Classical image processing (Watershed)

Machine Learning (SVM, Random Forest, k-Means)

Deep Learning (CNN classification, U-Net segmentation)

The goal is to evaluate trade-offs between accuracy, interpretability, runtime, and data requirements.

1️⃣ Classical Pipeline (Watershed)
Method

Image enhancement (contrast normalization)

Thresholding

Morphological operations

Distance transform

Watershed segmentation

Region property extraction

Output

classical_results.csv

Four-panel visualization (input → threshold → distance → watershed)

Metric

Average particles per image:
599.54

Strengths

No labeled data required

High interpretability

Very fast

Limitations

Sensitive to threshold choice

Struggles with noisy backgrounds

2️⃣ Machine Learning (Region-Based)
Feature Extraction

For each detected region:

area

perimeter

equivalent diameter

eccentricity

solidity

circularity

mean / std intensity

LBP texture features

Supervised Models
SVM

F1 Score: 0.994

Fast

Works well with engineered features

Random Forest

F1 Score: 1.000

Best classical ML performance

High robustness

Confusion matrices and clustering visualizations included.

Unsupervised (k-Means)

k = 3

Silhouette score: 0.300

Clusters partially separate feature space but less interpretable than supervised models.

3️⃣ Deep Learning
CNN (Image-Level Classification)

Architecture:

Conv → BN → ReLU → MaxPool (×2)

Dense layers

Early stopping

Training:

20 images (proxy labels)

256 px resolution

Data augmentation

F1 Score: 0.857

Observations:

Performs reasonably with limited data

Lower interpretability than classical ML

U-Net (Pixel-Level Segmentation)

Architecture:

Encoder–decoder

Skip connections

BCE loss

Dice + IoU evaluation

Training:

20 images

Pseudo masks

256 px resolution

Results

Dice: 0.607

IoU: 0.436

Outputs include:

Training curves

Segmentation overlays

Feature map visualization

Final 3×3 comparison collage (300 DPI with scale bar)

📊 Final Comparison
Method	Metric	Performance	Labels Required	Interpretability	Runtime
Watershed	Avg particles	599.54	None	High	Fast
SVM	F1	0.994	Region labels	Medium	Fast
Random Forest	F1	1.000	Region labels	Med-High	Fast
k-Means	Silhouette	0.300	None	Low-Med	Fast
CNN	F1	0.857	Image labels	Low	Medium
U-Net	Dice / IoU	0.607 / 0.436	Pixel masks	Medium	Med-Slow
🧠 Key Insights

Classical watershed is strong when objects are well separated.

Feature-based ML (especially Random Forest) performs extremely well with engineered features.

CNN classification works but needs more data for robustness.

U-Net segmentation improves structure understanding but requires larger labeled datasets for optimal performance.

With limited training data (20 images), region-based ML outperforms deep learning.
