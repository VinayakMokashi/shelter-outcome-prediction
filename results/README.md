# `results/`

Saved model/tuning artifacts (`.pkl`). These files are large (hundreds of MB each) and are
**not** stored in this repo. Download them from the
[results Drive folder](https://drive.google.com/drive/folders/1rUGrAiCm9zcT76vAWFSQJfdOqtGtUpvF?usp=sharing)
and place them here:

| File | Description |
|---|---|
| `pipeline_results_elasticnet.pkl` | Logistic Regression (ElasticNet) tuning results |
| `pipeline_results_rf.pkl` | Random Forest tuning results |
| `pipeline_results_svm.pkl` | SVM (RBF) tuning results |
| `pipeline_results_xgboost.pkl` | XGBoost tuning results |
| `final_model_XGB_results.pkl` | Final selected XGBoost model + metrics |

Load an artifact with:

```python
import pickle
with open("results/final_model_XGB_results.pkl", "rb") as f:
    results = pickle.load(f)
```
