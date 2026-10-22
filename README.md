# Geometry of a Nightingale Song

[![Project Status](https://img.shields.io/badge/status-experimental-orange.svg)](#)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](#)

## Overview

Geometry of a Nightingale Song is a research / analysis project that studies the structure of nightingale vocalizations using geometric and topological data-analysis techniques. The goal is to transform audio recordings of nightingale song into geometric representations (point clouds, manifolds, graphs), then analyze and visualize the structure, motifs, and variability using dimensionality reduction, graph/geodesic methods, and topological summaries.

This repository contains code, notebooks, scripts, and documentation to reproduce the analysis and visualizations, plus an accompanying video demonstration.

---

## Video Demonstration

[![Watch the demo video](https://img.youtube.com/vi/hlntM5h8w4s/maxresdefault.jpg)](https://youtu.be/hlntM5h8w4s)

Or link directly:
- Demo video: [Watch on YouTube](https://youtu.be/hlntM5h8w4s)

---

## Key Features

- Audio preprocessing and high-quality spectrogram generation
- Feature extraction (MFCCs, spectral features, pitch contours)
- Time-warping and alignment of song syllables
- Construction of k-NN graphs and geodesic-distance embeddings
- Dimensionality reduction (PCA, t-SNE, UMAP) for visual exploration
- Topological Data Analysis (persistent homology) to capture shape features
- Clustering and motif discovery
- Interactive notebooks and static visualizations
- Reproducible scripts for pipeline stages

---

## Motivation & Scientific Goals

Nightingale songs are rich with structure at multiple time scales: motifs, syllables, and long-range patterns. By mapping short audio segments to points in feature space we may reveal geometric structure (clusters, trajectories, loops) that correspond to song motifs, transitions, or performance variability. Topological measures can detect global organization (e.g., loops for cyclic patterns) that complements local cluster-based analysis.

Primary scientific questions:
- Do nightingale syllables populate low-dimensional manifolds?
- Can geometric/topological structure reveal song motifs and transitions?
- How stable are motifs across individuals or recording sessions?

---

## Dataset

This project expects collections of nightingale recordings (WAV or FLAC). Common sources:
- Xeno-canto (https://www.xeno-canto.org) — community-contributed bird recordings
- Macaulay Library (Cornell) — curated recordings with metadata

Organize your dataset under the `data/` folder:
- `data/raw/` — raw audio files (one WAV/FLAC per recording)
- `data/metadata.csv` — CSV with columns (filename, species, location, date, recorder, notes)

Note: This repository does not include copyrighted third-party recordings. Always respect licensing and attribution requirements from data providers.

---

## High-level Pipeline

1. Data ingestion and audio normalization
2. Segmentation: detect syllables/notes or process fixed windows
3. Feature extraction for each segment:
   - MFCCs, spectral centroid, bandwidth, rolloff
   - Pitch (F0) / fundamental frequency contours
   - Delta/delta-delta features or time-aggregated statistics
4. Optional DTW/time-warping to align motifs
5. Build point cloud (each segment = a point in feature space)
6. Construct k-NN graph and compute geodesic distances (Isomap-like)
7. Dimensionality reduction (PCA / UMAP / t-SNE) for visualization
8. Compute persistent homology (e.g., Vietoris–Rips) for topology
9. Cluster and annotate motifs
10. Produce figures, interactive plots, and video demo

---

## Typical File / Folder Layout

- data/
  - raw/
  - processed/
  - metadata.csv
- notebooks/
  - 01-data-prep.ipynb
  - 02-feature-extraction.ipynb
  - 03-geometry-embeddings.ipynb
  - 04-topology.ipynb
- src/
  - audio/
    - preprocess.py
    - segment.py
    - features.py
  - geometry/
    - knn_graph.py
    - embeddings.py
  - topology/
    - persistent_homology.py
  - viz/
    - plot_utils.py
- scripts/
  - run_preprocess.sh
  - run_full_pipeline.sh
- results/
  - figures/
  - video/
- requirements.txt
- environment.yml
- README.md

If your repository differs, please adapt the layout and the commands below.

---

## Installation

Recommended: use a conda environment.

Conda:
```bash
conda create -n nightingale python=3.10 -y
conda activate nightingale
conda install -c conda-forge ffmpeg jupyterlab nodejs -y
pip install -r requirements.txt
