# Volumetric 3D Crop Generator for Deep Learning Training

A tool for generating 3D training crops from large-scale light microscopy datasets (confocal and light-sheet), designed for deep learning segmentation workflows such as StarDist 3D and U-Net.

**No programming knowledge required to use the interactive GUI.**

---

## Background

Training a deep learning segmentation model on volumetric microscopy data requires small, meaningful 3D crops — not blank regions, and ideally from areas containing relevant biological signal. This repository provides two tools for this purpose, developed and used as part of a lab-wide segmentation pipeline for cochlear light-sheet and confocal microscopy datasets.

---

## Contents

### `Crop_n5_PyQt5.py` ⟵ *Current recommended tool*

An interactive PyQt5 GUI for manual crop selection from large `.n5` / `.zarr` datasets.

**Key features:**
- Supports both **fused** and **tiled** n5 datasets
- Loads large volumetric datasets memory-efficiently using **Dask** — no need to load the full dataset into RAM
- Visualizes data interactively in a **Napari** viewer
- Fully interactive GUI — select channel, downsample factor, crop dimensions (X, Y, Z), and region of interest without writing any code
- Draw a rectangle directly on the Napari viewer to define the spatial crop region
- Automatically generates matching crops across **all selected channels** and saves them
- Handles multi-tile and multi-channel dataset structures

**Workflow:**
1. Launch the GUI
2. Select your `.n5` dataset folder (fused or tiled)
3. Choose reference channel and setup ID
4. Select downsample factor for visualization
5. View data in Napari — either randomized single stack or full dataset
6. Set crop dimensions (X, Y, Z) using spinboxes
7. Draw rectangle on Napari viewer to select region of interest
8. Select output folder and filename
9. Click Crop — crops are saved automatically across all selected channels

**Requirements:**
```
napari
dask
zarr
PyQt5
numpy
imageio
natsort
```

---

### `LoadAndCropImage.py` ⟵ *Earlier pipeline version*

An automated random crop generator for `.ome.tif` datasets with content-based filtering.

- Prompts user to select a reference channel
- Generates random 3D crops across the dataset
- Filters out blank/empty crops using **entropy filtering**, **Otsu thresholding**, and binary morphological checks
- Only saves crops where non-empty signal exceeds a threshold (default: 12% of crop area)
- Configurable crop dimensions (X, Y, Z) and number of crops per dataset

> Note: This script was the earlier version of the pipeline, developed for `.ome.tif` datasets. For `.n5` datasets and interactive region selection, use `Crop_n5_PyQt5.py`.

---

## Context

These tools were developed as part of a lab-wide deep learning segmentation pipeline for large-scale cochlear microscopy datasets. The cropping workflows were used to generate training data for StarDist 3D and U-Net based segmentation models, ultimately deployed across 10+ researchers.

---

## Author

Anupriya Thirumalai  
[LinkedIn](https://www.linkedin.com/in/anupriyathirumalai/) | [Email](mailto:anupriya.thirumalai@example.com)
