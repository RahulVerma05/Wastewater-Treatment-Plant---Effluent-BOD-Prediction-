# Wastewater Treatment Plant - Effluent BOD Prediction

I am a chemical engineering student and I wanted to build something related to my field, so I picked wastewater treatment as the topic. The goal is to predict the effluent BOD (Biological Oxygen Demand) of a wastewater treatment plant based on influent parameters like flow rate, inlet BOD, COD, and suspended solids.

---

## What is this project about?

In a wastewater treatment plant, we receive raw sewage (influent) and treat it before releasing it back into the environment (effluent). The quality of the treated water is measured using parameters like BOD, COD, and suspended solids. 

BOD (Biological Oxygen Demand) is one of the most important parameters — it tells us how much organic matter is present in the water. Lower effluent BOD means better treatment.

The idea here is simple — can we predict the effluent BOD just by looking at what's coming into the plant? That's what this model tries to do.

---

## Dataset

I used a synthetic dataset that I generated based on real wastewater treatment plant operating parameters and standard CPCB (Central Pollution Control Board) discharge norms. The dataset has 1000 rows simulating daily plant operation.

| Feature | Description | Unit |
|---|---|---|
| Q-E | Influent flow rate | m³/day |
| DBO-E | Influent BOD | mg/L |
| DQO-E | Influent COD | mg/L |
| SS-E | Influent Suspended Solids | mg/L |
| PH-E | Influent pH | — |
| PH-S | Effluent pH | — |
| DBO-S | Effluent BOD (target) | mg/L |
| DQO-S | Effluent COD | mg/L |
| SS-S | Effluent Suspended Solids | mg/L |

---

## What I did

### 1. EDA (Exploratory Data Analysis)
- Plotted flow rate vs BOD, COD, SS, and pH at both inlet and outlet
- Created a correlation heatmap to understand which features affect effluent BOD the most
- Found that inlet BOD (DBO-E) and inlet COD (DQO-E) are the strongest predictors

### 2. Preprocessing
- No missing values in the dataset
- Selected features based on correlation: Q-E, DBO-E, DQO-E, SS-E
- Applied StandardScaler — fitted only on training data to avoid data leakage
- 80/20 train-test split

### 3. Models I tried
I compared three models:
- Linear Regression (baseline)
- Random Forest
- XGBoost

### 4. Results

| Model | RMSE | MAE | R² |
|---|---|---|---|
| Linear Regression | — | — | — |
| Random Forest | — | — | — |
| XGBoost | 3.81 | — | 0.8988 |

XGBoost gave the best results with R² of 0.8988 — meaning the model explains about 90% of the variance in effluent BOD.

### 5. SHAP Analysis
I used SHAP (SHapley Additive exPlanations) to understand which features were driving the predictions. The SHAP summary plot and waterfall plot both confirmed that inlet BOD and inlet COD are the two most important features — which makes sense from a chemical engineering perspective.

---

## What I learned

- How to build a regression pipeline from scratch
- The importance of fitting the scaler only on training data (data leakage is a real issue)
- How to use SHAP to explain model predictions
- That domain knowledge helps a lot — knowing what BOD and COD mean made it easier to interpret the results

---

## Libraries used

- pandas, numpy
- matplotlib, seaborn
- scikit-learn
- xgboost
- shap

---

## How to run

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost shap
jupyter notebook WasteWater_treatment_prediction.ipynb
```

---
