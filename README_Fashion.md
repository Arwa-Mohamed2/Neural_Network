# 👗 Fashion-MNIST Clothing Classification — MLP

**Course:** Artificial Neural Networks  
**Dataset:** Fashion-MNIST — 60,000 training images, 10 clothing classes  
**Framework:** TensorFlow / Keras · Google Colab  
**Experiment:** ReLU vs Sigmoid activation functions

---

## Problem Description

Fashion-MNIST is a benchmark dataset of grayscale clothing images designed as a drop-in replacement for the original MNIST digits dataset. This project builds and trains a **Multi-Layer Perceptron (MLP)** to classify 10 types of clothing items.

Two experiments are conducted to compare the effect of different activation functions on model performance — all other hyperparameters are held constant.

---

## Dataset

- **Name:** Fashion-MNIST
- **Source:** Built into Keras — `tensorflow.keras.datasets.fashion_mnist`
- **Size:** 60,000 training images · 10,000 test images
- **Format:** Grayscale 28×28 pixel images, pre-split into train and test sets
- **Classes:** 10 clothing categories

| Class ID | Label |
|---|---|
| 0 | T-shirt/top |
| 1 | Trouser |
| 2 | Pullover |
| 3 | Dress |
| 4 | Coat |
| 5 | Sandal |
| 6 | Shirt |
| 7 | Sneaker |
| 8 | Bag |
| 9 | Ankle boot |

> No download needed — Keras loads the dataset automatically on first run.

---

## Model Architecture

```
Input (784,)  ← 28×28 image flattened into a 1D vector
  └─ Dense(256, ReLU/Sigmoid) → Dropout(0.3)
  └─ Dense(128, ReLU/Sigmoid) → Dropout(0.2)
  └─ Dense(10, Softmax)       ← output: probability per class
```

**Preprocessing applied:**
-  **Normalisation** — pixel values scaled from [0, 255] to [0.0, 1.0]
-  **Flattening** — 28×28 images reshaped to 784-length vectors
-  **One-hot encoding** — integer labels converted to categorical vectors
-  **Data quality check** — NaN verification and label distribution inspection

---

## Experiments

| | Model A | Model B |
|---|---|---|
| **Activation** | ReLU | Sigmoid |
| **Optimiser** | Adam | Adam |
| **Epochs** | 20 | 20 |
| **Batch Size** | 64 | 64 |
| **Hidden Layers** | 256 → 128 | 256 → 128 |
| **Dropout** | 0.3 · 0.2 | 0.3 · 0.2 |

> Only the activation function changes between experiments. Everything else is identical — this isolates the effect of the activation function on performance.

---

## Results

| Model | Accuracy | Loss |
|---|---|---|
| Model A — ReLU | 0.8835% | 0.3383 |
| Model B — Sigmoid | 0.8867% | 0.3154 |

> **Best model:** Model B (Sigmoid)
> **Difference:** Model B outperformed Model A by 0.32%
---

## 📈 Visualisations

All plots are saved automatically to Google Drive under `fashion_mnist_project/results/`:

| File | Description |
|---|---|
| `sample_images.png` | 10 sample clothing images (one per class) |
| `training_curves.png` | Loss & accuracy curves for both models (2×2 grid) |
| `confusion_matrix.png` | 10×10 confusion matrix for Model A (ReLU) |

---

## How to Run

### 1. Clone the repository
```bash
git clone https://github.com/iarwamohamed/fashion-mnist-classification.git
cd fashion-mnist-classification
```

### 2. Open in Google Colab
Upload `NN_Proj_Fashion.ipynb` to [colab.research.google.com](https://colab.research.google.com).

> No GPU required — the MLP is lightweight and trains fast on CPU.

### 3. Run all cells in order

| Cell | Purpose |
|---|---|
| Cell 1 | Mount Google Drive |
| Cell 2 | Imports & libraries |
| Cell 3 | Load & preprocess data (normalise · flatten · one-hot encode) |
| Cell 3.5 | Data quality checks (NaN verification, label distribution) |
| Cell 4 | Visualise sample images |
| Cell 5 | **Experiment A** — Build & train Model A (ReLU) |
| Cell 6 | **Experiment B** — Build & train Model B (Sigmoid) |
| Cell 7 | Training curves (loss & accuracy, 2×2 grid) |
| Cell 8 | Results comparison table |
| Cell 9 | Classification report — Model A |
| Cell 10 | Confusion matrix — Model A |
| Cell 11 | Save both models to Google Drive |
| Cell 12 | Test on your own uploaded image |

### 4. Test on a custom image (Cell 12)
1. Download any clothing image from the web (JPG or PNG)
2. In Colab, open the **Files panel** (📁 icon on the left sidebar) → click **Upload**
3. Right-click the uploaded file → **Copy path**
4. Paste it into Cell 12:
```python
IMAGE_PATH = '/content/your_image.jpg'
```
5. Run the cell — the model converts it to 28×28 grayscale and shows its **top-3 predictions** with confidence scores

> **Note:** The displayed image will appear pixelated — this is expected. Fashion-MNIST was trained on 28×28 images, so all inputs are aggressively downsampled. The model predicts from shape, not texture or colour.

---

## Repository Structure

```
fashion-mnist-classification/
│
├── NN_Proj_Fashion.ipynb        # Main notebook
├── README.md                    # This file
└── results/                     # Auto-generated after training (saved to Drive)
    ├── sample_images.png
    ├── training_curves.png
    └── confusion_matrix.png
```

---

## 👩‍💻 Author

**Arwa Mohamed**  
Artificial Neural Networks Course
