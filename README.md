# 🏈 NFL Stadium Attendance Prediction using Random Forest

This repository contains a complete machine learning pipeline for predicting weekly NFL stadium attendance using a `RandomForestRegressor`. The model was trained and evaluated on a custom-preprocessed dataset constructed from publicly available Kaggle data.

---

<details> <summary>📁 <strong>Project Structure</strong> <span style="font-weight:normal">(click to expand)</span></summary>
.
├── data
│   ├── attendance.csv              # raw game-level attendance (2000-2019)  (backup)
│   ├── games.csv                   # raw game metadata: teams, scores, dates  (backup)
│   ├── standings.csv               # raw season-level team stats              (backup)
│   ├── merged_unprocessed.csv      # raw merge before any cleaning
│   └── merged_preprocessed.csv     # cleaned merge – no encoding/scaling yet
│
├── model_scalers
│   ├── hyp_tuning_best_model.pkl   # RandomForestRegressor (best GridSearchCV params)
│   ├── scaler.pkl                  # StandardScaler fitted to feature matrix X
│   └── target_scaler.pkl           # StandardScaler fitted to target y (attendance)
│
├── outputs
│   ├── mae_vs_estimators.png       # elbow plot: MAE vs n_estimators
│   ├── rf_test_results.txt         # held-out test metrics (MAE/MSE/R², scaled & original)
│   └── rf_validation_results.txt   # CV metrics used for hyper-parameter tuning
│
├── prediction.ipynb                # full pipeline & reproducibility notebook
├── requirements.txt                # pip-installable dependency list
└── README.md                       # project overview, usage guide, citations
</details>



---

## 🧠 Model Summary

* **Algorithm** : `RandomForestRegressor` (scikit-learn 1.3)  
* **Tuning** : `GridSearchCV` (3-fold CV, negative MAE)  
* **Best Parameters**

  | hyper-parameter | value |
  |-----------------|-------|
  | `n_estimators`  | 250   |
  | `max_depth`     | None  |
  | `min_samples_split` | 2 |
  | `min_samples_leaf`  | 3 |
  | `max_features`      | None |

* **Target** : weekly stadium attendance (inverse-transformed with `target_scaler.pkl`)

---

## 🧪 Data Source & Pre-processing

Raw Kaggle CSVs (`games.csv`, `standings.csv`, `attendance.csv`, seasons 2000-2019) live under `data/`.  
They are merged on season + game identifiers into **`merged_unprocessed.csv`**.

Cleaning & engineering in `prediction.ipynb`:

* shift team standings by one season to prevent leakage  
* standardise date formats & team codes  
* split **after** cleaning into 70 / 15 / 15 train-validation-test  
* one-hot encode categoricals and `StandardScaler`-scale numerics **in-memory** only

The encoded table is written to **`merged_preprocessed.csv`** for reference; on-disk splits remain raw.
---

## 📚 Citation

If you use this model or data in your work, please cite it as:

> Emil Paskovski, *NFL Stadium Attendance Prediction using Random Forest*, TU Wien, 2025.  
> DOI: TO BE ADDED


---

## 🛡 License

- **Model, Code, and Scalers**: CC BY 4.0
- **Original Dataset (Kaggle by Sujay Kapadnis)**: No explicit license or usage terms were provided by the dataset uploader. The dataset is assumed to be shared for educational and research purposes as per standard Kaggle community practice. Users are advised to consult the dataset page before reuse or redistribution.

## ⚙️ Quick Start

```bash
# 1 clone
git clone https://github.com/yourusername/NFL-Attendance-Prediction.git
cd NFL-Attendance-Prediction

# 2 install deps
python3.13 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

```python
import pickle

# Load model and scalers
model = pickle.load(open("hyp_tuning_best_model.pkl", "rb"))
scaler = pickle.load(open("scaler.pkl", "rb"))
target_scaler = pickle.load(open("target_scaler.pkl", "rb"))
