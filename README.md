# APS Failure Prediction 

## Overview

This project applies tree‑based ensemble models—Random Forests and XGBoost model trees—alongside class‑imbalance remedies (class weighting and SMOTE) to the APS Failure dataset of Scania Trucks.

### Objectives

1. Impute missing values and perform exploratory analysis (CV ranking, correlation heat‑map, scatter / box plots).
2. Train a baseline Random Forest classifier and evaluate with out‑of‑bag (OOB) error, confusion matrix, ROC curve, AUC and misclassification cost.
3. Re‑train Random Forest with class‑weight compensation and compare.
4. Build an XGBoost model tree (L1‑penalised logistic leaves), tune the `alpha` regularisation term with cross‑validation and evaluate.
5. Apply **SMOTE** to oversample the minority class, retrain XGBoost and compare with the uncompensated model.
6. Address conceptual questions from *ISLR* Chapters 5–9.

## Dataset

The Air‑Pressure System (APS) failure dataset comprises **60 000** training and **16 000** test observations, each with **170** numeric features plus a binary *class* label. fileciteturn0file1
The positive class (failures of a specific component) represents \~1.7 % of the training set, leading to severe class imbalance. Missing values are encoded as `"na"`.

Download `aps_failure_training_set.csv` & `aps_failure_test_set.csv` from the [UCI ML repository](https://archive.ics.uci.edu/dataset/468/aps+failure+at+scania+trucks) and place them in `data/`.

## Repository Structure

```text
.
├── Data/
│   ├── aps_failure_training_set.csv
│   ├── aps_failure_test_set.csv
│   └── README_DATA_LICENSE.txt
├── NOTEBOOK/
│   └── aps-failure-code.ipynb        # main analysis notebook
└── README.md
```

## Environment & Installation

```bash
git clone https://github.com/<your‑user>/aps-failure-prediction.git
cd aps-failure-prediction

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install pandas numpy scikit-learn imbalanced-learn xgboost matplotlib seaborn jupyterlab
```

Key packages:

* `pandas`, `numpy`
* `scikit‑learn`
* `imbalanced‑learn`
* `xgboost`
* `matplotlib`, `seaborn`
* `jupyterlab`


## Running the Notebook

```bash
jupyter lab NOTEBOOK/aps-failure-code.ipynb
```

The notebook is segmented so that each section can be executed independently:

1. Data loading & imputation (default: KNNImputer)
2. Exploratory Data Analysis
3. Baseline Random Forest
4. Class‑balanced Random Forest
5. XGBoost model tree
6. SMOTE ➔ XGBoost

> **Performance note:** SMOTE on all 59 000 majority‑class rows may require several hours and >16 GB RAM. A down‑sampling cell is provided to cap the majority class at 6 000 samples if resources are limited.

### Metrics Snapshot (`comparison_df`)

|                   |  Train Error | Train Accuracy |    Train ROC |  Test Error | Test Accuracy |     Test ROC |
| ----------------- | -----------: | -------------: | -----------: | ----------: | ------------: | -----------: |
| **Without SMOTE** | **0.001467** |   **0.998533** | **0.999300** | **0.00700** |   **0.99300** | **0.995877** |
| **With SMOTE**    |     0.007017 |       0.992983 |     0.998659 |     0.01225 |       0.98775 |     0.995843 |

## License
 
This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.

The **APS Failure** dataset is © 2016 Scania CV AB and distributed under GPL‑v3; see `aps_failure_description.txt` for details.fileciteturn0file1
