Here is a polished `README.md` for your **Playground Series S5E4 - Podcast Listening Time Prediction** Kaggle project, incorporating all the steps and logic from your notebook:

---

````markdown
# 🎧 Podcast Listening Time Prediction

Predict how long listeners will tune into a podcast episode based on various features using ensemble learning and cross-validation.

📍 **Competition**: [Kaggle Playground Series - Season 5, Episode 4](https://www.kaggle.com/competitions/playground-series-s5e4)  
📊 **Author**: [Dur-e Yashfeen](https://www.kaggle.com/dureyashfeen)

---

## 📁 Dataset Overview

- `train.csv` – 750,000 podcast episodes with metadata and `Listening_Time_minutes` (target).
- `test.csv` – Test episodes without the target.
- `sample_submission.csv` – Format for predictions.

### Key Features:
- `Podcast_Name`, `Episode_Title`
- `Episode_Length_minutes`
- `Genre`, `Host_Popularity_percentage`, `Guest_Popularity_percentage`
- `Publication_Day`, `Publication_Time`
- `Number_of_Ads`, `Episode_Sentiment`

---

## 🔍 Exploratory Data Analysis

### Missing Values:
- `Guest_Popularity_percentage`: ~19%
- `Episode_Length_minutes`: ~12%
- `Number_of_Ads`: ~0%

➡️ **Strategy**: Filled all missing values with column means.

### Target Distribution:
Plotted `Listening_Time_minutes` using Plotly (histogram + violin).

---

## 🧹 Preprocessing

- **Label Encoding** applied to:
  - Categorical columns: `Genre`, `Publication_Day`, `Publication_Time`, `Episode_Sentiment`, `Podcast_Name`, `Episode_Title`
- **Dropped Columns**:
  - `Podcast_Name`, `Episode_Title`, and `id` (from features)

---

## 🧠 Model Training

### 🎯 Target:
- `Listening_Time_minutes`

### 📌 Features:
- All numerical + encoded categorical features

### 📊 Models Tried:
- `RandomForestRegressor`
- `GradientBoostingRegressor`
- `XGBoost`
- ✅ `LightGBM` (best performance)

### ✅ Final Model:
```python
final_model = lgb.LGBMRegressor(n_estimators=300, random_state=42)
final_model.fit(X, y)
````

---

## 🔁 Cross-Validation

Used 5-Fold Cross-Validation with LightGBM:

```python
LightGBM CV RMSE: ~13.10
```

---

## 📤 Submission

```python
sample_submission['Listening_Time_minutes'] = preds
sample_submission.to_csv('submission.csv', index=False)
```

---

## 📌 Results Sample

| id     | Listening\_Time\_minutes |
| ------ | ------------------------ |
| 750000 | 56.01                    |
| 750001 | 18.58                    |
| 750002 | 49.79                    |
| 750003 | 79.10                    |
| 750004 | 48.39                    |

---

## 🚀 Future Improvements

* Use NLP on `Podcast_Name` or `Episode_Title`
* Use target-aware encoding instead of Label Encoding
* Add feature engineering (e.g., time bins, title length)
* Try model stacking and tuning hyperparameters

---

## 👩‍💻 Author

**Dur-e Yashfeen**
