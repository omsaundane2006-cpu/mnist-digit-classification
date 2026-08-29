# Handwritten Digit Classification — MNIST

> **AI Internship Program Submission**
> | | |
> |---|---|
> | **Submitted by** | Om Raju Saundane |
> | **Program / Organization** | AI Internship Program |

A machine learning project that classifies handwritten digits (0–9) from the MNIST dataset using two neural network architectures — a fully-connected **Artificial Neural Network (ANN)** and a **Convolutional Neural Network (CNN)** — and compares their performance.

![Sample digits](assets/digit_samples.png)

---

## Table of Contents

- [Overview](#overview)
- [Project Structure](#project-structure)
- [Dataset](#dataset)
- [Models](#models)
- [Installation](#installation)
- [Usage](#usage)
- [Results](#results)
- [Evaluation Metrics](#evaluation-metrics)
- [Tech Stack](#tech-stack)
- [Future Work](#future-work)
- [Resources](#resources)
- [License](#license)

---

## Executive Summary

This project was completed as part of an AI internship program to demonstrate practical, end-to-end machine learning skills: data preprocessing, model design, training, evaluation, and technical documentation.

Two neural network architectures were built and compared on the MNIST handwritten digit dataset — a fully-connected ANN (baseline) and a CNN (upgraded). The CNN outperformed the ANN by learning spatial features directly from the pixel grid, illustrating a core computer vision principle: architecture choice matters as much as raw model capacity. The project includes reproducible notebooks, a written report, an evaluation pipeline (confusion matrix, per-class metrics, error analysis), and a presentation deck summarizing the work.

**Skills demonstrated:** Python, TensorFlow/Keras, neural network design (ANN & CNN), model evaluation, data visualization, technical writing, and project documentation.

## Overview

Handwritten digits vary widely in size, slant, thickness, and style. This project builds and trains neural networks that learn general visual patterns for each digit class rather than memorizing individual images.

**Objective:** Build and compare two neural network models that classify a 28×28 pixel digit image into one of 10 classes (0–9).

| | |
|---|---|
| **Task** | Multi-class image classification |
| **Dataset** | MNIST (60,000 train / 10,000 test images) |
| **Models** | ANN (baseline) and CNN (upgraded) |
| **Frameworks** | TensorFlow / Keras |

---

## Project Structure

```
MNIST_Digit_Classification_Project/
│
├── README.md                              # This file
├── requirements.txt                       # Python dependencies
│
├── notebooks/
│   ├── 01_ANN_MNIST_Classification.ipynb  # Fully-connected ANN baseline
│   └── 02_CNN_MNIST_Classification.ipynb  # Convolutional Neural Network
│
├── src/
│   └── quick_start_demo.py                # Runnable, dependency-light demo (no internet needed)
│
├── docs/
│   ├── PROJECT_REPORT.md                  # Full written report: methodology, implementation, results
│   └── METHODOLOGY.md                     # Pipeline & architecture details
│
├── presentation/
│   └── MNIST_Digit_Classification.pptx    # 12-slide project presentation
│
└── assets/
    ├── digit_samples.png                  # Sample digit images used in docs/slides
    └── quick_start_demo_results.png       # Output of the quick-start demo script
```

---

## Dataset

**MNIST** (Modified National Institute of Standards and Technology) is the standard benchmark dataset for handwritten digit recognition.

| Property | Value |
|---|---|
| Training images | 60,000 |
| Test images | 10,000 |
| Image size | 28 × 28 pixels, grayscale |
| Pixel range | 0 (black) – 255 (white), normalized to 0–1 |
| Classes | 10 (digits 0–9) |

The full notebooks (`notebooks/`) load MNIST directly via `tensorflow.keras.datasets.mnist`, which requires an internet connection on first run. The `src/quick_start_demo.py` script uses scikit-learn's built-in 8×8 digit dataset instead, so it runs fully offline with no download.

---

## Models

### 1. Artificial Neural Network (ANN) — Baseline

```
Input (28×28)
  → Flatten → 784 values
  → Dense(128, ReLU) → Dropout(0.2)
  → Dense(64, ReLU)  → Dropout(0.2)
  → Dense(10, Softmax)
```

Treats the image as a flat list of 784 pixel values — no spatial awareness.

### 2. Convolutional Neural Network (CNN) — Upgraded

```
Input (28×28×1)
  → Conv2D(32, 3×3, ReLU) → MaxPooling2D(2×2)
  → Conv2D(64, 3×3, ReLU) → MaxPooling2D(2×2)
  → Flatten → Dense(128, ReLU) → Dropout(0.3)
  → Dense(10, Softmax)
```

Learns spatial patterns (edges, curves, strokes) directly from the pixel grid via convolution and pooling — the standard approach for image data.

---

## Installation

```bash
# 1. Clone or download this project, then move into it
cd MNIST_Digit_Classification_Project

# 2. (Recommended) create a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt
```

---

## Usage

### Run the full notebooks (requires internet, for MNIST download)

```bash
jupyter notebook notebooks/01_ANN_MNIST_Classification.ipynb
jupyter notebook notebooks/02_CNN_MNIST_Classification.ipynb
```

Or open either notebook directly in [Google Colab](https://colab.research.google.com/) — both are Colab-ready.

### Run the offline quick-start demo (no internet required)

```bash
python src/quick_start_demo.py
```

This trains an MLP and an SVM on scikit-learn's built-in digit dataset and saves a results chart to `quick_start_demo_results.png`. It's a fast way to confirm your environment is working before running the full MNIST notebooks.

---

## Results

Typical MNIST test-set performance for each architecture:

| Model | Test Accuracy |
|---|---|
| ANN (Dense) | ~97.8% |
| CNN (Conv2D) | ~99.2% |

> **Note:** These are typical published benchmark figures for these architectures, provided as a reference target. Run the notebooks yourself and record your own test accuracy — MNIST results can vary slightly by run due to random weight initialization, unless a fixed random seed is used.

The CNN consistently outperforms the ANN because convolutional layers preserve the 2D spatial relationships between pixels that a flattening operation destroys.

---

## Evaluation Metrics

Both notebooks evaluate the trained model using:

1. **Accuracy & Loss curves** — training vs. validation, per epoch
2. **Confusion Matrix** — which digits get mixed up with which
3. **Classification Report** — precision, recall, and F1-score per digit
4. **Misclassified image gallery** — visual inspection of wrong predictions

Commonly confused digit pairs on MNIST: **4↔9**, **3↔5**, **7↔1** — these share curved, overlapping strokes that are sometimes ambiguous even to a human eye.

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python | Core programming language |
| TensorFlow / Keras | Model building & training |
| NumPy | Numerical array operations |
| Matplotlib / Seaborn | Charts & visualizations |
| scikit-learn | Metrics, evaluation reports, offline demo dataset |
| Jupyter / Google Colab | Interactive notebook environment |

See `requirements.txt` for exact packages.

---

## Future Work

- **Data augmentation** — rotation, shifting, zoom for robustness to real-world handwriting
- **Batch normalization** between convolutional layers
- **Hyperparameter tuning** — learning rate, filter sizes, dropout rate
- **Deployment** — an interactive web app where a user draws a digit and gets a live prediction

---

## Resources

- [MNIST dataset (Yann LeCun's site)](http://yann.lecun.com/exdb/mnist/)
- [TensorFlow Keras documentation](https://www.tensorflow.org/api_docs/python/tf/keras)
- [scikit-learn documentation](https://scikit-learn.org/stable/documentation.html)
- `docs/PROJECT_REPORT.md` — full written report (methodology, implementation, results, key findings)
- `docs/METHODOLOGY.md` — pipeline and architecture reference
- `presentation/MNIST_Digit_Classification.pptx` — 12-slide presentation covering the full project

---

## License

This project is provided for educational purposes. The MNIST dataset is made available by Yann LeCun and Corinna Cortes under a Creative Commons Attribution-Share Alike 3.0 license.
