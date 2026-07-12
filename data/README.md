# `data/`

Column dictionary for the modelling dataset is in [`Dataset Description.txt`](Dataset%20Description.txt).

The CSV files themselves are large and are **not** stored in this repo. Download them from the
[data Drive folder](https://drive.google.com/drive/folders/1wF2DhvBdwzhu8MxORFRXhM7_FQDj2ZdW?usp=sharing)
and place them here:

| File | Description |
|---|---|
| `aac_intakes.csv` | Raw Austin Animal Center intake records |
| `aac_outcomes.csv` | Raw Austin Animal Center outcome records |
| `merged_outcomes_intakes.csv` | Intakes joined to outcomes (output of `Data_Extraction.ipynb`) |
| `data_for_modelling.csv` | Cleaned, feature-engineered modelling table (output of `Exploration.ipynb`) |

The dataset has **135,206 rows** and **14 features**; the target is `outcome_type` (6 classes).
