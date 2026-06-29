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


# FPP3 Chapter 8.2 - Methods with Trend

## Why do we need another method?

Simple Exponential Smoothing (SES):
- Assumes **no trend** and **no seasonality**.
- Forecasts are **flat** (constant).

If the data has a **trend**, SES performs poorly.

Solution:
- **Holt's Linear Trend Method**
- **Damped Trend Method**

---

# Holt's Linear Trend Method

## When to use

Use when:
- Data has a trend.
- No seasonality.
- Trend is expected to continue.

Example:
- Population
- Sales increasing every year
- Revenue growth

---

## Main idea

Instead of estimating only the level (like SES),

Holt estimates:

- Level
- Trend (slope)

So every new observation updates BOTH.

---

## Components

### 1. Level (ℓₜ)

Represents the current value of the series.

Example:

If sales are around 250 units today,

Level ≈ 250.

---

### 2. Trend (bₜ)

Represents how fast the series is increasing or decreasing.

Example:

Sales increase by 8 every month.

Trend = +8.

---

## Holt's Equations

### Forecast Equation

```
ŷₜ₊ₕ = ℓₜ + h bₜ
```

Meaning:

Forecast =
Current Level +
(Number of periods ahead × Current Trend)

Example:

Level = 100

Trend = 5

Forecast:

1 step ahead:

```
100 + 1×5 = 105
```

2 steps:

```
100 + 2×5 = 110
```

5 steps:

```
100 + 5×5 = 125
```

Forecasts form a straight line.

---

### Level Equation

```
ℓₜ = αyₜ + (1−α)(ℓₜ₋₁ + bₜ₋₁)
```

Interpretation:

New level =
Weighted average of

- Actual observation
- Previous forecast

Exactly like SES, except the previous forecast now includes the trend.

---

### Trend Equation

```
bₜ = β*(ℓₜ − ℓₜ₋₁) + (1−β*)bₜ₋₁
```

Interpretation:

New trend =
Weighted average of

- Newly observed change in level
- Previous trend estimate

---

# Parameters

## α (Alpha)

Controls the level.

Large α:
- Reacts quickly.
- More weight on recent observations.

Small α:
- Smoother.
- Reacts slowly.

---

## β* (Beta)

Controls the trend.

Large β:
- Trend changes quickly.
- Sensitive.

Small β:
- Trend changes slowly.
- Stable.

---

## Forecast Shape

Unlike SES,

Forecasts are NOT flat.

They continue following the trend.

Example:

```
Actual data:

100
105
110
115
120

Forecast:

125
130
135
140
145
```

Straight line.

---

# Problem with Holt's Method

Holt assumes:

The trend continues forever.

If sales increase by 5 every month,

20 months later it predicts

+100.

Sometimes unrealistic.

Long-term forecasts often become too large.

This is called:

**Over-forecasting.**

---

# Damped Trend Method

Solution:

Reduce the trend gradually.

Instead of continuing forever,

the trend slowly becomes weaker.

---

## New parameter

φ (phi)

```
0 < φ < 1
```

Usually

```
0.8 ≤ φ ≤ 0.98
```

---

## Meaning of φ

### φ = 1

No damping.

Exactly Holt's method.

Trend continues forever.

---

### φ close to 1

Very little damping.

Trend almost unchanged.

---

### Smaller φ

More damping.

Trend disappears faster.

Forecast becomes flatter.

---

## Forecast Equation

```
ŷₜ₊ₕ =
ℓₜ + (φ + φ² + ... + φʰ)bₜ
```

Instead of adding

```
h × trend
```

we add

```
φ + φ² + ...
```

Since

```
φ² < φ
φ³ < φ²
```

each future trend contribution becomes smaller.

---

## Intuition

Suppose

Trend = 10

Without damping:

```
10
20
30
40
50
```

With damping:

```
9
17
24
29
33
```

Growth slows down.

Eventually,

forecast becomes almost flat.

---

# Holt vs Damped Holt

## Holt

Trend stays constant forever.

Forecast:

```
/
/
/
/
/
```

Good for:
- Short forecasts
- Stable trends

Can overestimate long-term forecasts.

---

## Damped Holt

Trend gradually decreases.

Forecast:

```
/
 /
  /
   _
```

Good for:
- Long-term forecasting
- More realistic forecasts

Usually performs better.

---

# Example from the textbook

Australian Population

Population keeps increasing.

Holt:

Forecast keeps increasing forever.

Damped Holt:

Still increases,

but more slowly over time.

More realistic.

---

# Choosing the Best Method

Compare models using forecast accuracy metrics.

Common metrics:

- RMSE
- MAE
- MAPE
- MASE

The textbook compares:

- SES
- Holt
- Damped Holt

Result:

Damped Holt had the lowest errors.

Therefore,

it was selected as the best model.

---

# Summary Table

| Method | Trend | Seasonality | Forecast Shape |
|---------|-------|-------------|----------------|
| SES | ❌ | ❌ | Flat |
| Holt | ✅ | ❌ | Straight line |
| Damped Holt | ✅ | ❌ | Trend gradually flattens |

---

# Key Exam Points

Remember:

- SES only estimates **level**.
- Holt estimates **level + trend**.
- Damped Holt estimates **level + trend**, but the trend gradually weakens.

---

## Parameters

α
- Controls level updates.

β*
- Controls trend updates.

φ
- Controls how quickly the trend fades.

---

## Holt Forecast

```
Forecast = Level + h × Trend
```

---

## Damped Holt

Forecast still has a trend,

but the trend becomes smaller over time.

---

## When to use

SES
- No trend
- No seasonality

Holt
- Trend
- No seasonality

Damped Holt
- Trend
- No seasonality
- Better long-term forecasts


# FPP3 Chapter 8.3 - Holt-Winters' Seasonal Method

## Why do we need Holt-Winters?

Recall:

- SES handles **level only**.
- Holt handles **level + trend**.

But many time series also have **seasonality**.

Example:

- Ice cream sales
- Electricity demand
- Tourism
- Retail sales

These repeat every:

- Week
- Month
- Quarter
- Year

Solution:

**Holt-Winters Method**

It extends Holt's method by adding a **seasonal component**.

---

# When to use

Use Holt-Winters when data has:

- Trend ✅
- Seasonality ✅

Examples:

- Monthly sales
- Quarterly tourism
- Daily website visits
- Weekly customer demand

---

# Components

Holt-Winters estimates **three things**.

## 1. Level (ℓₜ)

Current average value.

Example:

Sales are currently around

```
250
```

---

## 2. Trend (bₜ)

How fast the data is increasing or decreasing.

Example:

Sales increase

```
+8 units/month
```

---

## 3. Seasonal Component (sₜ)

Repeating seasonal pattern.

Example:

Every December

Sales are always higher.

Every February

Sales are always lower.

The model learns these seasonal effects.

---

# Parameters

There are now **three smoothing parameters**.

---

## α (Alpha)

Controls updates to the **level**.

Large α

- Reacts quickly

Small α

- Reacts slowly

---

## β* (Beta)

Controls updates to the **trend**.

Large β

- Trend changes quickly

Small β

- Trend changes slowly

---

## γ (Gamma)

Controls updates to the **seasonality**.

Large γ

- Seasonal pattern changes quickly

Small γ

- Seasonal pattern stays almost constant

---

# Seasonal Period (m)

m = number of observations per season.

Examples:

Daily data with weekly seasonality

```
m = 7
```

Monthly data

```
m = 12
```

Quarterly data

```
m = 4
```

Hourly data with daily seasonality

```
m = 24
```

---

# Two Types of Seasonality

There are **two versions** of Holt-Winters.

---

# 1. Additive Seasonality

Use when seasonal changes stay roughly the same size.

Example:

Every December sales increase by

```
+500
```

Every year.

Even if average sales grow,

the seasonal increase stays around

```
+500
```

Seasonal effect is **constant**.

---

### Example

```
Average Sales

100
200
300
400

December effect

+20
+20
+20
+20
```

Always adds the same amount.

---

# 2. Multiplicative Seasonality

Use when seasonal changes increase as the series grows.

Instead of adding a fixed number,

seasonality is a percentage.

---

### Example

Average Sales

```
100
200
300
```

December effect

```
+20%
+20%
+20%
```

Actual increase becomes

```
20
40
60
```

Seasonal swings get larger as the level increases.

---

# Quick Comparison

## Additive

Seasonality = constant amount

```
+20
+20
+20
```

Good when seasonal variation stays similar.

---

## Multiplicative

Seasonality = percentage

```
+20%
+20%
+20%
```

Good when seasonal variation grows with the level.

---

# Forecast Equation

Conceptually,

Forecast =

```
Level
+ Trend
+ Seasonality
```

(Additive)

or

```
(Level + Trend)
× Seasonality
```

(Multiplicative)

You do NOT need to memorize every equation.

Remember the intuition.

---

# Additive Holt-Winters

Forecast

```
Forecast =
Level
+ Trend
+ Seasonal Effect
```

Example

Current level

```
100
```

Trend

```
+5
```

Seasonal effect

```
+20
```

Forecast

```
125
```

---

# Multiplicative Holt-Winters

Forecast

```
Forecast =
(Level + Trend)
× Seasonal Effect
```

Example

Level + Trend

```
100
```

Seasonal factor

```
1.20
```

Forecast

```
120
```

---

# Seasonal Component

The model updates the seasonal pattern every season.

Example:

Monthly data

Every January

the model compares

January this year

with

January last year.

It updates the seasonal index accordingly.

---

# Additive vs Multiplicative

| Additive | Multiplicative |
|-----------|----------------|
| Constant seasonal effect | Seasonal effect grows with level |
| Uses addition | Uses multiplication |
| Absolute changes | Percentage changes |

---

# Example from the textbook

Australian Tourism

Quarterly data

Strong seasonal pattern.

Highest demand

```
Q1
```

because it is Australian summer.

The textbook compares:

- Additive Holt-Winters
- Multiplicative Holt-Winters

Both produced almost identical RMSE.

Therefore,

both fit the data equally well.

---

# Seasonal Components

## Additive

Seasonal components approximately sum to

```
0
```

Example

```
+1.5
-0.3
-0.7
-0.5

Total ≈ 0
```

---

## Multiplicative

Seasonal components approximately sum to

```
m
```

where

```
m = seasonal length
```

Quarterly

```
m = 4
```

Example

```
1.2
1.0
0.9
0.9

Total ≈ 4
```

---

# Holt-Winters with Damped Trend

Just like Holt,

Holt-Winters can also use damping.

Instead of trend continuing forever,

the trend slowly becomes flatter.

Now the model has

- Level
- Trend
- Seasonality
- Damping

This is often one of the best forecasting models.

---

# Daily Data

Holt-Winters also works for daily data.

Example:

Weekly seasonality

```
m = 7
```

The model learns

Monday

Tuesday

Wednesday

...

Sunday

patterns automatically.

---

# Choosing Between Models

No trend

→ SES

Trend only

→ Holt

Trend + Seasonality

→ Holt-Winters

Trend + Seasonality + more realistic long-term forecasts

→ Damped Holt-Winters

---

# Summary Table

| Method | Level | Trend | Seasonality |
|---------|------|-------|-------------|
| SES | ✅ | ❌ | ❌ |
| Holt | ✅ | ✅ | ❌ |
| Holt-Winters | ✅ | ✅ | ✅ |
| Damped Holt-Winters | ✅ | ✅ (damped) | ✅ |

---

# Which Seasonal Method?

Choose **Additive** if:

- Seasonal changes stay constant.

Example:

```
100
120
110
130
```

Every year the seasonal swing is about the same.

---

Choose **Multiplicative** if:

- Seasonal changes increase as the data grows.

Example:

```
100 → ±20

200 → ±40

300 → ±60
```

Seasonality grows with the level.

---

# Key Exam Points

Remember:

- Holt-Winters = Holt + Seasonality.
- Estimates **Level, Trend, and Seasonality**.
- α updates Level.
- β updates Trend.
- γ updates Seasonality.
- Additive = constant seasonal effect.
- Multiplicative = percentage seasonal effect.
- Damped Holt-Winters gradually reduces the trend.
- Choose the model using forecast accuracy metrics such as RMSE, MAE, MAPE, or MASE.


# FPP3 Chapter 8.4 - A Taxonomy of Exponential Smoothing Methods

## What is a Taxonomy?

A **taxonomy** is simply a **classification system**.

Chapter 8.4 does **not** introduce new forecasting methods.

Instead, it organizes every exponential smoothing method into one framework.

Instead of memorizing many separate methods, we classify them based on:

- Trend component
- Seasonal component

---

# Classification

Each model is written as

```
(Trend, Seasonality)
```

Example

```
(A,M)
```

means

- Trend = Additive
- Seasonality = Multiplicative

The **first letter** always describes the trend.

The **second letter** always describes the seasonal component.

---

# Trend Components

There are only three possible trend types.

## N (None)

No trend.

Forecasts remain flat.

Example:

Simple Exponential Smoothing.

---

## A (Additive)

Trend increases or decreases by a constant amount.

Example:

```
100
105
110
115
120
```

The increase is always +5.

This is Holt's Linear Method.

---

## Ad (Additive Damped)

Trend gradually becomes weaker over time.

Example

Instead of

```
+5
+5
+5
+5
```

it becomes

```
+5
+4
+3
+2
...
```

Useful because real-world trends rarely continue forever.

---

# Seasonal Components

There are three possible seasonal types.

## N (None)

No seasonality.

---

## A (Additive)

Seasonality stays approximately constant.

Example

Sales every December are always about

```
+200
```

regardless of overall sales.

---

## M (Multiplicative)

Seasonality changes proportionally with the level.

Example

December sales are always

```
20% higher
```

As sales increase,

the seasonal swings also become larger.

---

# The Nine Exponential Smoothing Models

There are

```
3 Trend options
×

3 Seasonal options

=

9 models
```

| Trend | Seasonality | Shorthand |
|--------|-------------|-----------|
| None | None | (N,N) |
| None | Additive | (N,A) |
| None | Multiplicative | (N,M) |
| Additive | None | (A,N) |
| Additive | Additive | (A,A) |
| Additive | Multiplicative | (A,M) |
| Additive Damped | None | (Ad,N) |
| Additive Damped | Additive | (Ad,A) |
| Additive Damped | Multiplicative | (Ad,M) |

---

# Common Model Names

| Shorthand | Common Name |
|-----------|-------------|
| (N,N) | Simple Exponential Smoothing (SES) |
| (A,N) | Holt's Linear Method |
| (Ad,N) | Additive Damped Trend Method |
| (A,A) | Additive Holt-Winters |
| (A,M) | Multiplicative Holt-Winters |
| (Ad,A) | Holt-Winters Damped Method |

Notice that

```
(N,A)

(N,M)

(Ad,M)
```

are valid models,

but they do not have widely used common names.

---

# Why Doesn't FPP3 Use Multiplicative Trend?

Earlier researchers proposed models with

- Multiplicative Trend
- Multiplicative Damped Trend

However,

these often produce unrealistic forecasts,

so FPP3 does **not** recommend them.

Only these trend types are used:

- N
- A
- Ad

---

# Table 8.7

Table 8.7 is a summary of every exponential smoothing method.

It does **not** introduce new equations.

Instead,

it combines all equations from

- SES
- Holt
- Damped Holt
- Holt-Winters

into one table.

---

# Which Components Does Each Model Have?

| Model | Level | Trend | Seasonal | Damping |
|--------|:-----:|:-----:|:--------:|:-------:|
| (N,N) | ✅ | ❌ | ❌ | ❌ |
| (N,A) | ✅ | ❌ | ✅ | ❌ |
| (N,M) | ✅ | ❌ | ✅ | ❌ |
| (A,N) | ✅ | ✅ | ❌ | ❌ |
| (A,A) | ✅ | ✅ | ✅ | ❌ |
| (A,M) | ✅ | ✅ | ✅ | ❌ |
| (Ad,N) | ✅ | ✅ | ❌ | ✅ |
| (Ad,A) | ✅ | ✅ | ✅ | ✅ |
| (Ad,M) | ✅ | ✅ | ✅ | ✅ |

---

# Smoothing Parameters

Different models use different smoothing parameters.

| Parameter | Meaning |
|-----------|----------|
| α | Level smoothing |
| β* | Trend smoothing |
| γ | Seasonal smoothing |
| φ | Damping parameter |

---

# Formula Summary (Table 8.7)

## Symbols

- ℓₜ = Level
- bₜ = Trend
- sₜ = Seasonal component
- α = Level smoothing
- β* = Trend smoothing
- γ = Seasonal smoothing
- φ = Damping parameter
- h = Forecast horizon
- m = Seasonal length
- φₕ = φ + φ² + ... + φʰ

---

## (N,N) — No Trend, No Seasonality (SES)

### Forecast

```
ŷₜ₊ₕ = ℓₜ
```

### Level

```
ℓₜ = αyₜ + (1−α)ℓₜ₋₁
```

---

## (N,A) — No Trend, Additive Seasonality

### Forecast

```
ŷₜ₊ₕ = ℓₜ + sₜ₊ₕ₋ₘ(k+1)
```

### Level

```
ℓₜ = α(yₜ − sₜ₋ₘ) + (1−α)ℓₜ₋₁
```

### Seasonal

```
sₜ = γ(yₜ − ℓₜ₋₁) + (1−γ)sₜ₋ₘ
```

---

## (N,M) — No Trend, Multiplicative Seasonality

### Forecast

```
ŷₜ₊ₕ = ℓₜ sₜ₊ₕ₋ₘ(k+1)
```

### Level

```
ℓₜ = α(yₜ / sₜ₋ₘ) + (1−α)ℓₜ₋₁
```

### Seasonal

```
sₜ = γ(yₜ / ℓₜ₋₁) + (1−γ)sₜ₋ₘ
```

---

## (A,N) — Holt's Linear Method

### Forecast

```
ŷₜ₊ₕ = ℓₜ + hbₜ
```

### Level

```
ℓₜ = αyₜ + (1−α)(ℓₜ₋₁ + bₜ₋₁)
```

### Trend

```
bₜ = β*(ℓₜ − ℓₜ₋₁) + (1−β*)bₜ₋₁
```

---

## (A,A) — Additive Holt-Winters

### Forecast

```
ŷₜ₊ₕ = ℓₜ + hbₜ + sₜ₊ₕ₋ₘ(k+1)
```

### Level

```
ℓₜ = α(yₜ − sₜ₋ₘ) + (1−α)(ℓₜ₋₁ + bₜ₋₁)
```

### Trend

```
bₜ = β*(ℓₜ − ℓₜ₋₁) + (1−β*)bₜ₋₁
```

### Seasonal

```
sₜ = γ(yₜ − ℓₜ₋₁ − bₜ₋₁) + (1−γ)sₜ₋ₘ
```

---

## (A,M) — Multiplicative Holt-Winters

### Forecast

```
ŷₜ₊ₕ = (ℓₜ + hbₜ)sₜ₊ₕ₋ₘ(k+1)
```

### Level

```
ℓₜ = α(yₜ / sₜ₋ₘ) + (1−α)(ℓₜ₋₁ + bₜ₋₁)
```

### Trend

```
bₜ = β*(ℓₜ − ℓₜ₋₁) + (1−β*)bₜ₋₁
```

### Seasonal

```
sₜ = γ(yₜ / (ℓₜ₋₁ + bₜ₋₁)) + (1−γ)sₜ₋ₘ
```

---

## (Ad,N) — Additive Damped Trend

### Forecast

```
ŷₜ₊ₕ = ℓₜ + φₕbₜ
```

### Level

```
ℓₜ = αyₜ + (1−α)(ℓₜ₋₁ + φbₜ₋₁)
```

### Trend

```
bₜ = β*(ℓₜ − ℓₜ₋₁) + (1−β*)φbₜ₋₁
```

---

## (Ad,A) — Damped Holt-Winters (Additive)

### Forecast

```
ŷₜ₊ₕ = ℓₜ + φₕbₜ + sₜ₊ₕ₋ₘ(k+1)
```

### Level

```
ℓₜ = α(yₜ − sₜ₋ₘ) + (1−α)(ℓₜ₋₁ + φbₜ₋₁)
```

### Trend

```
bₜ = β*(ℓₜ − ℓₜ₋₁) + (1−β*)φbₜ₋₁
```

### Seasonal

```
sₜ = γ(yₜ − ℓₜ₋₁ − φbₜ₋₁) + (1−γ)sₜ₋ₘ
```

---

## (Ad,M) — Damped Holt-Winters (Multiplicative)

### Forecast

```
ŷₜ₊ₕ = (ℓₜ + φₕbₜ)sₜ₊ₕ₋ₘ(k+1)
```

### Level

```
ℓₜ = α(yₜ / sₜ₋ₘ) + (1−α)(ℓₜ₋₁ + φbₜ₋₁)
```

### Trend

```
bₜ = β*(ℓₜ − ℓₜ₋₁) + (1−β*)φbₜ₋₁
```

### Seasonal

```
sₜ = γ(yₜ / (ℓₜ₋₁ + φbₜ₋₁)) + (1−γ)sₜ₋ₘ
```

---

# Master Cheat Sheet

| Model | Trend | Seasonality | Forecast |
|------|-----------|------------|-----------|
| (N,N) | None | None | ℓₜ |
| (N,A) | None | Additive | ℓₜ + s |
| (N,M) | None | Multiplicative | ℓₜ × s |
| (A,N) | Additive | None | ℓₜ + hbₜ |
| (A,A) | Additive | Additive | ℓₜ + hbₜ + s |
| (A,M) | Additive | Multiplicative | (ℓₜ + hbₜ)s |
| (Ad,N) | Damped | None | ℓₜ + φₕbₜ |
| (Ad,A) | Damped | Additive | ℓₜ + φₕbₜ + s |
| (Ad,M) | Damped | Multiplicative | (ℓₜ + φₕbₜ)s |

---

# Key Exam Points

- A taxonomy is a **classification system**.
- Models are written as **(Trend, Seasonality)**.
- Trend options:
  - N = None
  - A = Additive
  - Ad = Additive Damped
- Seasonal options:
  - N = None
  - A = Additive
  - M = Multiplicative
- There are **3 × 3 = 9** exponential smoothing models.
- Table 8.7 is a **summary of the formulas from previous chapters**, not a new forecasting method.
- Choose a model based on whether the data has **trend**, **seasonality**, and whether the **seasonality is additive or multiplicative**.


# FPP3 Chapter 8.5 - Innovations State Space Models for Exponential Smoothing

## Main Idea

Up to Chapter 8.4, exponential smoothing methods were introduced as **forecasting algorithms**.

These algorithms:

- Produce **point forecasts**
- Update the level, trend and seasonality using smoothing equations

However, they do **not** describe how the data are statistically generated.

Chapter 8.5 introduces **innovations state space models**, which provide a statistical framework for ETS models.

---

# Why Do We Need State Space Models?

The exponential smoothing methods from previous chapters:

- Produce point forecasts
- Do not describe uncertainty

State space models:

- Produce the **same point forecasts**
- Also provide **prediction intervals**
- Describe the data as a **stochastic (random) process**
- Allow statistical estimation and model comparison

---

# Algorithm vs Statistical Model

## Exponential Smoothing Algorithm

Focuses on:

```
Observed Data
↓

Update Components

↓

Forecast
```

Produces only a point forecast.

---

## Statistical Model

Focuses on:

```
Hidden States

↓

Observed Data

↓

Forecast Distribution
```

Models both the forecast and the uncertainty.

---

# What is a State?

A **state** is an **unobserved (hidden) component** of the time series.

Examples:

- Level
- Trend
- Seasonality

These cannot be observed directly.

Instead, they are estimated from the observed data.

---

Example

Observed values:

```
120
125
130
```

Hidden states might be:

```
Level = 124

Trend = +5

Seasonality = +3
```

Only the observations are known.

The states must be estimated.

---

# State Space Model

A state space model consists of **two equations**:

1. Measurement (Observation) Equation
2. State (Transition) Equation

---

# Measurement Equation

The measurement equation describes

> **How the observed data are generated from the hidden states.**

General idea:

```
Observation

=

State

+

Random Error
```

or

```
Observation

=

State × Error
```

depending on the error model.

---

Example

```
Observed Sales

=

Current Level

+

Error
```

---

# State Equation

The state equation describes

> **How the hidden states evolve over time.**

General idea:

```
Previous State

↓

Updated State
```

For example,

the level today depends on

- yesterday's level
- today's forecasting error

---

# Innovations

An **innovation** is simply the **new information** contained in the latest observation.

Mathematically,

Innovation = Forecast Error

```
Innovation

=

Actual

−

Forecast
```

This is the same one-step-ahead residual used earlier,

but it is now treated as a random variable.

---

# Error Correction Form

Recall SES:

```
ℓₜ = αyₜ + (1−α)ℓₜ₋₁
```

This can be rearranged as

```
ℓₜ = ℓₜ₋₁ + α(yₜ − ℓₜ₋₁)
```

Since

```
eₜ = yₜ − ℓₜ₋₁
```

we obtain

```
ℓₜ = ℓₜ₋₁ + αeₜ
```

This is called the **error correction form**.

Interpretation:

```
New Level

=

Old Level

+

Correction
```

where

```
Correction = α × Forecast Error
```

---

# Interpretation of α

The meaning of α is exactly the same as before.

Large α

- Large corrections
- Fast adaptation
- Rough estimates

Small α

- Small corrections
- Smooth estimates
- Slow adaptation

Special cases:

```
α = 0

Level never changes.
```

```
α = 1

Level follows every observation.
```

The model becomes a random walk.

---

# Additive Error Models

Assume

```
Actual

=

Forecast

+

Error
```

The forecasting error is

```
eₜ = yₜ − ŷₜ|ₜ₋₁
```

Errors are assumed to follow

```
eₜ ~ NID(0, σ²)
```

Meaning:

- Normally distributed
- Independent
- Mean = 0
- Variance = σ²

---

## ETS(A,N,N)

This represents

- Additive Error
- No Trend
- No Seasonality

Measurement equation

```
yₜ = ℓₜ₋₁ + εₜ
```

State equation

```
ℓₜ = ℓₜ₋₁ + αεₜ
```

Interpretation:

Observation

=

Previous Level

+

Random Error

Level is then updated using the forecast error.

---

# Multiplicative Error Models

Instead of absolute errors,

errors are measured proportionally.

General idea

```
Actual

=

Forecast × (1 + Error)
```

Used when variability increases as the series level increases.

---

## ETS(M,N,N)

Represents

- Multiplicative Error
- No Trend
- No Seasonality

Measurement equation

```
yₜ = ℓₜ₋₁(1 + εₜ)
```

State equation

```
ℓₜ = ℓₜ₋₁(1 + αεₜ)
```

---

# Additive vs Multiplicative Errors

## Additive Errors

```
Actual

=

Forecast

+

Error
```

Error is an absolute difference.

Example

Forecast = 100

Actual = 110

Error = +10

---

## Multiplicative Errors

```
Actual

=

Forecast × (1 + Error)
```

Error is a percentage.

Example

Forecast = 100

Actual = 110

Relative Error = 10%

---

# ETS Notation

Previous chapters used

```
(Trend, Seasonality)
```

Example

```
(A,M)
```

Now ETS models add the **Error** component.

Notation becomes

```
ETS(Error, Trend, Seasonality)
```

---

Examples

```
ETS(A,N,N)

Additive Error

No Trend

No Seasonality
```

---

```
ETS(M,A,N)

Multiplicative Error

Additive Trend

No Seasonality
```

---

```
ETS(A,A,M)

Additive Error

Additive Trend

Multiplicative Seasonality
```

---

# Why Do Additive and Multiplicative Error Models Produce the Same Point Forecast?

If the smoothing parameters are identical,

both models produce

the same point forecasts.

However,

they model uncertainty differently.

Therefore,

their

- Prediction intervals
- Forecast distributions

are different.

---

# Holt's Method in State Space Form

For

```
ETS(A,A,N)
```

Measurement equation

```
yₜ = ℓₜ₋₁ + bₜ₋₁ + εₜ
```

State equations

```
ℓₜ = ℓₜ₋₁ + bₜ₋₁ + αεₜ
```

```
bₜ = bₜ₋₁ + βεₜ
```

Interpretation

Observation depends on

- Previous Level
- Previous Trend
- Random Error

Both level and trend are updated using the innovation.

---

# General Pattern of Every ETS Model

Every ETS model follows exactly the same structure.

## Measurement Equation

Describes

```
State

↓

Observation
```

---

## State Equations

Describe

```
Old State

↓

New State
```

---

## Innovation

Measures

```
Actual

−

Forecast
```

and updates every state.

---

# Table 8.8

Table 8.8 lists the state space equations for every ETS model.

Although the equations differ,

they all follow the same pattern.

For every model:

1. Measurement equation
2. State equation(s)
3. Innovation (forecast error)
4. Hidden states updated using smoothing parameters

The only differences are

- Additive vs Multiplicative errors
- Presence of trend
- Presence of seasonality
- Damped vs non-damped trend

---

# Summary Table

| Concept | Meaning |
|----------|---------|
| State | Hidden component (level, trend, seasonality) |
| Measurement Equation | Describes how observations are generated from the states |
| State Equation | Describes how the hidden states evolve over time |
| Innovation | New information = Forecast Error |
| Error Correction | Update state using the innovation |
| Additive Error | Observation = Forecast + Error |
| Multiplicative Error | Observation = Forecast × (1 + Error) |
| ETS(Error, Trend, Seasonality) | Complete notation for ETS models |

---

# Key Exam / Interview Points

Remember:

- Previous chapters described ETS as a forecasting algorithm.
- Chapter 8.5 describes ETS as a **statistical state space model**.
- Hidden states are **Level, Trend and Seasonality**.
- Every state space model has:
  - Measurement equation
  - State equation
- Innovations are simply **one-step-ahead forecast errors**.
- Error correction updates the hidden states using the innovation.
- Additive and multiplicative error models often produce the **same point forecasts**, but **different prediction intervals**.
- ETS notation changes from **(Trend, Seasonality)** to **ETS(Error, Trend, Seasonality)**.