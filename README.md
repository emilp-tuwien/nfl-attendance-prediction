# 🏈 NFL Stadium Attendance Prediction using Random Forest

This repository contains a complete machine learning pipeline for predicting weekly NFL stadium attendance using a `RandomForestRegressor`. The model was trained and evaluated on a custom-preprocessed dataset constructed from publicly available Kaggle data.

---
## 📁 Project structure

* **data/**
  * `attendance.csv` – raw attendance (2000-2019)
  * `games.csv` – raw game metadata
  * `standings.csv` – raw season stats
  * `merged_unprocessed.csv` – first raw merge
  * `merged_preprocessed.csv` – cleaned merge
* **model_scalers/**
  * `hyp_tuning_best_model.pkl` – best RF model
  * `scaler.pkl` – StandardScaler (X)
  * `target_scaler.pkl` – StandardScaler (y)
* **outputs/**
  * `mae_vs_estimators.png` – MAE curve
  * `rf_test_results.txt` – test-set metrics
  * `rf_validation_results.txt` – CV metrics
* `prediction.ipynb` – full pipeline notebook  
* `requirements.txt` – Python deps
* `LICENSE` - CC-BY-4.0
* `README.md`

---

## 📊 Data

**Raw inputs** (in `data/`):
- `attendance.csv` – per-game spectator counts, 2000–2019
- `games.csv` – game metadata (teams, scores, date)
- `standings.csv` – season-level team stats

**Processed artifacts**:
- `merged_unprocessed.csv` – joined on game identifier
- `merged_preprocessed.csv` – cleaned & ready for modeling
- *Splits:* train/val/test (70/15/15)

---

### Data Dictionary

See [DATA_DICTIONARY.md](DATA_DICTIONARY.md) for full schema.

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
