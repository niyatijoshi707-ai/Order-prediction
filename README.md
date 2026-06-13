# 🛒 Number of Orders Prediction — Retail Demand Forecasting with LightGBM

<div align="center">



---

## 🎯 Objective

Retail businesses need to **anticipate demand** to manage inventory, staff schedules, and logistics. Over-stocking is wasteful; under-stocking loses sales.

This project builds a **LightGBM regression model** that predicts the number of orders (`#Order`) for a supplement retail store based on:
- The **type of store** (S1–S4)
- The **location type** (L1–L5)
- Whether a **holiday** is active
- Whether a **discount** is being offered

---

## 📂 Dataset

| Property | Detail |
|---|---|
| **Source** | Supplement store sales data (CSV) |
| **Target Variable** | `#Order` — number of orders per record |
| **Features Used** | `Store_Type`, `Location_Type`, `Holiday`, `Discount` |
| **Train / Test Split** | 80% / 20% |

---

## 🧠 Why LightGBM?

LightGBM (Light Gradient Boosting Machine) is a **tree-based ensemble method** developed by Microsoft. It is chosen here because:

- **Fast training**: Uses histogram-based algorithms that are significantly faster than standard gradient boosting
- **Handles categoricals well**: After label encoding, tree-based models naturally partition on discrete feature values
- **No feature scaling needed**: Unlike linear models or neural networks, gradient boosting is scale-invariant
- **Excellent on structured/tabular data**: Consistently outperforms linear models on real-world tabular datasets

For a small feature set (4 features) with a continuous target, LightGBM provides strong predictive power without hyperparameter tuning.

---

## 🏗️ Pipeline

```
supplement.csv
     │
     ▼
Exploratory Analysis
  - Pie charts: Store ID, Store Type, Location Type, Discount, Holiday distributions
     │
     ▼
Label Encoding (Ordinal Mapping)
  Discount:       No → 0,  Yes → 1
  Holiday:        No → 0,  Yes → 1
  Store_Type:     S1 → 1,  S2 → 2,  S3 → 3,  S4 → 4
  Location_Type:  L1 → 1, ..., L5 → 5
     │
     ▼
Feature Matrix X = [Store_Type, Location_Type, Holiday, Discount]
Target Vector  y = [#Order]
     │
     ▼
Train/Test Split (80% / 20%, random_state=42)
     │
     ▼
LightGBM Regressor — fit on X_train, y_train
     │
     ▼
Predict on X_test
     │
     ▼
Evaluate: MAE, MSE
Visualize: Actual vs. Predicted scatter plot
Feature Importance bar chart
```

---

## ⚙️ What Each Step Does & Why

| Step | What it is | Why it's used here |
|---|---|---|
| **Plotly Pie Charts** | Interactive distribution plots | Understand balance/imbalance across store types, locations, holidays, discounts |
| **Ordinal Encoding** | Maps category strings to integers | LightGBM accepts numeric arrays; ordinal encoding preserves natural ordering (S1 < S4, L1 < L5) |
| **LGBMRegressor** | Gradient boosted decision trees (regression) | Strong baseline for tabular demand forecasting with minimal tuning |
| **MAE** (Mean Absolute Error) | Average absolute prediction error | Interpretable in the same unit as `#Order`; robust to outliers |
| **MSE** (Mean Squared Error) | Penalizes large errors quadratically | Useful for detecting cases where predictions are wildly off |
| **Scatter Plot (Actual vs. Predicted)** | Visual alignment check | Points clustering near the diagonal = good predictions |
| **Feature Importance** | LightGBM's built-in split importance scores | Reveals which of the 4 features drives order count the most |

---

## 📈 Results

The model outputs:

- **MAE** and **MSE** printed to console
- **Actual vs Predicted scatter plot** — proximity to the diagonal indicates accuracy
- **Feature importance table** — sorted to show which variable (Store_Type, Location_Type, Holiday, Discount) most influences order volume

---

## 🗂️ Project Structure

```
order_prediction/
├── Numbers_of_order_predictions_Niyati_Joshi.ipynb
└── README.md
```

---

## 🛠️ Tech Stack

- **Python 3.10**
- **LightGBM** — gradient boosting regression
- **Pandas** — data loading, encoding, feature engineering
- **NumPy** — array manipulation
- **Plotly Express** — interactive pie chart visualizations
- **Matplotlib** — scatter plot for actual vs. predicted
- **Scikit-learn** — `train_test_split`, `mean_absolute_error`, `mean_squared_error`

---

## 🚀 How to Run

```bash
# Upload supplement.csv when prompted in Colab, or adjust path for local run

jupyter notebook Numbers_of_order_predictions_Niyati_Joshi.ipynb
```

---

## 💡 Key Insight

> With only 4 features, LightGBM can still surface meaningful demand signals. The feature importance output answers a real business question: **does holiday status matter more than store type?** Does offering a discount actually drive more orders, or is location type the dominant factor? This model makes those answers quantifiable.

---

## 👩‍💻 Author

**Niyati Joshi** — Turning transaction data into actionable business intelligence.

---

<div align="center"><i>Better forecasts mean better decisions — and fewer empty shelves.</i></div>
