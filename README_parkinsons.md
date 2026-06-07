# Parkinson's Disease Severity Prediction
### Regularisation & Dimensionality Reduction: Ridge, LASSO, and PCR

![Python](https://img.shields.io/badge/Python-3.9+-blue) ![scikit-learn](https://img.shields.io/badge/scikit--learn-1.0+-orange) ![Status](https://img.shields.io/badge/Status-Complete-green)

---

## Overview

This project predicts **Parkinson's Disease severity** (measured by UPDRS score) from voice biomarker data using three regularised regression methods: Ridge, LASSO, and Principal Components Regression (PCR).

The key question: **which modelling approach best handles the high multicollinearity among voice features?**

---

## Dataset

- **Source:** Parkinson's Disease Voice Measurements dataset
- **Subjects:** 40 individuals — 20 Parkinson's patients (6F, 14M) and 20 healthy controls (10F, 10M)
- **Samples:** 1,040 voice recordings (26 samples per subject)
- **Features:** 26 voice biomarkers including:
  - Jitter variants (pitch irregularity)
  - Shimmer variants (amplitude variation)
  - Harmonics-to-noise ratio
  - Pitch statistics (mean, median, min, max, SD)
  - Voice break measures
- **Target:** UPDRS score (Unified Parkinson's Disease Rating Scale) — continuous severity measure

---

## Methods

| Method | Key Idea | Hyperparameter |
|--------|----------|----------------|
| Ridge Regression | L2 penalty — shrinks all coefficients | α (lambda) |
| LASSO Regression | L1 penalty — sets some coefficients to zero | α (lambda) |
| PCR | PCA + OLS on reduced components | k (n_components) |

All models use **10-fold cross-validation** for hyperparameter tuning and are evaluated on a held-out 20% test set.

---

## Results

| Model | Optimal Parameter | Test MSE | Test RMSE |
|-------|------------------|----------|-----------|
| Ridge | α = 148.50 | 214.53 | 14.65 |
| LASSO | α = 0.1262 | 213.40 | 14.61 |
| **PCR** | **k = 16 components** | **211.25** | **14.54** |

**PCR achieved the lowest test MSE**, explaining ~92% of variance with 16 principal components.

### Key Finding
PCR outperforms direct regularisation because the 26 voice features are **highly intercorrelated** — multiple jitter and shimmer variants measure related acoustic phenomena. Dimensionality reduction removes redundant information more effectively than coefficient shrinkage alone.

---

## Project Structure

```
parkinsons-severity-prediction/
│
├── P161610_DONGYINA.ipynb        # Main analysis notebook
├── Assignment1_data.txt          # Voice measurement dataset
├── model_comparison.png          # Visualisation outputs
└── README.md
```

---

## How to Run

**Requirements:**
```bash
pip install pandas numpy scikit-learn matplotlib
```

**Steps:**
1. Clone the repository
2. Place `Assignment1_data.txt` in the same directory as the notebook
3. Open `P161610_DONGYINA.ipynb` in Jupyter Notebook
4. Run all cells sequentially (`Kernel > Restart & Run All`)

---

## Notebook Contents

1. **Import Libraries** — pandas, numpy, scikit-learn, matplotlib
2. **Load & Explore Dataset** — shape, UPDRS distribution, class balance
3. **Preprocessing** — StandardScaler normalisation, 80/20 train-test split
4. **Ridge Regression** — RidgeCV with 10-fold CV, alpha tuning
5. **LASSO Regression** — LassoCV with 10-fold CV, feature selection analysis
6. **PCR** — PCA component sweep (k=1 to 26), optimal component selection
7. **Visualisation** — MSE comparison bar chart, PCR elbow curve, actual vs predicted scatter
8. **Discussion** — Clinical interpretation, model comparison, conclusions

---

## Clinical Context

UPDRS measures Parkinson's severity across motor and non-motor symptoms. Voice deterioration is one of the earliest and most measurable indicators — approximately 90% of Parkinson's patients develop speech impairments. Jitter and shimmer reflect vocal fold instability directly linked to neuromotor dysfunction.

---

## Course

STQD6114 — Statistical Learning  
Master of Data Science and Analytics  
Universiti Kebangsaan Malaysia (UKM), 2026
