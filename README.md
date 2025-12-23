# shelter-outcome-prediction
Predicting animal shelter outcomes at intake using supervised machine learning

## Data
Full dataset (not stored in this repo):
- Drive folder: [https://drive.google.com/...](https://drive.google.com/drive/folders/1wF2DhvBdwzhu8MxORFRXhM7_FQDj2ZdW?usp=sharing)
- Place downloaded files in `data/` before running the code.

## Results

Before running any code, download all files from  
https://drive.google.com/drive/folders/1rUGrAiCm9zcT76vAWFSQJfdOqtGtUpvF?usp=sharing  
and place them in the `results/` folder.

This Drive folder contains the saved pickle files for all models and other
artifacts needed to reproduce the results.

## Report (PDF): report/
Repo goal: Predict outcome_type (6 classes) at intake time so shelters can proactively allocate limited resources to animals at risk of poor outcomes.

## Project overview

Animal shelters face overcrowding, limited staff/vets, and longer stays due to medical/behavioral issues. If we can predict likely outcomes right when an animal arrives, shelters can intervene earlier (marketing, foster placement, fee waivers, medical care) instead of reacting late.

## Dataset

This project uses two public Austin Animal Center datasets:

Intakes table (recorded at arrival)

Outcomes table (recorded at exit)

We:

merge tables on AnimalID

restrict analysis to cats and dogs

keep only predictors available at intake (avoid leakage)

## Summary (after merge & filtering):

Rows: 135,206

Predictors: 13

Target: outcome_type with 6 classes: Adoption, Return to Owner, Transfer, Euthanasia, Died, Other

Time range: Oct 1, 2013 → May 2, 2025

## Repository structure:

.
├── data/        # raw + preprocessed (if too large, keep empty and provide download steps)
├── figures/     # generated plots
├── results/     # saved models, predictions, pickles, metrics, etc.
├── report/      # final PDF report
├── src/         # notebooks / scripts used to run the pipeline
├── .gitignore
├── LICENSE
└── README.md

## Modeling approach
Features & preprocessing

We start with 13 input features, and after one-hot encoding high-cardinality categories (breed/color), we end up with 950+ features.
retain most recent visit per AnimalID and create visit_count (# historical visits)

Preprocessing (fit on train only, then applied to val/test):

Numeric (2): StandardScaler 

Datetime (3): month/weekday/hour → cyclical encoding (sin/cos) 

Categorical (8): one-hot encoding

## Evaluation metric

Primary metric: Macro-F2 (recall-heavy; macro averaging gives each class equal weight under imbalance).
Baseline: always predict most common class (Adoption) for reference.

# Training & selection pipeline

For each of 5 random seeds:

Stratified 60/20/20 split (train/val/test)

Fit preprocessors on train; transform all sets

Handle imbalance with class/sample weights from train labels

Hyperparameter search on train; pick best by Validation Macro-F2

Evaluate chosen config on test; store Test Macro-F2

Final reporting:

Test Macro-F2 reported as mean ± std across runs

Best configuration selected by highest average validation Macro-F2 across seeds

## Models & hyperparameters tuned

We compare 4 models:

Logistic Regression (Elastic Net)

SVM

Random Forest

XGBoost

## Key fixed settings:

Random Forest: n_estimators = 500

XGBoost: n_estimators = 10000, early stopping = 50, learning_rate = 0.03, colsample_bytree = 0.9, subsample = 0.66

All models: balanced class/sample weights

Search spaces (see report Table 1) include:

Elastic Net: C, l1_ratio

SVM: C, gamma, kernel ∈ {linear, rbf}

RF: max_depth, max_features

XGB: max_depth, reg_alpha, reg_lambda

