# FPP3 Chapter 8.1 - Simple Exponential Smoothing (SES)

## When to Use SES

Use Simple Exponential Smoothing when the series has:

- No trend
- No seasonality
- Only a changing level

Examples:

- Stable sales
- Stable demand
- Stable exports

---

## Main Idea

SES forecasts are weighted averages of past observations.

Recent observations receive larger weights.

Older observations receive exponentially smaller weights.

---

## SES Forecast Formula

$$
\hat y_{T+1|T}
=
\alpha y_T
+
\alpha(1-\alpha)y_{T-1}
+
\alpha(1-\alpha)^2y_{T-2}
+
\cdots
$$

where

$$
0 \le \alpha \le 1
$$

and

- \(\alpha\) = smoothing parameter

---

## Effect of α

### Large α

- More weight on recent observations
- Responds quickly to changes
- Less smoothing

### Small α

- More weight on older observations
- Responds slowly to changes
- More smoothing

---

## Recursive Form

The practical SES formula is:

$$
\hat y_{t+1|t}
=
\alpha y_t
+
(1-\alpha)\hat y_{t|t-1}
$$

Interpretation:

New Forecast

=

α × Latest Observation

+

(1 − α) × Previous Forecast

---

## Component Form

### Forecast Equation

$$
\hat y_{t+h|t}
=
\ell_t
$$

### Level Equation

$$
\ell_t
=
\alpha y_t
+
(1-\alpha)\ell_{t-1}
$$

where

- \(\ell_t\) = estimated level at time \(t\)

---

## Flat Forecast Property

SES produces flat forecasts:

$$
\hat y_{T+h|T}
=
\ell_T
$$

for all

$$
h=1,2,3,\ldots
$$

Therefore:

- No trend forecast
- No seasonal forecast
- Future forecasts are constant

---

## Relationship to Other Methods

### Average Method

- Equal weights on all observations

### Naive Method

- 100% weight on last observation

### SES

- Larger weights on recent observations
- Smaller weights on older observations

---

## Key Takeaway

SES estimates only a level component.

It is the foundation of more advanced ETS methods:

- SES → Level only
- Holt → Level + Trend
- Holt-Winters → Level + Trend + Seasonality