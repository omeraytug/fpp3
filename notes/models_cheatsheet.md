## Linear Regression

Models the relationship between a target variable and one or more explanatory (external) variables. Assumes that the residuals (errors) are **independent white noise**, meaning they contain no remaining information that can be used for prediction.

---

## Dynamic Regression (Regression with AR Terms)

A linear regression model that also includes **lagged values of the target** as predictors. It captures the influence of both external variables and the series' own past values. Residuals are still assumed to be **white noise**.

---

## SARIMA

A univariate time series model that uses only the history of the target series. It models:
- **AR (AutoRegressive):** dependence on past values.
- **I (Integrated):** differencing to achieve stationarity.
- **MA (Moving Average):** dependence on past forecast errors (residuals).
- **Seasonal components:** seasonal AR, differencing, and MA.

No external regressors are used.

---

## SARIMAX (Regression with SARIMA Errors)

A linear regression model with external variables whose residuals are modeled by a SARIMA process instead of being assumed to be white noise.

- **Regression part:** captures the effects of external variables.
- **SARIMA part:** captures the remaining autocorrelation in the residuals.

Also known as **Regression with SARIMA (ARIMA) Errors**.