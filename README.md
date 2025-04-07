# Fashion MNIST Dataset Analysis

---

## 📌 Introduction

The dataset used is the **Fashion MNIST** dataset, which includes **70,000 images** of clothing items divided into:
- **Training set**: 60,000 images
- **Test set**: 10,000 images

Each image is:
- 28x28 pixels
- Grayscale (values between 0–255)
- Flattened into a row of **784 pixel columns**
- Labeled with one of the following categories:

| Label | Clothing Type   |
|-------|------------------|
| 0     | T-shirt/top      |
| 1     | Trouser          |
| 2     | Pullover         |
| 3     | Dress            |
| 4     | Coat             |
| 5     | Sandal           |
| 6     | Shirt            |
| 7     | Sneaker          |
| 8     | Bag              |
| 9     | Ankle boot       |

---

## 📉 Data Dimensionality Reduction

To improve performance and reduce computation time:

- The dataset was limited to **20,000 rows**.
- Data was **rescaled** using `MinMaxScaler` (or by dividing by 255).
- **PCA (Principal Component Analysis)** was used to determine the number of components preserving **>95% variance**, resulting in **188 components**.
- **T-SNE (t-distributed Stochastic Neighbor Embedding)** was used to reduce data to **2 dimensions** for better visual clustering.

---

## 📊 Visualization

### PCA (2D)

- Fast but poor for visual clustering.
- Hard to detect patterns or clusters in the result.

### T-SNE (2D)

- **Clearer clustering** than PCA.
- Some **outliers** are visible, especially on the right side.

---

## 🔗 Clustering Dataset

Clustering was done both on:
- **2D data** (via T-SNE)
- **188D data** (via PCA)

### 🧱 Agglomerative Clustering

#### 2D
- Tried different linkage methods: `'ward'`, `'complete'`, `'average'`
- Evaluation Metrics:
  - `Rand Score`: ~89%
  - `V-Measure`: ~59%

#### 188D
- `Rand Score`: 83%
- `V-Measure`: 41%

### 📍 KMeans

#### 2D
- Clusters appear rigid, divided like “by a ruler”
- `Rand Score`: 88.95%
- `V-Measure`: 54.92%

#### 188D
- Faster than AgglomerativeClustering
- `Rand Score`: 81%
- `V-Measure`: 51%

### 🌌 DBSCAN

#### 2D
- Detected **780 outliers** (~3.8% of dataset)
- Found 10 clusters using loops to tune `eps` and `min_samples`
- `Rand Score`: 85.97%
- `V-Measure`: 59.27%

#### 188D
- Struggled to perform well
- Often too many noise points or a single large cluster
- No satisfactory clustering was found

---

## 🔍 Splitting Dataset for Classification

Dataset was split into **training** and **test** sets using `train_test_split()`.

---

## ✅ Classification Results

### 🔹 KNeighborsClassifier

- Best `n_neighbors`: 4
- **Accuracy**: 84.36%
- Confusion matrix was created for performance analysis.

### 🔸 DecisionTreeClassifier

- Best `random_state`: 44
- Best `max_depth`: 9
- **Accuracy**: 79.02%

### 🌲 RandomForestClassifier

- Best `max_depth`: 18
- **Accuracy**: 87.86%
- Outperformed other classifiers

---

## 📎 Summary

- **T-SNE** was significantly better than PCA for 2D visualization.
- **DBSCAN** was best at identifying outliers.
- **RandomForestClassifier** achieved the highest classification accuracy.
- Dataset reduction and parameter tuning were key to improving performance.

---
