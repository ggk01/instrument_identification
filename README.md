# 🎶 Instrument Activation Detection with CRNN

## 🧠 Project Overview

This project focuses on **frame-level detection of musical instrument activations** in audio tracks. The task is **multi-label classification**, where multiple instruments may be active simultaneously at each time frame. The goal is to predict which instruments are active at any point in time during a song.

We use the **AAM Dataset**, a publicly available collection of `.wav` tracks and corresponding `.arff` files that contain segment-level annotations with ground truth instruments.

---

## 📁 Dataset

- **Dataset Used**: [Artificial Audio Multitracks (AAM)](https://zenodo.org/record/8040391)
- **Contents**:
  - `.wav` audio files for analysis and feature extraction.
  - `.arff` annotation files with segment-level instrument activity.
- **Preprocessing**:
  - Extraction of **Mel Spectrograms**.
  - Creation of frame-level multi-hot label matrices.
- **Ground Truth**:
  - Instrument labels per time frame obtained from the annotations.

We originally attempted to work with **MedleyDB**, but access limitations led us to opt for AAM instead.

---

## 🏗️ Model Architectures

We experimented with two core architectures:

### 🔹 Baseline: MLP (Multi-Layer Perceptron)
- Simple feed-forward model.
- Performs decently even with small datasets.
- Useful for benchmarking.

### 🔹 Proposed: CRNN (Convolutional Recurrent Neural Network)
- Combines CNNs for spectral pattern recognition and LSTMs for temporal modeling.
- Performs worse than MLP on low-data regimes.
- Outperforms MLP as the amount of training data increases.

---

## ⚖️ Class Imbalance Handling

- Observed rare classes (instruments that appear in very few tracks).
- Solutions applied:
  - **Oversampling** tracks with rare instrument classes.
  - **Weighted loss averaging**.

---

## 📊 Evaluation

We evaluated model performance both quantitatively and qualitatively.

### 🧮 Metrics
- **F1-Score** (Macro, Micro, Weighted)
- **Hamming Loss**
- **Jaccard Index**

### 🎨 Visual Inspection
- Per-track **frame-level visualization** of predictions vs. ground truth.
- Highlighting correct (green) and incorrect (red) predictions.
- Useful for spotting systematic errors per instrument.

---

## ❌ Confusion Analysis

- Identification of **instrument confusions**, especially for sonically overlapping instruments.
- Built confusion heatmaps to analyze model errors (e.g., Flute vs. Violin).

---

## 🚀 Future Work (as of June 12, 2025)

- **Expand training data** using the full AAM dataset or additional corpora.
- **Experiment with hyperparameter tuning** (e.g., learning rate, batch size, network depth).
- Explore **data augmentation** techniques.
- Try **attention-based** or **transformer-based** architectures for improved temporal modeling.

---

## 🔧 Requirements

- Python ≥ 3.9
- PyTorch
- Librosa
- Plotly
- Scikit-learn
- Pandas

---
