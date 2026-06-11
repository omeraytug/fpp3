# Chapter 3: Transformations, Decomposition and Seasonal Adjustment

---

# 3.1 Transformations

Sometimes the variability of a time series changes as the level changes.

Example:

* Small fluctuations when values are low.
* Large fluctuations when values are high.

In such cases, a transformation can stabilize the variance.

Let:

* $y_t$ = original observations
* $w_t$ = transformed observations

## Common Transformations

| Transformation | Formula             |
| -------------- | ------------------- |
| Square Root    | $w_t=\sqrt{y_t}$    |
| Cube Root      | $w_t=\sqrt[3]{y_t}$ |
| Logarithm      | $w_t=\log(y_t)$     |

### Strength of Transformations

$$
\sqrt{y_t}
\rightarrow
\sqrt[3]{y_t}
\rightarrow
\log(y_t)
$$

The logarithm generally provides the strongest variance stabilization.

## Why Logarithms?

Logarithms are particularly useful because they are easy to interpret.

Changes in logarithms correspond approximately to percentage changes.

$$
\log(y_t)-\log(y_{t-1})
$$

is approximately the percentage growth rate from $y_{t-1}$ to $y_t$.

---

# Box-Cox Transformations

The previous transformations belong to the Box-Cox family.

$$
w_t=
\begin{cases}
\log(y_t), & \lambda=0 \
\dfrac{\operatorname{sign}(y_t)|y_t|^\lambda-1}{\lambda},
& \lambda\neq0
\end{cases}
$$

(FPP uses the Bickel-Doksum version, which allows negative values.)

## Interpretation of λ

| λ   | Interpretation         |
| --- | ---------------------- |
| 1   | No transformation      |
| 0.5 | Square root            |
| 0   | Logarithm              |
| -1  | Inverse transformation |

## Rule of Thumb

Ask:

> Do fluctuations increase as the level increases?

* No → Use the original data.
* Yes → Consider a log or Box-Cox transformation.

---

# 3.2 Time Series Components

A time series can be viewed as a combination of:

$$
y_t=f(T_t,S_t,R_t)
$$

where:

* $T_t$ = Trend-cycle component
* $S_t$ = Seasonal component
* $R_t$ = Remainder (noise)

## Goal of Decomposition

Separate a series into:

1. Trend
2. Seasonality
3. Remainder

This helps us understand the structure of the data before forecasting.

---

# Additive Decomposition

$$
y_t=T_t+S_t+R_t
$$

Use when seasonal fluctuations remain approximately constant over time.

Example:

```text
100 ± 20
200 ± 20
500 ± 20
```

The seasonal amplitude stays constant.

---

# Multiplicative Decomposition

$$
y_t=T_t\times S_t\times R_t
$$

Use when seasonal fluctuations grow with the level of the series.

Example:

```text
100 ± 20%
200 ± 20%
500 ± 20%
```

The seasonal amplitude increases as the series grows.

## Choosing Between Additive and Multiplicative

### Additive

Use when:

* Seasonal effects are approximately constant.
* Seasonal amplitude does not change with the level.

### Multiplicative

Use when:

* Seasonal effects are proportional to the level.
* Seasonal amplitude increases with the level.

### Quick Rule

* Constant seasonal amplitude → Additive
* Increasing seasonal amplitude → Multiplicative

---

## Relationship Between Logs and Multiplicative Models

Multiplicative model:

$$
y_t=T_t\times S_t\times R_t
$$

Taking logarithms:

$$
\log(y_t)
=========

\log(T_t)
+
\log(S_t)
+
\log(R_t)
$$

Therefore:

> Logarithms convert multiplicative relationships into additive relationships.

This is why multiplicative series are often log-transformed before decomposition.

---

# 3.3 Seasonal Adjustment

Seasonal adjustment removes the seasonal component from a series.

## Additive Case

Original:

$$
y_t=T_t+S_t+R_t
$$

Seasonally adjusted:

$$
y_t-S_t=T_t+R_t
$$

## Multiplicative Case

Original:

$$
y_t=T_t\times S_t\times R_t
$$

Seasonally adjusted:

$$
\frac{y_t}{S_t}
===============

T_t\times R_t
$$

## Important Point

A seasonally adjusted series is **not** the trend.

It still contains:

* Trend
* Random noise

Therefore:

$$
\text{Seasonally Adjusted Series}
=================================

T_t+R_t
$$

(additive case)

## Why Perform Seasonal Adjustment?

To compare periods fairly.

Example:

Retail sales are usually higher in December.

Removing seasonality helps determine whether sales are truly increasing or decreasing.

---

# 3.4 Moving Averages

Moving averages provide a simple estimate of the trend-cycle component.

## m-Moving Average

For odd $m$:

$$
\hat T_t
========

\frac1m
\sum_{j=-k}^{k}
y_{t+j}
$$

where

$$
k=\frac{m-1}{2}
$$

## Example: 7-MA

$$
\hat T_t
========

\frac1{7}
(
y_{t-3}
+y_{t-2}
+y_{t-1}
+y_t
+y_{t+1}
+y_{t+2}
+y_{t+3}
)
$$

## Why Use Moving Averages?

Nearby observations are often similar.

Averaging them:

* Removes noise
* Smooths fluctuations
* Reveals the underlying trend

## Effect of m

### Small m

* Less smoothing
* More noise remains

### Large m

* More smoothing
* Trend becomes smoother
* More detail is lost

---

# Endpoint Problem

Moving averages cannot be computed near the beginning and end of a series.

Example:

For a 3-MA:

$$
\hat T_t
========

\frac{y_{t-1}+y_t+y_{t+1}}3
$$

The first observation lacks $y_{t-1}$.

The last observation lacks $y_{t+1}$.

Therefore trend estimates are unavailable at the endpoints.

---

# Centered Moving Averages

Odd moving averages naturally have a center.

Example:

$$
\frac{y_{t-1}+y_t+y_{t+1}}3
$$

is centered at $t$.

Even moving averages do not.

To center them, compute a second moving average of length 2.

This creates a **Centered Moving Average (CMA)**.

## Centered 4-MA

$$
\hat T_t
========

\frac18 y_{t-2}
+
\frac14 y_{t-1}
+
\frac14 y_t
+
\frac14 y_{t+1}
+
\frac18 y_{t+2}
$$

## Removing Seasonality with Moving Averages

A moving average whose length equals the seasonal period removes seasonality.

| Data Frequency | Seasonal Period | Moving Average |
| -------------- | --------------- | -------------- |
| Quarterly      | 4               | 2×4 MA         |
| Monthly        | 12              | 2×12 MA        |

The resulting series approximates the trend-cycle component.

---

# 3.5 Classical Decomposition

The goal is to decompose a time series into:

$$
y_t=T_t+S_t+R_t
$$

or

$$
y_t=T_t\times S_t\times R_t
$$

## Step 1: Estimate Trend

Estimate $\hat T_t$ using moving averages.

* Odd seasonal period → m-MA
* Even seasonal period → centered m-MA

Examples:

* Quarterly → 2×4 MA
* Monthly → 2×12 MA

## Step 2: De-trend

### Additive

$$
y_t-\hat T_t
$$

leaves approximately:

$$
\hat S_t+\hat R_t
$$

### Multiplicative

$$
\frac{y_t}{\hat T_t}
$$

leaves approximately:

$$
\hat S_t\times\hat R_t
$$

## Step 3: Estimate Seasonal Indices

Estimate the seasonal effect for each season by averaging de-trended values.

Example:

Monthly data:

* Average all January values
* Average all February values
* ...
* Average all December values

This produces 12 seasonal indices.

## Seasonal Constraints

### Additive

$$
S^{(1)}
+
S^{(2)}
+
\cdots
+
S^{(m)}
=======

0
$$

### Multiplicative

$$
S^{(1)}
+
S^{(2)}
+
\cdots
+
S^{(m)}
=======

m
$$

## Step 4: Construct Seasonal Component

Repeat the seasonal indices through time.

## Step 5: Estimate Remainder

### Additive

$$
\hat{R}_t = y_t - \hat{T}_t - \hat{S}_t
$$

### Multiplicative

$$
\hat R_t
========

\frac{y_t}
{\hat T_t\hat S_t}
$$

## Ratio-to-Moving-Average Method

For multiplicative decomposition:

1. Estimate trend using moving averages.
2. Divide the data by the trend estimate.
3. Estimate seasonal indices.

This is called the **Ratio-to-Moving-Average Method**.

---

# 3.6 STL Decomposition

STL stands for:

**Seasonal-Trend decomposition using LOESS**

Unlike classical decomposition, STL uses LOESS smoothing rather than moving averages.

## STL Components

$$
y_t=T_t+S_t+R_t
$$

where:

* $T_t$ = trend
* $S_t$ = seasonality
* $R_t$ = remainder

## Advantages of STL

* Robust to outliers
* Handles changing seasonality
* Works with any seasonal period
* Produces better trend estimates
* Widely used in modern forecasting

## Classical vs STL

| Classical            | STL                       |
| -------------------- | ------------------------- |
| Uses moving averages | Uses LOESS                |
| Fixed seasonality    | Flexible seasonality      |
| Loses endpoints      | Better endpoint estimates |
| Older method         | Preferred modern method   |

---

# Key Takeaways

1. Transformations stabilize variance.
2. Logarithms convert multiplicative relationships into additive ones.
3. A time series consists of trend, seasonality, and remainder.
4. Additive decomposition is used when seasonal amplitude is constant.
5. Multiplicative decomposition is used when seasonal amplitude grows with the level.
6. Seasonal adjustment removes seasonality but not noise.
7. Moving averages estimate the trend-cycle component.
8. Classical decomposition uses moving averages.
9. STL uses LOESS and is generally preferred in modern forecasting.
10. Decomposition is primarily used to understand the structure of a time series before forecasting.
