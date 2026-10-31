---
name: time-series-forecasting
description: Use when the user works with time-stamped data and needs help with time series analysis, forecasting, anomaly detection, seasonal decomposition, or temporal feature engineering for predictive models.
---

# Time Series Analysis & Forecasting

Respect the temporal structure of the data. Time series cannot be treated like IID tabular data.

## 1. Understand the temporal structure

Before modeling, inspect:

- **Frequency**: is the data hourly, daily, weekly, monthly, irregular? Check for missing timestamps and gaps.
- **Coverage**: how much historical data is available? Is it sufficient for the forecast horizon?
- **Trend**: is there an upward/downward long-term direction?
- **Seasonality**: are there repeating patterns? Daily, weekly, monthly, yearly cycles? Use seasonal decomposition (STL, `seasonal_decompose`) to separate trend, seasonal, and residual components.
- **Stationarity**: check with ADF test (Augmented Dickey-Fuller) and KPSS test. Differencing may be needed for ARIMA-family models.
- **Autocorrelation**: examine ACF and PACF plots to understand lag structure and inform model order.
- **Outliers and structural breaks**: identify regime changes, holidays, and one-off events.

## 2. Validation strategy — NEVER randomly split time series

- **Chronological train/test split**: training data must come entirely before test data.
- **Rolling-origin (expanding window)**: train on data up to time t, forecast t+1 to t+h, slide forward. This simulates real deployment.
- **Walk-forward validation**: the gold standard for time series cross-validation.
- **Embargo gap**: when features use lagged values, leave a gap between train and test to prevent leakage.
- **Never** use `train_test_split(shuffle=True)` on time series data. This is the most common and damaging mistake.

## 3. Baseline models

Always establish baselines before complex models:

| Baseline | Description |
|---|---|
| **Naive (last value)** | Forecast = most recent observation |
| **Seasonal naive** | Forecast = value from the same season last cycle |
| **Moving average** | Forecast = mean of last k observations |
| **Historical mean** | Forecast = overall training mean |

A model that cannot beat seasonal naive is not useful. Report baseline metrics alongside model metrics.

## 4. Classical statistical models

- **ARIMA/SARIMA**: for univariate series with trend and seasonality. Use `auto_arima` (pmdarima) for automated order selection, but inspect diagnostics (residual ACF, Ljung-Box test, Q-Q plot).
- **Exponential Smoothing (ETS)**: Holt-Winters for series with trend and multiplicative/additive seasonality. Use `statsmodels.tsa.holtwinters`.
- **Prophet**: for business time series with strong seasonal effects and holiday impacts. Good for quick baselines with interpretable components.
- **VAR**: for multivariate time series when variables Granger-cause each other.

## 5. ML-based approaches

- **Feature engineering for ML**: create lag features, rolling statistics (mean, std, min, max), day-of-week, month, holiday indicators, and Fourier terms for seasonality. All features must be available at prediction time — no future leakage.
- **Tree-based models**: LightGBM, XGBoost with temporal features. Use walk-forward validation, not random cross-validation.
- **Deep learning**: LSTM, GRU, Temporal Fusion Transformer, N-BEATS for large datasets with complex patterns. Typically not worth the complexity for <10K observations.

## 6. Multi-step forecasting strategies

- **Recursive (iterated)**: predict one step ahead, use prediction as input for the next step. Error compounds.
- **Direct**: train separate models for each horizon step. No error compounding but more models to maintain.
- **Multi-output**: single model predicts all future steps at once. Best when using deep learning architectures designed for this.

State which strategy is used and its trade-offs.

## 7. Anomaly detection in time series

- **Statistical**: values beyond μ ± 3σ on residuals after decomposition.
- **IQR-based**: on deseasonalized residuals.
- **Isolation Forest / LOF**: on temporal features for multivariate anomaly detection.
- **Prophet anomaly detection**: using prediction intervals.
- Always inspect flagged anomalies visually. Anomalies are investigation triggers, not automatic removal candidates.

## 8. Forecast evaluation metrics

| Metric | Use When |
|---|---|
| **MAE** | Interpretable, robust to outliers |
| **RMSE** | Penalizes large errors more heavily |
| **MAPE** | Percentage-based, but undefined when actuals are zero |
| **sMAPE** | Symmetric MAPE, handles zeros better |
| **MASE** | Scale-independent, compares against naive baseline. MASE < 1 means better than naive |
| **Coverage** | For prediction intervals: what fraction of actuals fall within the interval |

Report metrics on the holdout period. Visualize predictions versus actuals with prediction intervals.

## 9. Deliverable

Provide: temporal EDA with decomposition plots, stationarity tests, baseline model results, chosen model with walk-forward validation, forecast with prediction intervals, residual diagnostics, and practical next steps (retraining schedule, monitoring for drift).
