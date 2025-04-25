# 🏈 NFL Stadium Attendance Prediction using Random Forest

This repository contains a complete machine learning pipeline for predicting weekly NFL stadium attendance using a `RandomForestRegressor`. The model was trained and evaluated on a custom-preprocessed dataset constructed from publicly available Kaggle data.

---

## 📁 Project Structure

| File | Description |
|------|-------------|
| `hyp_tuning_best_model.pkl` | Trained Random Forest model (best params from GridSearchCV) |
| `scaler.pkl` | `StandardScaler` for input features (X) |
| `target_scaler.pkl` | `StandardScaler` for target variable (y) |
| `prediction.ipynb` | Jupyter notebook containing full ML pipeline |
| `requirements.txt` | Python packages required to run the notebook |
| `rf_test_results.txt` | Evaluation metrics on the held-out test set |
| `rf_validation_results.txt` | Evaluation metrics on the validation set |
| `mae_vs_estimators.png` | Plot: MAE vs. number of estimators |
| `merged_preprocessed.csv` | Fully cleaned and transformed dataset |
| `merged_unprocessed.csv` | Original merged dataset before preprocessing |
| `input.csv` | Example input for inference (preprocessed format) |

---

## 🧠 Model Summary

- **Algorithm**: Random Forest Regressor (`sklearn.ensemble`)
- **Tuning Method**: `GridSearchCV` (3-fold CV)
- **Best Parameters**:
  - `n_estimators`: 250
  - `max_depth`: None
  - `min_samples_split`: 2
  - `min_samples_leaf`: 3
  - `max_features`: None
- **Target**: Weekly NFL stadium attendance

---

## 🧪 Data Source

The dataset was created by merging the following files from [Kaggle](https://www.kaggle.com/datasets/sujaykapadnis/nfl-stadium-attendance-dataset) by Sujay Kapadnis:

- `games.csv`
- `standings.csv`
- `attendance.csv`

---

## ⚙️ Preprocessing Steps

- One-hot encoding of categorical features
- Scaling of numerical features using `StandardScaler`
- Scaling of target variable for model training
- 70/15/15 split into training, validation, and test sets

---

## 🧾 Usage

To run predictions:

1. Load `hyp_tuning_best_model.pkl`
2. Scale your input using `scaler.pkl`
3. Predict with the model
4. Inverse-transform predictions using `target_scaler.pkl`

---

## 📚 Citation

If you use this model or data in your work, please cite it as:

> [Your Full Name], *NFL Stadium Attendance Prediction using Random Forest*, TU Wien, 2025.  
> DOI: [Add your TUWRD/Zenodo DOI here]


---

## 🛡 License

- **Model, Code, and Scalers**: CC BY 4.0
- **Original Dataset (Kaggle by Sujay Kapadnis)**: Licensed for academic use — check [dataset page](https://www.kaggle.com/datasets/sujaykapadnis/nfl-stadium-attendance-dataset) for full terms.


```python
import pickle

# Load model and scalers
model = pickle.load(open("hyp_tuning_best_model.pkl", "rb"))
scaler = pickle.load(open("scaler.pkl", "rb"))
target_scaler = pickle.load(open("target_scaler.pkl", "rb"))
