# `src/` — notebooks

All project code lives here as Jupyter notebooks. Run them in this order:

1. **`Data_Extraction.ipynb`** — load the raw AAC intake/outcome CSVs, filter to cats & dogs, drop leakage-prone columns, merge intakes with outcomes, and write `data/merged_outcomes_intakes.csv`.
2. **`Exploration.ipynb`** — exploratory data analysis and feature engineering (cyclical datetime features, `intactness`, `sex`, `HasName`, `visit_count`). Produces the plots in `../figures/` and writes `data/data_for_modelling.csv`.
3. **`Finals_LogisticRegression.ipynb`** — ElasticNet logistic-regression pipeline, tuned over 5 seeds.
4. **`Finals_RF.ipynb`** — Random Forest pipeline, tuned over 5 seeds.
5. **`Finals_SVM.ipynb`** — SVM (RBF kernel) pipeline, tuned over 5 seeds.
6. **`Finals_XGB.ipynb`** — XGBoost pipeline, tuned over 5 seeds. **Selected final model.**
7. **`Global_Feature_Importance_XGB.ipynb`** — permutation importance, XGBoost built-in importances, and global SHAP.
8. **`SHAP_XGB - Local+Global.ipynb`** — global and per-class local SHAP explanations.

Common conventions across the modelling notebooks:

- 60/20/20 train/validation/test split, repeated over random seeds `[1, 2, 3, 4, 5]`.
- Primary metric: **macro-averaged F2** (recall-weighted, class-balanced).
- Preprocessing via a scikit-learn `ColumnTransformer` (standard-scale numerics, one-hot encode categoricals, sin/cos encode cyclical time features).
- For tractable tuning, fitting is done on a 10% stratified sample of the full dataset.
- Tuning artifacts are saved to `../results/pipeline_results_<model>.pkl`.

> Data (`../data/*.csv`) and result artifacts (`../results/*.pkl`) are downloaded separately — see the main [README](../README.md).
