### 📈 FORECASTING TECH & ENERGY STOCKS THROUGH MACROECONOMIC DISRUPTION

### Overview

Retail investors often lack the macro-aware tools available to institutions. This project investigates whether macroeconomic signals (inflation, Treasury yields, consumer sentiment) and policy events genuinely improve stock price forecasting compared to historical data alone. By evaluating 14 tech and energy tickers—sectors that react differently to economic disruption—this study rigorously tests the value of macro-features against a naive baseline to prevent the risks of trading on statistical noise. Developed within the **AI4ALL Ignite** accelerator.

---

### 📊 Key Findings

* **The Random Walk Baseline:** Using price history alone, the ARIMA model did not outperform a naive "no change" forecast for any of the 14 tickers.
* **Volatility & External Shocks:** Forecast errors clustered heavily around real-world tariff shocks (April 2025, June 2026). Low-volatility stocks (e.g., ET) closely aligned with the naive baseline, while high-volatility stocks (e.g., META) exhibited the largest absolute errors.
* **The Cost of Complexity:** Adding macro and cross-ticker features to a Linear Regression model actually *increased* the average RMSE. This highlights that feeding models more features does not automatically yield better predictions, largely due to multicollinearity and missing-data imputation.
* **Methodological Corrections:** Identified and resolved standard data science pitfalls that artificially inflate model accuracy, including replacing a one-shot ARIMA with a rolling forecast, fixing data leakage in regression train/test splits, and correcting multi-scale RMSE calculations in the deep learning architecture.

---

### 🧠 Methodology

A three-tier modeling approach was designed to isolate the impact of different data inputs:

1. **ARIMA (Univariate Baseline):** Forecasted price using only its own history (automated via `auto_arima`). Evaluated using a rolling forecast to prevent compounding errors.
2. **Linear Regression (Feature Testing):** Compared a baseline set (price/volume) against a full feature set (adding macroeconomic variables) to directly quantify the value of macro signals.
3. **CNN-LSTM (Deep Learning):** Leveraged a sequence-to-sequence architecture (Conv1D encoder, LSTM encoder-decoder) to process all 42 features simultaneously over a 126-day lookback window.

---

### 🗄️ Data Architecture

Processed a dataset covering **1,254 trading days** (July 2021–July 2026). The final dataset included 42 raw features alongside engineered technical indicators (20/50-day SMA, 10-day momentum, 20-day rolling volatility, 14-day RSI). Standardized evaluation using MAE, RMSE, and MAPE enabled fair cross-ticker comparisons.

Data Sources:

* **Market Data:** Daily OHLCV for 14 tickers (7 Tech, 7 Energy).
* **FRED:** Resampled CPI (CPIAUCSL) and Consumer Sentiment (UMCSENT).
* **U.S. Treasury:** Daily Par Yield Curve Rates.
* **USTR:** Custom tariff-event calendar curated from Trade Policy Press Releases.

---

### 💻 Technologies Used

**Languages & Core Libraries:** Python, Pandas, NumPy
**Machine Learning & Modeling:** TensorFlow,Keras (CNN-LSTM), Scikit-Learn, Statsmodels, pmdarima
**Data & Visualization:** pandas-datareader, Matplotlib, Seaborn

---

This project was completed in collaboration with Shannon Chiang and Abby Lei.
