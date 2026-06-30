# ARIMA Model Building Workflow

Building an ARIMA model follows a logical sequence. The first step is to make the time series **stationary**, the second is to determine the model orders, the third is to estimate the model coefficients, and the final step is to evaluate whether the fitted model is adequate.

## 1. Make the series stationary

The first task is to determine the differencing order, **$d$**. A stationary series has a constant mean and variance over time and does not exhibit a trend or changing seasonal patterns.

The differencing order is usually determined by inspecting the time series plot and differencing the data until the trend (and other forms of non-stationarity) are removed. Statistical tests such as the **Augmented Dickey-Fuller (ADF)** test or the **KPSS** test can also help assess stationarity.

**ACF and PACF are *not* used to determine the differencing order.**

---

## 2. Choose the AR and MA orders

Once the series is stationary, the next step is to determine the autoregressive order **$p$** and the moving average order **$q$**.

When selecting the model manually, the **PACF** is used as a guide for choosing the **AR order ($p$)**, while the **ACF** is used as a guide for choosing the **MA order ($q$)**.

These plots provide suggestions rather than exact answers, so it is common to compare several candidate models before deciding on the final specification.

---

## 3. Estimate the model coefficients

After selecting the model orders **$(p, d, q)$**, the model parameters are estimated.

These include:

- **$c$** – constant (or drift, if included)
- **$\phi_1, \phi_2, \ldots, \phi_p$** – autoregressive (AR) coefficients
- **$\theta_1, \theta_2, \ldots, \theta_q$** – moving average (MA) coefficients

The estimation is most commonly performed using **Maximum Likelihood Estimation (MLE)**, although **Conditional Least Squares (CLS)** can also be used in some implementations.

---

## 4. Evaluate the fitted model

After fitting the model, the residuals should be examined to ensure that the model has captured all of the information in the data.

The residuals should resemble **white noise**, meaning they should have no remaining autocorrelation. This is typically checked by inspecting the **ACF of the residuals** and, if desired, performing a **Ljung–Box test**. If significant autocorrelation remains, a different ARIMA specification may be required.

---

# Modern ARIMA Workflow

Modern software such as `auto_arima()` automates much of this process.

Instead of relying primarily on manual ACF and PACF inspection, it typically:

1. Determines the differencing order **$d$** using unit-root tests.
2. Tries many combinations of **$p$** and **$q$**.
3. Estimates the model coefficients using **Maximum Likelihood Estimation (MLE)**.
4. Compares candidate models using information criteria such as **AIC**, **AICc**, or **BIC**.
5. Performs residual diagnostics to ensure the residuals behave like white noise.

As a result, manual ACF and PACF analysis is less common in practice but remains an important tool for understanding ARIMA models and for manually specifying model orders.