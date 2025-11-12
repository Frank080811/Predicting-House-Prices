<p align="left">
  <img src="blogo.jpg" alt="BentJun Logo" style="width:150px; height:auto;" />
</p>

# 🏠 King County House Price Prediction

## 📘 Introduction

This project aims to predict **house sale prices in King County (USA)** — which includes Seattle and surrounding areas — based on various property attributes such as square footage, number of bedrooms/bathrooms, and location features.  

The study uses **supervised machine learning regression models** to determine which features most strongly influence housing prices and to build a model capable of accurately predicting them.  

**Dataset:**  
The dataset used in this project is available on Kaggle:  
👉 [King County House Sales Dataset](https://www.kaggle.com/datasets/minasameh55/king-country-houses-aa)

---

## 🔍 Data Exploration & Understanding

The dataset contains **21 columns and 21,613 observations** of house sales between **May 2014 and May 2015**.  
Key variables include:
- `price`: Sale price of the house (target variable)
- `bedrooms`, `bathrooms`: Number of rooms
- `sqft_living`, `sqft_lot`: Living area and lot size
- `floors`, `waterfront`, `view`, `condition`, `grade`: Qualitative property attributes
- `yr_built`, `yr_renovated`: Construction and renovation year
- `zipcode`, `lat`, `long`: Location information
- `sqft_living15`, `sqft_lot15`: Averages for the neighborhood (15 nearest neighbors)

### Key Findings
- Prices range from **\$75,000 to \$7,700,000**, with a median of around **\$450,000**.  
- **Living area (`sqft_living`)**, **grade**, and **bathrooms** show the strongest correlation with price.  
- Several features (like `sqft_living15`, `grade`, and `view`) are strongly correlated with property value.

---

## 🧹 Data Preprocessing
The following steps were applied before model training:

1. **Handling missing values**
   - Checked and imputed or dropped columns with excessive missingness.
2. **Feature engineering**
   - Created new ratios and log transformations (`log1p_price`, `lot15_ratio`, etc.) to stabilize skewed data.
3. **Encoding categorical variables**
   - Converted non-numeric features (`zipcode`, `waterfront`, etc.) using one-hot or label encoding.
4. **Feature scaling**
   - Applied `StandardScaler` for linear models and left tree-based models unscaled.
5. **Data splitting**
   - Split dataset into **80% training** and **20% testing** sets using `train_test_split`.

---

## 📊 Exploratory Data Analysis (EDA)
- **Correlation analysis** highlighted strong relationships between living area, grade, and price.  
- **Distribution plots** showed positive skewness in price and square footage — corrected using `log1p` transformation.  
- **Heatmaps and pairplots** were used to identify multicollinearity and potential outliers.  

---

## 🤖 Model Development
A variety of regression and ensemble models were tested to identify the best-performing one:

| Model | Type |
|-------|------|
| Linear Regression | Baseline model |
| Ridge & Lasso Regression | Regularized linear models |
| Elastic Net | Hybrid regularization |
| Random Forest Regressor | Bagging ensemble |
| Gradient Boosting Regressor | Boosting ensemble |
| AdaBoost Regressor | Boosting ensemble |
| XGBoost Regressor | Optimized boosting |
| Support Vector Regressor (SVR) | Kernel-based regression |

---

## 📈 Model Evaluation

Models were compared using the following metrics:
- **R² Score** (Coefficient of Determination)
- **Mean Absolute Error (MAE)**
- **Root Mean Squared Error (RMSE)**
- **Cross-validated R² (5-fold)**

| Model | R² (Train) | R² (Test) | CV R² Mean | MAE | RMSE |
|-------|-------------|-----------|-------------|-----|------|
| Gradient Boosting | 0.9999 | 0.9996 | 0.9991 | 2,710 | 7,319 |
| Random Forest | 0.9997 | 0.9995 | 0.9983 | 501 | 8,807 |
| AdaBoost | 0.9651 | 0.9702 | 0.9644 | 52,464 | 67,174 |
| XGBoost | 0.9998 | 0.9684 | 0.9804 | 6,843 | 69,083 |
| Ridge Regression | 0.8648 | 0.8522 | 0.8576 | 78,828 | 149,499 |

---

## 🏆 Model Selection and Justification
**Gradient Boosting Regressor** was selected as the final model because:
- It achieved the **highest R² on test data (0.9996)** and excellent generalization across folds.  
- The model balances **bias-variance tradeoff** better than Random Forest (slightly less overfitting).  
- Ensemble boosting techniques handle complex, nonlinear relationships effectively.

After feature leakage removal (`log1p_price` excluded), Gradient Boosting remained the **most stable and interpretable** performer, with key predictors including:
- `sqft_living`
- `grade`
- `bathrooms`
- `lat`, `long`
- `yr_built`

---

## 🔍 Feature Importance
Top predictive factors identified by the Gradient Boosting model:
1. `sqft_living` — Size of the living area
2. `grade` — Quality of construction and design
3. `bathrooms`
4. `lat` / `long` — Geographic location
5. `sqft_above`
6. `sqft_living15` — Neighborhood living space

These factors collectively explain most of the variation in property prices.

---

## 🧾 Conclusion
- **Objective:** To predict house prices accurately and understand major price determinants.  
- **Outcome:** Gradient Boosting delivered the most accurate and generalizable model (R² ≈ 0.9996).  
- **Key Drivers:** Property size, grade, bathrooms, and geographic coordinates are dominant predictors.  
- **Future Work:**
  - Apply regularization or hyperparameter tuning to reduce minor overfitting.
  - Integrate more recent or external features (e.g., school quality, economic indicators).
  - Deploy the model as an interactive dashboard using Streamlit or FastAPI.

---

## 🧠 Technologies Used
- **Python 3.10+**
- **Libraries:** pandas, numpy, matplotlib, seaborn, scikit-learn, xgboost
- **Environment:** Jupyter Notebook / VS Code
- **Version Control:** Git + GitHub
- **Data Source:** [Kaggle - King County House Sales](https://www.kaggle.com/datasets/minasameh55/king-country-houses-aa)

---

## 👩‍💻 Author
**[Frank Sarfo]**  
Data Scientist | Machine Learning Engineer  
📧 francbenz92@gmail.com  
📍 MSc in Data Science, Arden University

---

> 📝 *“A model is only as good as the data and the questions that shaped it.”*








