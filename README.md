# Austin Animal Center Outcome Prediction 

Predicts **`outcome_type`** (multiclass) for **cats/dogs** using **intake-time features only**.  
Full project overview, methodology, and results are in **`report/`**

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


## Repo layout
- `data/` — **raw + preprocessed** datasets  
- `figures/` — all generated plots  
- `results/` — outputs (saved models/metrics/predictions, **.pkl** files)  
- `src/` — all code (notebooks/scripts)  
- `report/` — final PDF report  
## Environment (reproducible)

This repo includes a Conda YAML environment: `data1030.yml`

- **Env name:** data1030  
- **Python:** 3.12.10  
- **Key packages:** numpy 2.2.5, pandas 2.2.3, polars 1.27.1, scikit-learn 1.6.1, xgboost 3.0.0, shap 0.47.2, matplotlib 3.10.1, seaborn 0.13.2

### Create the environment
```bash
conda env create -f data1030.yml
conda activate data1030

