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
# Particle Detection and Segmentation  
### Classical vs Machine Learning vs Deep Learning Comparison

---

## Project Overview

This project implements and compares three different approaches for particle detection and segmentation:

1. **Classical Image Processing (Watershed)**
2. **Machine Learning (SVM, Random Forest, k-Means)**
3. **Deep Learning (CNN, U-Net)**

The objective is to evaluate performance, interpretability, runtime, and data requirements across methods.

---

# 1️⃣ Classical Pipeline (Watershed)

## Method
- Image enhancement
- Thresholding
- Morphological cleanup
- Distance transform
- Watershed segmentation
- Region property extraction

## Output
- `classical_results.csv`
- Four-panel visualization (input → threshold → distance → watershed)

## Metric
**Average particles per image:**  
`599.54`

## Strengths
- No labeled data required
- Highly interpretable
- Very fast

## Limitations
- Sensitive to threshold selection
- Performance degrades in noisy regions

---

# 2️⃣ Machine Learning (Region-Based Features)

## Feature Extraction

For each segmented region:

- Area  
- Perimeter  
- Equivalent diameter  
- Eccentricity  
- Solidity  
- Circularity  
- Mean / Std intensity  
- LBP texture features  

---

## Supervised Learning

### SVM
- **F1 Score:** `0.994`
- Fast
- Strong performance with engineered features

### Random Forest
- **F1 Score:** `1.000`
- Best ML performance
- Robust to feature variation

Outputs include:
- `ml_results.csv`
- Confusion matrices
- Feature importance ranking

---

## Unsupervised Learning (k-Means)

- k = 3
- **Silhouette Score:** `0.300`

Observations:
- Moderate cluster separation
- Lower interpretability compared to supervised methods

---

# 3️⃣ Deep Learning

---

## CNN (Image-Level Classification)

### Architecture
- Conv → BatchNorm → ReLU → MaxPool (×2)
- Dense layers
- Dropout
- Early stopping

### Training Setup
- 20 images
- 256×256 resolution
- Data augmentation
- Proxy labels

### Performance
- **F1 Score:** `0.857`

### Observations
- Works reasonably well with limited data
- Requires labeled data
- Lower interpretability than classical ML

---

## U-Net (Pixel-Level Segmentation)

### Architecture
- Encoder–decoder
- Skip connections
- Binary cross-entropy loss
- Dice and IoU evaluation

### Training Setup
- 20 images
- Pseudo segmentation masks
- 256×256 resolution

### Performance
- **Dice:** `0.607`
- **IoU:** `0.436`

### Outputs
- Training curves
- Segmentation comparisons
- Feature map visualizations
- Final 3×3 panel (300 DPI with scale bar)

---

# 📊 Final Comparison

| Method | Metric | Score | Labels Required | Interpretability | Runtime |
|--------|--------|-------|----------------|------------------|----------|
| Watershed (classical) | Avg particles/image | 599.54 | None | High | Fast |
| SVM (ML) | F1 | 0.994 | Region labels | Medium | Fast |
| Random Forest (ML) | F1 | 1.000 | Region labels | Med-High | Fast |
| k-Means (ML) | Silhouette (k=3) | 0.300 | None | Low-Med | Fast |
| CNN (DL) | F1 | 0.857 | Image labels | Low | Medium |
| U-Net (DL) | Dice / IoU | 0.607 / 0.436 | Pixel masks | Medium | Med-Slow |

---

# 🔍 Key Insights

- Classical watershed performs well when particles are clearly separated.
- Random Forest achieves the best overall performance with engineered features.
- CNN works but is limited by small dataset size.
- U-Net captures structure but needs more labeled data to outperform classical ML.
- With limited annotations, **feature-based ML is the most efficient solution**.

---

# 📁 Repository Contents

- `classical_results.csv`
- `ml_results.csv`
- `comparison_table.csv`
- Confusion matrices
- Clustering visualizations
- CNN training curves
- U-Net training curves
- Feature map visualizations
- `task3_final_3x3.png` (300 DPI with scale bar)

---

# 🏁 Recommendation

For small datasets:

→ **Random Forest with engineered features is the best trade-off.**

For large labeled datasets:

→ **U-Net segmentation provides the most scalable solution.**

---

