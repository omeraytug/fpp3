Fundamentals steps of the process of producing forecast:
- preparing data
- data visualization
- specifying a model 
- model estimation
- accuracy & performance evaluation
- producing forecasts 


# Fitted Values and Residuals

## Fitted Values

A fitted value is the model's estimate of an observed value.

$$
\hat{y}_t
$$

It means what the model thinks the value should be.

For one-step forecasting:

$$
\hat{y}_{t|t-1}
$$

This means the forecast of y_t using information available before time t.

---

## Important Note

Fitted values are not always true forecasts.

For example, in the mean method, the average is calculated using all observations, including future observations.

So the fitted value may use information that would not be available in real forecasting.

But in the naive method:

$$
\hat{y}_t = y_{t-1}
$$

This is a true one-step forecast because it only uses the previous observation.

---

## Residuals

Residuals measure forecast errors.

$$
e_t = y_t - \hat{y}_t
$$

where:

- y_t = actual value
- yhat_t = fitted value
- e_t = residual

---

## How to Interpret Residuals

If residual is positive:

$$
e_t > 0
$$

The actual value is higher than the fitted value.

The model underestimated.

If residual is negative:

$$
e_t < 0
$$

The actual value is lower than the fitted value.

The model overestimated.

If residual is zero:

$$
e_t = 0
$$

The model predicted perfectly.

---

## Innovation Residuals

If we transform the data, we usually check residuals on the transformed scale.

Example:

$$
w_t = \log(y_t)
$$

Innovation residual:

$$
w_t - \hat{w}_t
$$

Regular residual:

$$
y_t - \hat{y}_t
$$

If there is no transformation, innovation residuals and regular residuals are the same.

---

## Why Residuals Are Important

Residuals help us check if the model captured the important patterns in the data.

A good model should leave residuals that look random.

Good residuals should have:

- no trend
- no seasonality
- no clear pattern
- mean close to zero
- no autocorrelation

If residuals still show patterns, the model can probably be improved.

---

## Simple Example

Suppose:

$$
y_t = 120
$$

and

$$
\hat{y}_t = 115
$$

Then:

$$
e_t = 120 - 115 = 5
$$

The residual is positive, so the model underestimated.

---

## Key Idea

Fitted values are the model's estimates of the observed data.

Residuals are the difference between actual values and fitted values.

A good forecasting model should leave only random noise in the residuals.


# Residual Diagnostics

## Residuals

A residual is the forecasting error:

$$
e_t = y_t - \hat{y}_t
$$

where:

* $y_t$ = actual value
* $\hat{y}_t$ = fitted value (one-step-ahead forecast)

Residuals measure how far the forecast was from the actual observation.

---

## Goal of Residual Diagnostics

After fitting a forecasting model, we check whether the residuals behave like **white noise**.

If residuals still contain patterns, then the model has not used all available information.

A good forecasting model leaves only random noise in the residuals.

---

## Essential Properties of Good Residuals

### 1. Residuals Should Be Uncorrelated

Residuals should not show autocorrelation.

If residuals are correlated, then information remains in the errors and the model can be improved.

We check this using:

* ACF plot
* Ljung-Box test

---

### 2. Residuals Should Have Mean Zero

$$
\bar e = 0
$$

If the average residual is not zero, forecasts are biased.

If:

$$
\bar e > 0
$$

the model tends to under-forecast.

If:

$$
\bar e < 0
$$

the model tends to over-forecast.

Bias can be corrected by adding the mean residual to future forecasts.

---

## Desirable Properties of Residuals

These are useful but not strictly necessary.

### 3. Constant Variance (Homoscedasticity)

Residual variability should remain approximately constant over time.

A residual plot should show a similar spread throughout the series.

Large increases or decreases in spread indicate heteroscedasticity.

---

### 4. Normal Distribution

Residuals should be approximately normally distributed.

A histogram should look roughly bell-shaped.

Normality is mainly important for:

* prediction intervals
* confidence intervals

A forecasting model can still produce good forecasts even if residuals are not perfectly normal.

---

## Residual Diagnostic Plots

### Residual Time Plot

Used to check:

* mean near zero
* constant variance
* absence of obvious patterns

Good residuals fluctuate randomly around zero.

---

### Histogram

Used to check:

* symmetry
* normality
* outliers

A roughly bell-shaped histogram is desirable.

---

### ACF Plot

Used to check for autocorrelation.

Interpretation:

* Spikes inside confidence bounds → good
* Large spikes outside bounds → residual autocorrelation remains

If significant autocorrelation exists, the model can usually be improved.

---

## White Noise Residuals

The ideal residual series behaves like white noise:

$$
e_t \sim WN(0,\sigma^2)
$$

Characteristics:

* Mean = 0
* Uncorrelated
* Constant variance

If residuals are white noise, the model has extracted all predictable information from the data.

---

## Google Stock Price Example

The book uses the Naive Forecast:

$$
\hat y_t = y_{t-1}
$$

Residuals become:

$$
e_t = y_t - y_{t-1}
$$

which are simply daily stock price changes.

Results:

* Mean residual ≈ 0
* No significant autocorrelation
* Variance approximately constant
* Slight departure from normality due to a large stock price jump

Conclusion:

The Naive model provides good forecasts, although prediction intervals may not be perfectly accurate.

---

## Ljung-Box Test

The Ljung-Box test formally checks whether residuals are autocorrelated.

### Hypotheses

**Null Hypothesis**

$$
H_0:\ \text{Residuals are white noise}
$$

**Alternative Hypothesis**

$$
H_1:\ \text{Residuals contain autocorrelation}
$$

---

### Interpretation

If:

$$
p > 0.05
$$

Fail to reject $H_0$.

Residuals behave like white noise.

This is desirable.

If:

$$
p < 0.05
$$

Reject $H_0$.

Residuals contain autocorrelation.

The model may be improved.

---

## Box-Pierce and Ljung-Box Tests

Both tests examine whether a group of autocorrelations is significantly different from zero.

The textbook recommends:

* $\ell = 10$ for non-seasonal data
* $\ell = 2m$ for seasonal data

where $m$ is the seasonal period.

The Ljung-Box test is generally preferred because it is more accurate.

---

## Practical Checklist

When evaluating a forecasting model:

* [ ] Residual mean is approximately zero
* [ ] Residuals show no autocorrelation
* [ ] ACF spikes remain within confidence limits
* [ ] Residual variance is approximately constant
* [ ] Residual histogram is roughly normal
* [ ] Ljung-Box p-value > 0.05

If these conditions hold, the residuals are approximately white noise and the model is likely capturing all available information.

---

## Key Idea

**A good forecasting model leaves residuals that look like white noise.**

Residuals should contain random errors only, not predictable patterns.


# Distributional Forecasts and Prediction Intervals

## Why Do We Need More Than Point Forecasts?

A point forecast gives only a single predicted value.

Example:

$$
\hat{y}_{T+h|T} = 759
$$

However, future values are uncertain.

Instead of predicting one exact value, we should describe the range of possible future values.

This range is represented by a **forecast distribution**.

---

# Forecast Distribution

A forecast distribution describes the probability of all possible future values.

- Point forecast = mean of the forecast distribution.
- Most forecasting methods assume a normal distribution.

Example:

```
           Forecast Distribution

                 ^
                 |
            ____/ \____
          _/           \_
        _/               \_
-------|--------759--------|-------
```

The center of the distribution is the point forecast.

---

# Prediction Intervals (PI)

A prediction interval gives a range in which future observations are expected to fall with a specified probability.

Example:

Forecast:

$$
\hat{y}=759
$$

95% Prediction Interval:

$$
[737,\ 781]
$$

Interpretation:

There is a 95% probability that the future value will fall inside this interval.

---

# Prediction Interval Formula

For normally distributed forecasts:

$$
\hat{y}_{T+h|T} \pm c\hat{\sigma}_h
$$

where:

- $\hat{y}_{T+h|T}$ = point forecast
- $\hat{\sigma}_h$ = forecast standard deviation
- $c$ = multiplier based on confidence level

---

# Common Multipliers

| Coverage | Multiplier |
|-----------|-----------|
| 80% | 1.28 |
| 90% | 1.64 |
| 95% | 1.96 |
| 99% | 2.58 |

### Important

For exams, remember:

$$
80\% \rightarrow 1.28
$$

$$
95\% \rightarrow 1.96
$$

---

# Why Prediction Intervals Matter

Point forecasts alone do not show uncertainty.

Example:

Model A:

$$
100 \; [98,102]
$$

Model B:

$$
100 \; [50,150]
$$

Both have the same forecast.

Model A is much more certain because its interval is narrower.

---

# One-Step Forecast Intervals

For one-step forecasts ($h=1$), uncertainty is estimated using residuals.

Residual standard deviation:

$$
\hat{\sigma}
=
\sqrt{
\frac{
\sum e_t^2
}{
T-K-M
}
}
$$

where:

- $e_t$ = residuals
- $T$ = number of observations
- $K$ = number of estimated parameters
- $M$ = missing residuals

### Interpretation

Large residuals
→ larger uncertainty

Small residuals
→ smaller uncertainty

---

# Multi-Step Forecast Intervals

A key property:

As forecast horizon increases,

$$
h \uparrow
$$

uncertainty increases,

$$
\sigma_h \uparrow
$$

and prediction intervals become wider.

Example:

| Horizon | Prediction Interval |
|----------|----------|
| 1-step | [95,105] |
| 5-step | [90,110] |
| 10-step | [80,120] |

The further into the future we forecast, the more uncertain we become.

---

# Forecast Standard Deviation for Benchmark Methods

## Mean Method

$$
\hat{\sigma}_h
=
\hat{\sigma}
\sqrt{1+\frac{1}{T}}
$$

---

## Naive Method

$$
\hat{\sigma}_h
=
\hat{\sigma}
\sqrt{h}
$$

### Important

For the Naive method:

- Forecast remains constant.
- Uncertainty grows with $\sqrt{h}$.

Example:

$$
\hat{\sigma}=10
$$

1-step:

$$
10\sqrt{1}=10
$$

4-step:

$$
10\sqrt{4}=20
$$

9-step:

$$
10\sqrt{9}=30
$$

---

## Seasonal Naive Method

$$
\hat{\sigma}_h
=
\hat{\sigma}
\sqrt{k+1}
$$

where

$$
k=\left\lfloor \frac{h-1}{m} \right\rfloor
$$

and $m$ is the seasonal period.

---

## Drift Method

$$
\hat{\sigma}_h
=
\hat{\sigma}
\sqrt{
h
\left(
1+\frac{h}{T-1}
\right)
}
$$

---

# Bootstrapped Prediction Intervals

Normal prediction intervals assume:

$$
e_t \sim N(0,\sigma^2)
$$

But residuals are not always normally distributed.

An alternative is:

## Bootstrapping

Instead of assuming a normal distribution:

1. Collect historical residuals.
2. Randomly sample residuals.
3. Generate possible future values.
4. Repeat thousands of times.

---

# Naive Forecast with Bootstrap

Naive model:

$$
y_t = y_{t-1}+e_t
$$

Future simulation:

$$
y^*_{T+1}
=
y_T + e^*_{T+1}
$$

where

$$
e^*_{T+1}
$$

is a randomly selected historical residual.

Then:

$$
y^*_{T+2}
=
y^*_{T+1}
+
e^*_{T+2}
$$

Repeat for the entire forecast horizon.

---

# Sample Paths

Bootstrapping creates many possible futures.

Path 1:

```
759 → 762 → 760 → 765
```

Path 2:

```
759 → 755 → 751 → 748
```

Path 3:

```
759 → 767 → 772 → 780
```

Each path is one possible realization of the future.

---

# Creating Bootstrap Prediction Intervals

Generate many future paths:

Example:

5000 simulations

For each horizon:

1. Collect all simulated values.
2. Sort them.
3. Take percentiles.

Example:

95% interval:

- Lower = 2.5th percentile
- Upper = 97.5th percentile

Result:

$$
95\% \text{ Prediction Interval}
$$

---

# Advantages of Bootstrapping

- No normality assumption.
- Uses actual historical residuals.
- Can capture skewness.
- Can capture fat tails.
- Often more realistic than normal intervals.

---

# Exam Summary

### Must Know

- Forecast distribution = uncertainty around forecasts.
- Point forecast = mean of forecast distribution.
- Prediction intervals provide a likely range for future values.
- 80% multiplier = 1.28.
- 95% multiplier = 1.96.
- Prediction intervals widen as horizon increases.
- For Naive:

$$
\hat{\sigma}_h
=
\hat{\sigma}\sqrt{h}
$$

- Bootstrapping samples historical residuals to simulate future values.
- Bootstrap intervals do not require normally distributed residuals.

### One-Line Summary

A point forecast gives the most likely future value, while prediction intervals and forecast distributions quantify uncertainty; this uncertainty increases with forecast horizon and can be estimated using either normal-distribution formulas or bootstrap simulations.