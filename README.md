# ML-pile-bearing-capacity-BNBC
Predicting driven pile bearing capacity using SPT data and XGBoost. Features SHAP interpretability and Monte Carlo Reliability-Based Design (RBD).
<div align="center">

# 🏗️ Predicting Driven Pile Bearing Capacity
### Machine Learning & Reliability-Based Design (RBD)

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![XGBoost Champion](https://img.shields.io/badge/Model-XGBoost-orange.svg)](https://xgboost.readthedocs.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

*A comparative study bridging Data Science and Civil Engineering, benchmarking AI against BNBC2020 guidelines.*

---
</div>

## 📖 Overview
This repository contains an end-to-end Machine Learning pipeline designed to predict the axial bearing capacity of driven piles using Standard Penetration Test (SPT) datasets. 

Moving beyond standard predictive accuracy, this research heavily utilizes **Explainable AI (SHAP)** to reverse-engineer the model's geotechnical logic, and **Monte Carlo Simulations** to establish safe foundation design limits under severe SPT measurement uncertainty.

---

## 🗂️ Repository Architecture

* 📁 **data/**
  * 📊 `train_data.csv` *(29 independent boreholes)*
  * 📊 `test_data.csv` *(6 strictly isolated boreholes)*
* 📁 **notebooks/**
  * 📓 `01_data_preprocessing.ipynb` *(Feature engineering & stratum encoding)*
  * 📓 `02_model_benchmarking.ipynb` *(Training DT, RF, SVM, KNN, and XGBoost)*
  * 📓 `03_explainable_ai.ipynb` *(SHAP values & 2D Interaction Heatmaps)*
  * 📓 `04_monte_carlo_rbd.ipynb` *(60,000-iteration statistical stress testing)*
* 📁 **visuals/**
  * 🖼️ `HighRes_3Panel_Design_Heatmaps.png`
  * 🖼️ `HighRes_6Panel_Monte_Carlo.png`
* 📄 **README.md**
* ⚙️ **requirements.txt**

---

## 🧠 The Machine Learning Pipeline

### 1️⃣ Data Isolation & Engineering
> **Goal:** Guarantee generalizable soil physics, preventing local data memorization.
* **Action:** The dataset was strictly partitioned geographically. Models were trained on records from 29 boreholes across multiple sites, while validation was locked entirely to 6 unseen, independent borehole locations.

### 2️⃣ Algorithmic Benchmarking
> **Goal:** Find the optimal balance between bias and variance for complex soil behavior.
* **Evaluated:** Decision Trees (DT), Random Forest (RF), Support Vector Machines (SVM), K-Nearest Neighbors (KNN).
* 🏆 **Champion Model (XGBoost):** Selected for its superior ability to capture non-linear step-changes in stratigraphy and exponential end-bearing mechanics.

### 3️⃣ Geotechnical Explainability (XAI)
> **Goal:** Prove the AI acts as a valid structural engineering tool.
* Visualized exactly how the AI separates cumulative skin friction from localized tip resistance using **SHAP**.
* Generated **2D Partial Dependence Contour Heatmaps** to allow structural engineers to visually optimize pile geometry (Diameter vs. Length).

---

## 🎲 Reliability-Based Design (Monte Carlo Simulations)
*(See notebooks/04_monte_carlo_rbd.ipynb)*

Machine learning models inherently assume input data is perfectly accurate, but real-world SPT N60 measurements are highly susceptible to mechanical error. To bridge the gap between Data Science and Structural Engineering, this project features a custom Monte Carlo simulation engine.

* ⚠️ **The Stress Test:** Simulated 60,000 artificial pile installations applying a **20% Coefficient of Variation (COV)** to the SPT input data.
* 🛡️ **The Result:** Calculated the strict **5th-Percentile Characteristic Limit**, giving structural engineers a statistically guaranteed safety bound that explicitly accounts for on-site measurement errors.

<div align="center">

*(Drag and drop your HighRes_6Panel_Monte_Carlo.png <img width="4752" height="5514" alt="HighRes_6Panel_Manual_Scaling" src="https://github.com/user-attachments/assets/ef9a1e7a-e13b-4a43-9f4e-690a7d110fb9" />
image here)*

**Figure 1:** *6-Panel Monte Carlo simulation proving the localized volatility of Deep Sand End-Bearing versus the structural resilience of Upper Clay Skin Friction.*

</div>

---

## 🚀 How to Run Locally

1. **Clone the repository:** `git clone https://github.com/yourusername/your-repo-name.git`
2. **Install dependencies:** `pip install -r requirements.txt`
3. **Launch the environment:** Open the `notebooks/` directory and run them sequentially.
