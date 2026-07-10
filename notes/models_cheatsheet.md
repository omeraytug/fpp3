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


## SARIMA vs. SARIMAX

### SARIMA

A **univariate time series model** that models the target series directly using its own history.

- No linear regression component.
- No external (exogenous) variables.
- Uses:
  - **AR:** past values of the target.
  - **I:** differencing to achieve stationarity.
  - **MA:** past forecast errors (residuals).
  - Seasonal AR, I, and MA components.

The model learns only from the target series itself.

---

### SARIMAX

A **linear regression model with SARIMA errors**.

- Starts conceptually with a linear regression:
  \[
  y_t = \beta X_t + \eta_t
  \]
- The regression models the effect of the external variables.
- The residual process \(\eta_t\) is assumed to follow a SARIMA model rather than being white noise.

Unlike ordinary linear regression, the residuals are **not** assumed to be independent. Instead, they are modeled using AR, I, MA, and seasonal components.

> **Note:** The regression coefficients and SARIMA parameters are estimated **simultaneously** using maximum likelihood, not in separate steps.

SARIMAX contains a linear regression component, but its parameters are not estimated using ordinary least squares. Instead, the regression coefficients and the SARIMA parameters are estimated jointly using maximum likelihood (or a similar likelihood-based method).