# Machine Learning Analysis: Flight Prices and Optimal Booking Time

This project leverages machine learning techniques to conduct an in-depth analysis of the factors influencing flight prices and builds a high-performance predictive model. The core objective is to answer a critical question for travelers: **When is the best time to book a flight?**

## 🚀 Core Conclusion: The Optimal Booking Window

Through exploratory data analysis, a Gradient Boosting Machine (LightGBM) model, and model interpretation techniques (like Partial Dependence Plots), this project reaches a clear and actionable conclusion:

> **Optimal Booking Window:**
> The analysis definitively shows that the best (i.e., lowest and most stable) time to book a flight is **between 20 and 50 days in advance**.
>
> **Price Surge Point:**
> Booking **within 20 days** of the departure date results in a sharp and significant price increase.

---

## 📂 Project Workflow

This project follows an end-to-end data science workflow, from data exploration to final model interpretation.

### 1. Data Exploration and Preparation

* **Dataset:** The analysis is based on the `Clean_Dataset.csv` file.
* **Target Variable:** The target variable `price` is highly right-skewed. A log transformation (`log_price`) was applied before modeling to stabilize the distribution and improve model training.
* **Feature Engineering:**
    * **`stops`:** Ordinally encoded text values (e.g., 'zero', 'one', 'two_or_more') to numerical values (0, 1, 2) to preserve their inherent order.
    * **`route`:** A new `route` feature was created by combining `source_city` and `destination_city` (e.g., 'Delhi-Mumbai') to allow the model to learn route-specific price patterns.

### 2. Exploratory Data Analysis (EDA)

Data visualization revealed several key pricing drivers:

* **Price vs. Days Left:** Initial plots showed a strong, non-linear relationship between price and `days_left`.
* **Service Class:** `Business` class flights have a significantly higher median price and wider price distribution than `Economy` class.
* **Airline:** A clear pricing hierarchy exists among airlines, with full-service carriers like Vistara and Air India showing the highest median prices.
* **Time of Day:** 'Late_Night' departures are, on average, the cheapest, while 'Morning' and 'Night' departures are more expensive.

### 3. Modeling and Validation

* **Task Type:** This is a supervised regression task.
* **Feature Selection:**
    * **Numerical Features:** `duration`, `days_left`.
    * **Categorical Features:** `airline`, `departure_time`, `stops`, `arrival_time`, `class`, `route`.
* **Model Selection:**
    1.  **Baseline Model:** `Linear Regression`.
    2.  **Final Model:** `LGBMRegressor` (LightGBM). This was chosen for its state-of-the-art performance on tabular data and its ability to natively handle complex non-linear relationships and feature interactions discovered during EDA.
* **Validation:** The dataset was split into an 80% training set and a 20% testing set.

---

## 📊 结果与模型洞察

### 模型性能

The performance of the models in predicting the *original* price (after converting `log_price` predictions back) is compared below. The LightGBM model significantly outperformed the linear baseline, confirming the importance of modeling the data's non-linearity.

| Model | $R^2$ (R-squared) | MAE (Mean Absolute Error) |
| :--- | :--- | :--- |
| Linear Regression (Baseline) | 0.8837 | 4550.68 |
| **LightGBM (Final Model)** | **0.9191** | **3588.02** |

### Key Price Drivers

1.  **Feature Importance:**
    According to the trained LightGBM model, the most important features for predicting price are:
    1.  **`duration`:** Importance Score: 285
    2.  **`days_left`:** Importance Score: 200
    3.  **`airline_Air_India`:** Importance Score: 82
    4.  **`airline_AirAsia`:** Importance Score: 61
    5.  **`airline_Vistara`:** Importance Score: 58

    `class_Business` was also ranked as a top-10 most important feature.

2.  **The "Price-Booking" Curve (Partial Dependence Plot - PDP):**
    To deeply understand the impact of `days_left`, a Partial Dependence Plot (PDP) was generated. This plot isolates the marginal effect of `days_left` on the predicted price, averaging out all other features.

    * The plot clearly shows a sharp drop in price (partial dependence) as `days_left` increases from 0 to 20.
    * **After the ~20-day mark,** the curve flattens, remaining at its lowest level within the 20 to 50-day window.

    This insight provides definitive, model-based confirmation of the core conclusion.

---

## 🛠️ How to Run This Project

### Dependencies

This project relies on the standard Python data science ecosystem. You can install them using `pip`:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn lightgbm
、、、

