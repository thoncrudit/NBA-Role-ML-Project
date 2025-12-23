# Predicting NBA player roles using Machine Learning

The project investigates whether professional NBA player roles (**Starter vs. Reserve**) can be accurately predicted using season-level performance statistics.

---

## 👥 Authors

* **Gabriel B.** 


* **Tom B.** 


* **Samyuktha K.** 


* **Supervised by:** Gabriel D.

--- 
## 🚀 How to Run

1. Upload the season .txt files (2022-2025) located in ML Datasets.

2. Run all cells to execute the data cleaning, PCA analysis, and model training pipeline.

3. Evaluation metrics and visualizations will be generated inside the notebook.


---

## 📌 Project Overview

The core objective is to determine if historical performance data can identify systematic patterns associated with starting roles, providing a quantitative complement to traditional expert judgment.

### The dataset

* **Source:** Season-level performance statistics from **Basketball Reference**.

* **Scope:** Three regular seasons spanning **2022-2023** to **2024-2025**.

* **Observations:** 1,441 unique player-season entries after cleaning.

* **Target variable:** A binary label, `is_starter`, defined as 1 if a player started more than 50% of the games they played in a given season.

---

## 🛠️ Machine Learning pipeline

### 1. Pre-processing & cleaning

* **Duplicate handling:** Resolved issues with traded players by retaining only one entry per player-season to represent total performance.


* **Noise reduction:** Excluded players with fewer than **100 total minutes played** to ensure statistical significance.


* **Feature engineering:** Utilized 24 metrics, including offensive volume (PTS, FGA), efficiency (eFG%, FT%), and defensive contributions (STL, BLK).


* **Leakage prevention:** Explicitly excluded **Games Started (GS)** and **Games Played (G)** from the feature set to avoid direct encoding of the target variable.



### 2. Exploratory Data Analysis (EDA)

* **Correlation analysis:** Identified strong multicollinearity among volume-based features (Points, Minutes Played, Field Goal Attempts).


* **Dimensionality reduction:** Applied **Principal Component Analysis (PCA)** to confirm that the Starter vs. Reserve distinction is largely driven by a limited set of underlying factors related to usage and efficiency.



---

## 📊 Model Performance Comparison

The task was formulated as a supervised binary classification problem where the feature matrix is defined as . Models were evaluated using **F1-score** to account for the class imbalance (approx. 63% Reserves).

| Model | F1-Score (Normal) | F1-Score (5-Fold CV) |
| --- | --- | --- |
| **XGBoost (Tuned)** | **0.8094** | - |
| **Logistic Regression** | 0.8055 | 0.7774 |
| **Stacking Classifier** | 0.8000 | - |
| **Random Forest** | 0.7961 | 0.7789 |
| **Voting Classifier** | 0.7946 | - |
| **XGBoost (Untuned)** | 0.7935 | 0.7772 |
| **SVM (Tuned)** | 0.7693 | - |

---

## 🔍 Key Insights

* **Volume is King:** Player role is largely driven by volume-related statistics (Minutes Played and Offensive Usage) rather than subtle efficiency variations.


* **Model Robustness:** While simple linear models performed well, the **Tuned XGBoost** and **Stacking** models provided the highest peak accuracy by capturing complex interactions.


* **The "Sixth Man" Effect:** SHAP analysis revealed that misclassifications often occur with elite bench players who possess starter-level efficiency but reduced volume.



---

## 💻 Technical Requirements

* **Language:** Python 3.x
* **Environment:** Google Colab 

* **Libraries:** Pandas, Scikit-learn, XGBoost, SHAP, Matplotlib, Seaborn
