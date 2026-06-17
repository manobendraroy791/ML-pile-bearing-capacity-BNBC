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
  * 📖 `data_dictionary.md` *(Definitions for every feature and variable used in the pipeline)*
* 📁 **notebooks/**
  * 📓 `01_data_preprocessing.ipynb` *(Feature engineering & stratum encoding)*
  * 📓 `02_model_benchmarking.ipynb` *(Training DT, RF, SVM, KNN, and XGBoost)*
  * 📓 `03_explainable_ai.ipynb` *(SHAP values & 2D Interaction Heatmaps)*
  * 📓 `04_monte_carlo_rbd.ipynb` *(60,000-iteration statistical stress testing)*
* 📁 **visuals/**
  * 🖼️ `XGB_Performance_Overall.png` *(Actual vs. predicted capacity, training & testing R²)*
  * 🖼️ `XGB_Performance_BySoilType.png` *(Prediction accuracy split by Sand, Silt, and Clay)*
  * 🖼️ `Residual_Distribution.png` *(Error frequency analysis against a normal fit)*
  * 🖼️ `Proportional_Accuracy_Envelope.png` *(±10% / ±20% margin coverage across all test piles)*
  * 🖼️ `Feature_Importance_BySoilType.png` *(Relative feature importance for all three soil types)*
  * 🖼️ `Interaction_Heatmap.png` *(2D Partial Dependence Contour Heatmaps)*
  * 🖼️ `MonteCarlo_Reliability_Matrix.png` *(SPT variance impact on stratum mechanics)*
* 📄 **README.md**
* ⚙️ **requirements.txt**

---

## 🧠 The Machine Learning Pipeline

### 1️⃣ Data Isolation & Engineering
> **Goal:** Guarantee generalizable soil physics, preventing local data memorization.
* **Action:** The dataset was strictly partitioned geographically, with training and validation sets drawn from entirely separate site locations to mathematically prevent the model from memorizing site-specific geological noise.

### 2️⃣ Algorithmic Benchmarking
> **Goal:** Find the optimal balance between bias and variance for complex soil behavior.
* **Evaluated:** Decision Trees (DT), Random Forest (RF), Support Vector Machines (SVM), K-Nearest Neighbors (KNN).
* 🏆 **Champion Model (XGBoost):** Selected for its superior ability to capture non-linear step-changes in stratigraphy and exponential end-bearing mechanics.

<div align="center">

*<img width="974" height="776" alt="XGB_Performance_Overall" src="https://github.com/user-attachments/assets/7d4352f7-f1dc-4131-80f2-f4911f5ad916" />*

> **Figure 1:** *Actual vs. predicted pile bearing capacity, showing near-perfect agreement on training data (R² = 0.9998) and strong generalization on unseen testing data (R² = 0.9884).*

*<img width="1789" height="576" alt="XGB_Performance_BySoilType" src="https://github.com/user-attachments/assets/606b162a-18a3-4d9e-b1ac-a1c99717a85f" />*

> **Figure 2:** *Model accuracy broken down by terminal soil type — Sand (R² = 0.9822), Silt (R² = 0.9865), and Clay (R² = 0.9813).*

</div>

### 3️⃣ Model Uncertainty Quantification
> **Goal:** Characterize exactly how, and by how much, the model's predictions deviate from empirical ground truth to establish structural confidence intervals.

<div align="center">

*<img width="2649" height="1751" alt="Residual_Distribution" src="https://github.com/user-attachments/assets/37aae19d-5971-401d-93ba-3ed1288908b3" />*

> **Figure 3:** *Distribution of model residuals fitted against a normal curve (μ = 78.0 kN, σ = 243.2 kN), confirming prediction errors are tightly bounded and centered near zero.*

*<img width="2352" height="2352" alt="Proportional_Accuracy_Envelope" src="https://github.com/user-attachments/assets/e341fdab-e179-42cb-b5c6-634d1e56ea18" />*

> **Figure 4:** *Proportional accuracy showing 79.7% of test piles fall within a strict ±10% accuracy margin, and 93.2% fall within ±20%, relative to the actual BNBC capacity.*

</div>

### 4️⃣ Geotechnical Explainability (XAI)
> **Goal:** Prove the AI acts as a valid, physics-aware structural engineering tool.
* Visualized exactly how the AI separates cumulative skin friction from localized tip resistance using **SHAP**.
* Generated **2D Partial Dependence Contour Heatmaps** to allow structural engineers to visually optimize pile geometry (Diameter vs. Length).

<div align="center">

*<img width="1780" height="580" alt="Feature_Importance_BySoilType" src="https://github.com/user-attachments/assets/ccb048fe-a6f4-481a-9682-7dd201312f3d" />*

> **Figure 5:** *Relative feature importance for the XGBoost model across all three soil types — shaft friction (N60_Shaft) dominates in Clay, while pile geometry (Pile_Size_mm) dominates in Sand.*

*<img width="5352" height="1788" alt="Interaction_Heatmap" src="https://github.com/user-attachments/assets/300aae33-572d-4cf5-b416-a00f5cc2280e" />*

> **Figure 6:** *2D Partial Dependence Contour Heatmaps showing pile geometry optimization across Pile Size, Pile Length, Tip Resistance, and Shaft Stiffness.*

</div>

---

## 🎲 Reliability-Based Design (Monte Carlo Simulations)
*(See notebooks/04_monte_carlo_rbd.ipynb)*

Machine learning models inherently assume input data is perfectly accurate, but real-world SPT N60 measurements are highly susceptible to mechanical error. To bridge the gap between Data Science and Structural Engineering, this project features a custom Monte Carlo simulation engine.

* ⚠️ **The Stress Test:** Simulated 60,000 artificial pile installations applying a **20% Coefficient of Variation (COV)** to the SPT input data.
* 🛡️ **The Result:** Calculated the strict **5th-Percentile Characteristic Limit**, giving structural engineers a statistically guaranteed safety bound that explicitly accounts for on-site measurement errors.

<div align="center">

*<img width="4752" height="5514" alt="MonteCarlo_Reliability_Matrix" src="https://github.com/user-attachments/assets/71f4d57f-25cf-4148-83aa-1636ea3fa099" />*

> **Figure 7:** *Comprehensive reliability matrix showing SPT variance impact on stratum mechanics — proving the localized volatility of Deep Sand End-Bearing versus the structural resilience of Upper Clay Skin Friction.*

</div>

---

## 🚀 How to Run Locally

1. **Clone the repository:** `git clone https://github.com/manobendraroy791/ML-pile-bearing-capacity-BNBC.git`
2. **Install dependencies:** `pip install -r requirements.txt`
3. **Launch the environment:** Open the `notebooks/` directory and run them sequentially.
