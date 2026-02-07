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

Virtual Detectors and Post-Acquisition Imaging

In 4D-STEM, a full diffraction pattern is recorded at every probe scan position. This means that all scattered electron information is stored during acquisition, rather than being limited by a fixed physical detector geometry.

Virtual detectors allow post-acquisition imaging by digitally defining regions of interest in reciprocal space (such as a central disk for Bright Field or an annular region for Annular Dark Field). By integrating the diffraction intensity within these regions after data collection, different imaging modes can be reconstructed from the same dataset.

This approach enables flexible contrast generation (e.g., diffraction contrast in BF and Z-contrast in ADF) without re-acquiring data, and allows detector geometries to be optimized during data analysis rather than during the experiment.
