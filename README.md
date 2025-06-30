# Forecasting Daily Wikipedia Pageviews for Figma (Software)

This project forecasts daily Wikipedia pageviews for the **Figma (software)** page from early 2024 through mid-2026. The work was completed as part of a Data Science Intern assessment.

---

## 📝 Problem Statement

Given historical daily pageviews data (2022–2025), the objectives were to:

- Analyze patterns and detect structural breaks.
- Build an interpretable time series forecasting model.
- Predict daily traffic up to June 30th, 2026.
- Justify all methodological choices.

---

## ⚙️ Methodology Overview

1. **Data Exploration**
   - Loaded and visualized daily pageviews split by year.
   - Identified a significant drop in traffic in late 2023 (structural break).
   - Chose to model only 2024 onward for more stable behavior.

2. **Preprocessing**
   - Applied `log1p` transformation to stabilize variance.
   - Conducted Augmented Dickey-Fuller (ADF) tests to assess stationarity.
   - Performed first-order differencing (`d=1`) to achieve stationarity.

3. **Model Selection**
   - Used ACF and PACF plots to select ARIMA orders:
     - ACF lag-1 autocorrelation suggested `q=1`.
     - PACF lag-1 cutoff suggested `p=1`.
   - Detected strong weekly seasonality (7-day cycles), so set seasonal order `(1,0,1,7)`.
   - Selected **Seasonal ARIMA (SARIMA)** as the final model:
     - `order=(1,1,1)`
     - `seasonal_order=(1,0,1,7)`

4. **Model Evaluation**
   - Backtested on the last 90 days of data.
   - Evaluation metrics:
     - **Mean Absolute Error (MAE):** ~8.47
     - **Root Mean Squared Error (RMSE):** ~10.71

5. **Forecasting**
   - Trained the model on all available data from Jan 2024–May 2025.
   - Forecasted daily views up to June 30th, 2026.
   - Inverse-transformed predictions back to original scale.

---

Full forecast data is available in:

```
outputs/forecast_mid_next_year.csv
```

---

## 🛠️ Libraries Used

- pandas
- numpy
- matplotlib
- seaborn
- statsmodels
- scikit-learn
- jupyter

---

**SARIMA** was selected because:

- The data exhibits **clear weekly seasonality**.
- Differencing and ACF/PACF supported autoregressive and moving average terms.
- The model is interpretable and reproducible.
- Simpler and more transparent than black-box models (like LSTM).

---

