# Marketing Analytics & User Growth Modeling

## 📌 Project Overview
This project is an end-to-end data science pipeline that simulates, analyzes, and predicts Daily Active Users (DAU) based on marketing expenditures, time trends, and seasonal effects. The workflow includes custom data generation (Simulation), Exploratory Data Analysis (EDA), Statistical Testing, Time Series Analysis, and Predictive Modeling using Linear Regression and SARIMAX.

## ⚙️ Data Simulation
To mimic real-world business scenarios, the dataset (180 days) was synthetically generated using a deterministic mathematical model combined with Poisson noise. 

The base formula for daily users:
$$Users\_Base = 100 + 3(Ad\_Spend) + 1.5(Ad\_Spend\_Lag1) + 2(Day) - 0.01(Day^2) + 50(is\_weekend)$$

**Key Features:**
*   `Ad_Spend`: Daily advertising budget.
*   `Ad_Spend_Lag1`: Carry-over effect of yesterday's ad spend.
*   `Day` & `Day^2`: Non-linear (parabolic) time trend.
*   `is_weekend`: Binary flag for weekend spikes.

## 📊 Exploratory Data Analysis (EDA)
Thorough EDA was conducted to validate the simulated patterns. 

*   **Weekend vs. Weekday Traffic:**
    ![Weekend Boxplot](path/to/your/boxplot_image.png)
    *(Shows a clear spike in users during weekends.)*

*   **Ad Spend vs. Users:**
    ![Scatter Plot](path/to/your/scatter_image.png)
    *(Demonstrates the strong positive linear relationship.)*

*   **Correlation Matrix:**
    ![Correlation Heatmap](path/to/your/heatmap_image.png)
    *(Highlights `Ad_Spend` as the most highly correlated feature with target variable.)*

## 📈 Time Series Analysis
The target variable was analyzed for stationarity and seasonal patterns.
*   **Decomposition (Trend, Seasonality, Residuals):**
    ![Decomposition Plot](path/to/your/decomposition_image.png)
*   **Autocorrelation (ACF & PACF):** Significant lags were found at 1 and 7 days.
*   **ADF Test:** Confirmed the series is stationary ($p-value \approx 0.0067$).
    ![ACF PACF Plots](path/to/your/acf_pacf_image.png)

## 🚀 Modeling & Results
Three models were trained and evaluated to predict daily users:
1.  Simple Linear Regression (Baseline)
2.  **Linear Regression + $Day^2$ (Best Performing)**
3.  SARIMAX (Time Series Modeling)

### 📊 Model Accuracy and Performance Evaluation

To evaluate the accuracy and effectiveness of the models used for predicting the number of users, three different approaches were compared: **Simple Linear Regression**, **Linear Regression with a quadratic time term ($Day^2$)**, and the **SARIMAX** model.  
The comparison is based on three key metrics: **MAE**, **RMSE**, and **R²**.

### Performance Comparison

| Model | MAE | RMSE | R² |
|------|:---:|:----:|:---:|
| **Linear Regression** | 19.91 | 25.60 | 0.9009 |
| **Linear Regression + Quadratic Term ($Day^2$)** | **12.51** | **15.86** | **0.9619** |
| **SARIMAX** | 12.52 | 15.86 | 0.9605 |


### 📌 Key Findings
*   The **Linear Regression + $Day^2$** model achieved the highest performance ($R^2 = 0.9619$). 
*   **Parameter Recovery:** The model successfully recovered the exact hidden parameters used during the simulation phase (e.g., estimating `Ad_Spend` coefficient as 2.82, very close to the true value of 3).
*   **Residual Analysis:** Residuals were randomly distributed around zero, confirming the validity of the OLS assumptions.

![Residuals Plot](path/to/your/residuals_image.png)

---
## ✅ Conclusion

This project demonstrates a full data science cycle — from synthetic data generation to predictive modeling — on a marketing analytics problem. The **Linear Regression + $Day^2$** model proved most effective ($R^2 = 0.9619$), successfully recovering the true simulation parameters and confirming that ad spend, carry-over effects, and non-linear time trends are the primary drivers of user growth.

---

## 🔭 Future Work

- **Real Data Integration:** Replace synthetic data with actual marketing and user metrics to validate model generalizability.
- **Feature Expansion:** Incorporate additional signals such as campaign type, channel-level spend, or competitor activity.
- **Automated Retraining:** Build a pipeline that retrains the model periodically as new data arrives, enabling production-ready forecasting.

