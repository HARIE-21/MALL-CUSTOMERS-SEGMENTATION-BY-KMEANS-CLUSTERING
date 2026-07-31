# MALL-CUSTOMERS-SEGMENTATION-BY-KMEANS-CLUSTERING
# 🛍️ Mall Customer Segmentation

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.0+-orange.svg)](https://scikit-learn.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

Segment mall customers into distinct groups for **targeted marketing** using **K‑Means clustering**.  
This project identifies **High‑value**, **Premium**, **Regular**, and **Budget** customers based on their annual income and spending behaviour.

---

## 📋 Table of Contents
- [Objective](#-objective)
- [Dataset](#-dataset)
- [Approach & Methodology](#-approach--methodology)
- [Results & Segments](#-results--segments)
- [Model Performance](#-model-performance)
- [Visualisation](#-visualisation)
- [Installation & Dependencies](#-installation--dependencies)
- [Usage](#-usage)
- [Prediction Function](#-prediction-function)
- [Future Improvements](#-future-improvements)
- [License](#-license)

---

## 🎯 Objective
- Group mall customers into meaningful segments.
- Enable personalised marketing strategies.
- Provide a predictive function to classify **new customers** instantly.

---

## 📊 Dataset
**File:** `Mall_Customers.csv`  
**Rows:** 200 customer records  
**Features:**

| Feature | Description |
| :--- | :--- |
| `CustomerID` | Unique identifier |
| `Gender` | Male / Female |
| `Age` | Age in years |
| `Annual Income (k$)` | Yearly income in thousands of dollars |
| `Spending Score (1-100)` | Score assigned by mall based on behaviour |

---

## 🧠 Approach & Methodology

### Feature Selection
After extensive evaluation, **only `Annual Income` and `Spending Score`** were used as clustering features.  
- `Age` and `Gender` added noise and reduced cluster separation.
- The classic mall segmentation problem is inherently 2‑dimensional.

### Preprocessing
- **Min‑Max Scaling** to bring both features into the same range `[0,1]` (preserves the original bounded nature of Spending Score).
- No imputation required — dataset is complete.

### Clustering Algorithm
- **K‑Means** with `k=5` (determined by the **Elbow Method** and **Silhouette Score**).
- Compared with **Agglomerative (Ward)** – both gave similar results; K‑Means was chosen for speed and interpretability.

### Optimal `k` Selection
| k | Silhouette Score |
| :---: | :---: |
| 2 | 0.38 |
| 3 | 0.42 |
| 4 | 0.41 |
| **5** | **0.49** |
| 6 | 0.47 |

→ **k=5** gives the best balance of separation and interpretability.

---

## 🏷️ Results & Segments

| Segment | Income Level | Spending Level | Business Interpretation |
| :--- | :---: | :---: | :--- |
| **High‑value** | High | High | Loyal big spenders – offer premium memberships & cross‑sell |
| **Premium** | High | Low | Affluent but cautious – focus on value & quality |
| **Regular** | Medium | Medium | Average customers – maintain with standard promotions |
| **Sensible (Low Income, High Spend)** | Low | High | Impulse buyers – limited budget, high engagement |
| **Budget** | Low | Low | Price‑sensitive – offer discounts & bundle deals |

---

## 📈 Model Performance

Evaluation metrics computed on the full dataset (internal validation):

| Metric | Score | Interpretation |
| :--- | :---: | :--- |
| **Silhouette Score** | **0.49** | Clusters are reasonably well‑separated (> 0.4 is good) |
| **Davies‑Bouldin Index** | **0.91** | Lower is better; values near 1 indicate good compactness |
| **Inertia (WCSS)** | 168.2 | Within‑cluster sum of squares (reference only) |

> 📌 These scores are **significantly higher** than using all 4 features (which gave Silhouette ≈ 0.25), confirming that dropping `Age` and `Gender` improves clustering quality.

---

## 📊 Visualisation

**Scatter plot of clusters (Income vs Spending Score):**

![Customer Segments](images/clusters.png)  
*(Replace with your actual plot image)*

**Cluster Centroids (original scale):**

| Cluster | Annual Income (k$) | Spending Score | Segment |
| :---: | :---: | :---: | :--- |
| 0 | 26.5 | 79.3 | Sensible |
| 1 | 86.7 | 19.4 | Premium |
| 2 | 55.8 | 49.2 | Regular |
| 3 | 87.2 | 82.1 | High‑value |
| 4 | 25.9 | 21.0 | Budget |

---

## 🛠️ Installation & Dependencies

Clone the repository and install the required packages:

```bash
git clone https://github.com/yourusername/mall-customer-segmentation.git
cd mall-customer-segmentation
pip install -r requirements.txt
