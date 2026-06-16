# Chapter 2 - Time Series Graphics and Data Structures

---

# Big Picture

Before forecasting anything:

```text
Plot the data.
```

This is the first rule of time series analysis.

Graphs help identify:

- Trend
- Seasonality
- Cycles
- Outliers
- Structural changes
- Relationships between variables

A forecasting model should capture the patterns visible in the plots.

---

# 2.1 DataFrames and Time Series Data

A time series contains:

```text
Observation
+
Time information
```

Examples:

| Time | Sales |
|--------|--------|
| Jan | 100 |
| Feb | 120 |
| Mar | 150 |

---

# DataFrame

Most time series are stored in pandas DataFrames.

Example:

| Year | Observation |
|--------|--------|
| 2015 | 123 |
| 2016 | 39 |
| 2017 | 78 |

---

# Important Time Columns

---

## Timestamp

Represents:

```text
A specific instant in time
```

Example:

```python
Timestamp("2020-01-01")
```

---

## Period

Represents:

```text
A span of time
```

Example:

```python
Period("2020-01")
```

means:

```text
Entire month of January 2020
```

---

# Key Variables

Sometimes one DataFrame contains many time series.

Example:

| Year | Length | Sex | Time |
|--------|--------|--------|--------|
| 1896 | 100 | Men | 12.0 |
| 1900 | 100 | Men | 11.0 |

---

The combination:

```text
Length + Sex
```

uniquely identifies each series.

These are called:

```text
Key Variables
```

---

# Common Pandas Operations

---

## Filter Rows

```python
.loc[]
```

---

## Remove Columns

```python
.drop()
```

---

## Create Columns

```python
.assign()
```

---

## Group Data

```python
.groupby()
```

---

## Aggregate Data

```python
.agg()
```

---

# Seasonal Period

Very important.

The seasonal period is:

```text
Number of observations
before the pattern repeats.
```

---

## Common Seasonal Periods

| Data Frequency | Seasonal Period |
|---------------|---------------|
| Quarterly | 4 |
| Monthly | 12 |
| Weekly | 52 |
| Daily | 7 |
| Hourly | 24 |
| Half-hourly | 48 |

---

# Multiple Seasonalities

Some data have more than one seasonality.

Example:

Daily data may have:

```text
Weekly seasonality = 7

Yearly seasonality = 365
```

---

# 2.2 Time Plots

Most important graph in time series.

---

# Definition

A time plot displays:

```text
Observation
vs
Time
```

---

# Purpose

Used to identify:

- Trend
- Seasonality
- Cycles
- Outliers
- Structural changes

---

# Example Questions

When looking at a time plot ask:

```text
Is there a trend?

Is there seasonality?

Are there unusual observations?

Does variability change?

Did something change suddenly?
```

---

# Example Findings

Time plots often reveal:

- Strikes
- Recessions
- Covid effects
- Holidays
- Data errors

---

# Key Rule

Always create a time plot first.

---

# 2.3 Time Series Patterns

One of the most important sections.

---

# Trend

Definition:

```text
Long-term increase
or decrease.
```

---

Examples:

```text
Population growth

GDP growth

Housing prices
```

---

Important:

```text
Trend does NOT have
to be linear.
```

---

# Seasonal Pattern

Definition:

```text
Pattern repeats
at a fixed known frequency.
```

---

Examples:

```text
Monthly sales

Weekly demand

Daily electricity usage
```

---

Characteristics:

```text
Known period

Repeats regularly
```

---

Examples:

```text
Monthly data
→ period = 12

Quarterly data
→ period = 4
```

---

# Cyclic Pattern

Definition:

```text
Long-term rises and falls
without fixed frequency.
```

---

Examples:

```text
Business cycles

Economic expansions

Recessions
```

---

# Seasonal vs Cyclic

This is commonly tested.

---

## Seasonal

```text
Fixed frequency

Known period

Predictable timing
```

Example:

```text
Christmas sales
```

---

## Cyclic

```text
Variable frequency

No fixed length

Economic driven
```

Example:

```text
Business cycle
```

---

# Random Variation

Not every movement has a pattern.

Some movements are:

```text
Pure randomness
```

---

Example:

```text
Daily stock returns
```

often look close to random.

---

# Summary

| Pattern | Fixed Frequency? |
|----------|----------|
| Trend | No |
| Seasonality | Yes |
| Cycles | No |
| Random Noise | No |

---

# 2.4 Seasonal Plots

A seasonal plot reorganizes data by season.

---

# Purpose

Makes seasonal patterns easier to see.

---

Instead of:

```text
Time on x-axis
```

we use:

```text
Month
Quarter
Day
Hour
```

---

# Benefits

Helps identify:

```text
Strong seasonality

Changing seasonality

Abnormal seasons
```

---

# Interpretation

Look for:

```text
Repeated shapes
```

across years.

---

# Multiple Seasonalities

Some data contain:

```text
Daily pattern

Weekly pattern

Yearly pattern
```

simultaneously.

---

Examples:

```text
Electricity demand

Traffic

Website visits
```

---

# 2.5 Seasonal Subseries Plots

Alternative way to view seasonality.

---

# Idea

Create a separate mini-plot for each season.

Example:

```text
Jan
Feb
Mar
...
Dec
```

---

# Benefits

Makes it easier to see:

```text
How each month changes
through time.
```

---

# Useful For

Finding:

```text
Changing seasonal behavior
```

---

# 2.6 Scatterplots

Used when comparing two variables.

---

# Example

Electricity demand

vs

Temperature

---

# Purpose

Reveal relationships.

---

# Correlation

Measures strength of linear relationship.

Notation:

$$
r
$$

Range:

$$
-1 \le r \le 1
$$

---

# Interpretation

### r = 1

Perfect positive relationship

---

### r = -1

Perfect negative relationship

---

### r = 0

No linear relationship

---

# Important Warning

Correlation only measures:

```text
Linear relationships
```

---

A strong nonlinear relationship can still produce:

```text
Low correlation.
```

---

# Anscombe's Lesson

Different datasets can have:

```text
Same correlation
```

but

```text
Completely different patterns.
```

Always inspect plots.

---

# Scatterplot Matrix

Used when many variables exist.

Shows:

```text
Every variable
against every other variable.
```

---

Purpose:

```text
Quickly identify
relationships.
```

---

# 2.7 Lag Plots

One of the most important forecasting tools.

---

# Definition

Plot:

$$
y_t
$$

against:

$$
y_{t-k}
$$

---

where:

```text
k = lag
```

---

# Purpose

Detect dependence over time.

---

# Interpretation

### Random Cloud

```text
Little dependence
```

---

### Clear Pattern

```text
Strong dependence
```

---

# Seasonal Data

Seasonality often appears as:

```text
Strong relationships
at seasonal lags.
```

Example:

Quarterly data:

```text
Lag 4
Lag 8
```

often show strong relationships.

---

# Why Important?

Lag plots visually explain what ACF measures numerically.

---

# 2.8 Autocorrelation (ACF)

One of the most important concepts in forecasting.

---

# Definition

Autocorrelation measures:

```text
Relationship between
a series and its past values.
```

---

Example:

```text
Today
vs
Yesterday
```

---

# ACF

Autocorrelation Function.

Contains:

$$
r_1,r_2,r_3,...
$$

---

where:

```text
r1 = lag 1 correlation

r2 = lag 2 correlation

etc.
```

---

# ACF Plot

Shows:

```text
Correlation
vs
Lag
```

---

# ACF and Trend

Trend causes:

```text
Large positive correlations

Slow decay
```

---

Typical pattern:

```text
1.0
0.9
0.8
0.7
...
```

---

# ACF and Seasonality

Seasonality causes:

```text
Large spikes
at seasonal lags.
```

---

Example:

Monthly data:

```text
12
24
36
...
```

---

Quarterly data:

```text
4
8
12
...
```

---

# Interpreting ACF

---

## Strong Positive ACF

```text
Observations are similar
to previous values.
```

---

## Negative ACF

```text
Alternating behavior.
```

---

## Near Zero

```text
Little dependence.
```

---

# Important Exam Clues

---

Trend:

```text
ACF slowly decreases
```

---

Seasonality:

```text
Repeating spikes
```

---

Trend + Seasonality:

```text
Slow decay
+
Seasonal spikes
```

---

# 2.9 White Noise

Extremely important concept.

---

# Definition

White noise:

```text
Pure randomness
```

---

Properties:

### Mean = 0

---

### Constant Variance

---

### No Autocorrelation

---

# White Noise Plot

Looks random.

No visible pattern.

---

# White Noise ACF

Most spikes:

```text
Close to zero
```

---

# Confidence Bounds

For white noise:

$$
\pm \frac{1.96}{\sqrt{T}}
$$

where:

- T = series length

---

# Interpretation

If most spikes stay inside bounds:

```text
Series behaves like white noise.
```

---

If many spikes exceed bounds:

```text
Series is probably not white noise.
```

---

# Why Is White Noise Important?

Because:

```text
Nothing predictable remains.
```

---

A good forecasting model often leaves:

```text
Residuals
≈
White Noise
```

This becomes extremely important in Chapter 5.

---

# Key Exam Takeaways

1. Always plot data first.
2. Trend = long-term movement.
3. Seasonality = fixed repeating pattern.
4. Cycles = variable long-term fluctuations.
5. Seasonal period = observations before repetition.
6. Seasonal plots reveal seasonality clearly.
7. Lag plots show dependence visually.
8. ACF measures dependence numerically.
9. Trend → slowly decaying ACF.
10. Seasonality → spikes at seasonal lags.
11. White noise has no autocorrelation.
12. Good forecasting models leave white-noise residuals.

---

# Quick Memory Sheet

```text
Time Plot
→ First graph to create

Trend
→ Long-term direction

Seasonality
→ Fixed repeating pattern

Cycle
→ Variable long-term fluctuation

Seasonal Plot
→ Visualize seasonality

Scatterplot
→ Relationship between variables

Correlation
→ Linear relationship

Lag Plot
→ y_t vs y_(t-k)

ACF
→ Correlation with past values

Trend in ACF
→ Slow decay

Seasonality in ACF
→ Seasonal spikes

White Noise
→ No trend
→ No seasonality
→ No autocorrelation
```

# Chapter 3 - Time Series Decomposition

---

# Big Picture

Many time series contain several patterns at once:

- Trend
- Seasonality
- Cycles
- Random noise

Instead of analyzing everything together, we can split the series into components.

```text
Original Series
        ↓
Decomposition
        ↓
Trend
Seasonality
Remainder
```

This makes the series easier to understand and forecast.

---

# 3.1 Transformations and Adjustments

Before modeling a time series, it is often useful to simplify it.

Goal:

```text
Simpler data
=
Easier modeling
=
Better forecasts
```

---

# Calendar Adjustments

Some variation is caused purely by calendar effects.

Example:

```text
February
=
28 days

March
=
31 days
```

Sales may differ simply because one month has more days.

Solution:

```text
Sales per day
instead of
Total monthly sales
```

This removes calendar effects.

---

# Population Adjustments

Some series grow simply because population grows.

Example:

```text
Hospital beds
```

Instead of:

```text
Total beds
```

use:

```text
Beds per 1000 people
```

This gives a more meaningful measure.

---

# GDP Per Capita

Instead of:

```text
GDP
```

Use:

```text
GDP / Population
```

This removes population effects.

Interpretation becomes much easier.

---

# Inflation Adjustments

Money changes value over time.

Example:

```text
$100 in 1990
≠
$100 today
```

Because of inflation.

---

## CPI Adjustment

CPI = Consumer Price Index

Used to convert values into:

```text
Constant dollars
```

instead of:

```text
Nominal dollars
```

---

## Why Adjust For Inflation?

Without adjustment:

```text
Sales may appear to increase
```

even if the business is actually shrinking.

After adjustment:

```text
Real growth becomes visible.
```

---

# Mathematical Transformations

Used when variance changes over time.

Example:

```text
Small fluctuations early
Huge fluctuations later
```

This is difficult to model.

---

# Log Transformation

Most common transformation.

Formula:

$$
w_t=\log(y_t)
$$

Benefits:

- Stabilizes variance
- Reduces skewness
- Converts growth into percentages

---

# Important Interpretation

Log scale:

```text
Equal distances
≈ Equal percentage changes
```

This is why economists love logs.

---

# Box-Cox Transformation

General family of transformations.

Parameter:

$$
\lambda
$$

controls the transformation.

---

## Important Values

### λ = 1

```text
Almost no transformation
```

---

### λ = 0

```text
Log transformation
```

---

### 0 < λ < 1

```text
Moderate variance reduction
```

---

# Why Use Box-Cox?

Goal:

```text
Make variance
approximately constant.
```

This makes forecasting easier.

---

# Remember

You do NOT need to memorize the formula.

Just remember:

```text
λ = 0 → log

λ = 1 → almost original data
```

and

```text
Box-Cox helps stabilize variance.
```

---

# 3.2 Time Series Components

A time series can be decomposed into:

```text
Trend
Seasonality
Remainder
```

---

# Additive Decomposition

Formula:

$$
y_t=S_t+T_t+R_t
$$

where:

- S = Seasonal
- T = Trend
- R = Remainder

---

## Interpretation

Each component contributes independently.

Example:

```text
Sales
=
Trend
+
Seasonality
+
Noise
```

---

# Multiplicative Decomposition

Formula:

$$
y_t=S_t \times T_t \times R_t
$$

---

## Interpretation

Components interact proportionally.

Example:

```text
Higher trend
=
Larger seasonal swings
```

---

# When To Use Additive?

Use additive when:

```text
Seasonal variation
remains roughly constant.
```

Example:

```text
Always ±100 units
```

around the trend.

---

# When To Use Multiplicative?

Use multiplicative when:

```text
Seasonality grows
as the series grows.
```

Example:

```text
10% seasonal effect
```

instead of:

```text
100 unit seasonal effect
```

---

# Important Connection

Multiplicative decomposition:

$$
y_t=S_tT_tR_t
$$

Taking logs:

$$
\log(y_t)
=
\log(S_t)
+
\log(T_t)
+
\log(R_t)
$$

So:

```text
Log transform
+
Additive decomposition

≈

Multiplicative decomposition
```

Very important concept.

---

# STL Example Components

STL decomposition produces:

---

## Trend Component

Captures:

```text
Long-term movement
```

Questions:

```text
Growing?
Declining?
Flat?
```

---

## Seasonal Component

Captures:

```text
Repeating patterns
```

Examples:

- Monthly seasonality
- Quarterly seasonality
- Weekly seasonality

---

## Remainder Component

Captures:

```text
Everything unexplained
```

Essentially:

```text
Random noise
```

plus unusual events.

---

# Seasonally Adjusted Data

Very important concept.

---

## Additive Case

Remove seasonality:

$$
y_t-S_t
$$

---

## Multiplicative Case

Remove seasonality:

$$
y_t/S_t
$$

---

# Why Use Seasonally Adjusted Data?

Suppose unemployment rises every summer.

That seasonal increase may not be economically important.

Seasonal adjustment helps reveal:

```text
Underlying movement
```

instead of:

```text
Regular seasonal fluctuations.
```

---

# Important Exam Note

Seasonally adjusted data still contains:

```text
Trend
+
Remainder
```

It is NOT perfectly smooth.

---

# Better For Turning Points?

Use:

```text
Trend component
```

not:

```text
Seasonally adjusted data
```

because noise remains.

---

# 3.3 Moving Averages

One of the most important concepts.

---

# Purpose

Moving averages estimate trend.

Idea:

```text
Average nearby observations
```

to remove random noise.

---

# Moving Average

Formula:

$$
\hat T_t
=
\frac1m
\sum y_t
$$

Conceptually:

```text
Trend
=
Average of nearby values
```

---

# Example

3-MA:

```text
(Previous + Current + Next)/3
```

5-MA:

```text
Average of 5 observations
```

---

# Effect of Larger Window

Small MA:

```text
More flexible
Less smooth
```

Large MA:

```text
More smooth
Less flexible
```

---

# Important Rule

```text
Larger window
=
Smoother trend
```

---

# Centered Moving Average

Used when seasonality exists.

Example:

```text
2x4-MA
```

means:

```text
4-MA
then
2-MA
```

Purpose:

```text
Create symmetry
```

and remove seasonality more effectively.

---

# Choosing Moving Average Order

If seasonality period:

```text
m = 12
```

(monthly data)

use:

```text
2x12-MA
```

---

If seasonality period:

```text
m = 7
```

(daily weekly seasonality)

use:

```text
7-MA
```

---

# Weighted Moving Average

Not all observations receive equal weight.

Example:

```text
Recent observations
receive larger weights.
```

Advantages:

```text
Smoother trend estimates
```

than simple moving averages.

---

# 3.4 Classical Decomposition

Historical decomposition method.

Built using moving averages.

---

# Additive Classical Decomposition

Workflow:

### Step 1

Estimate trend.

---

### Step 2

Remove trend.

```text
Detrend data
```

---

### Step 3

Estimate seasonality.

---

### Step 4

Calculate remainder.

---

Formula:

$$
R_t
=
y_t
-
T_t
-
S_t
$$

---

# Multiplicative Classical Decomposition

Same process but uses division.

Formula:

$$
R_t
=
\frac{y_t}{T_tS_t}
$$

---

# Weaknesses of Classical Decomposition

Very important exam section.

---

## Problem 1

No trend estimates near endpoints.

---

## Problem 2

Over-smooths rapid changes.

---

## Problem 3

Seasonality assumed constant.

Real-world seasonality often changes.

---

## Problem 4

Sensitive to outliers.

---

# Conclusion

Classical decomposition is important historically,

but modern methods are better.

---

# 3.5 X-11 and SEATS

Used by government statistical agencies.

Examples:

- Census Bureau
- Statistics Canada
- ABS

---

# X-11

Improved classical decomposition.

Advantages:

- Handles outliers
- Handles trading day effects
- Handles changing seasonality
- Trend available at endpoints

---

# SEATS

Based on ARIMA models.

Widely used by official agencies.

Details are beyond this course.

---

# Exam Takeaway

Know only:

```text
X-11 and SEATS
=
Professional seasonal adjustment methods.
```

---

# 3.6 STL Decomposition

Most important decomposition method in FPP3.

STL stands for:

```text
Seasonal
Trend
Loess
```

---

# Why STL Is Popular

Advantages:

### Works with any seasonality

Not limited to:

- Monthly
- Quarterly

---

### Seasonality Can Change

Classical decomposition:

```text
Fixed seasonality
```

STL:

```text
Changing seasonality
```

---

### Trend Flexibility

Can control trend smoothness.

---

### Robust To Outliers

Unusual observations do not strongly distort trend and seasonality.

---

# STL Components

Produces:

```text
Trend
Seasonal
Remainder
```

same as classical decomposition.

---

# STL Parameters

Two important parameters:

---

## Seasonal Window

Controls:

```text
How quickly seasonality changes
```

Small value:

```text
Flexible seasonality
```

Large value:

```text
Stable seasonality
```

---

## Trend Window

Controls:

```text
How quickly trend changes
```

Small value:

```text
Flexible trend
```

Large value:

```text
Smooth trend
```

---

# Robust STL

Option:

```text
robust=True
```

Benefits:

```text
Outliers have less influence.
```

Usually preferred.

---

# STL vs Classical Decomposition

| STL | Classical |
|-------|-------|
| Flexible seasonality | Fixed seasonality |
| Handles outliers | Sensitive to outliers |
| Any seasonality | Limited |
| Better endpoints | Poor endpoints |
| Preferred today | Mostly historical |

---

# Key Exam Takeaways

1. Transformations simplify forecasting.
2. Log transformation stabilizes variance.
3. Box-Cox generalizes log transformations.
4. Additive decomposition:
   - y = Trend + Seasonal + Remainder
5. Multiplicative decomposition:
   - y = Trend × Seasonal × Remainder
6. Seasonally adjusted data removes seasonality.
7. Moving averages estimate trend.
8. Larger MA windows create smoother trends.
9. Classical decomposition is important historically.
10. STL is the preferred modern decomposition method.
11. STL allows changing seasonality.
12. STL can be robust to outliers.

---

# Quick Memory Sheet

```text
Calendar Adjustment
→ Remove calendar effects

Population Adjustment
→ Per capita data

Inflation Adjustment
→ Constant dollars

Log Transformation
→ Stabilize variance

Box-Cox
→ General transformation

Additive
→ T + S + R

Multiplicative
→ T × S × R

Seasonally Adjusted
→ Remove seasonality

Moving Average
→ Estimate trend

Large MA
→ Smoother trend

Classical Decomposition
→ Historical method

STL
→ Modern decomposition

STL Advantages
→ Flexible
→ Robust
→ Changing seasonality
```

# Chapter 4 - Time Series Features

---

# Big Picture

A feature is any numerical summary of a time series.

Examples:

- Mean
- Variance
- Autocorrelation
- Trend strength
- Seasonal strength

Instead of looking at hundreds of time series manually, we can compare them using features.

```text
Time Series
     ↓
Extract Features
     ↓
Compare / Cluster / Analyze
```

The tsfeatures package calculates many useful time series features automatically.

---

# Why Features Matter

Suppose you have:

```text
10 series
```

You can inspect them manually.

But what if you have:

```text
10,000 series
```

Impossible.

Instead:

```text
Convert each series
into a collection of numbers
(features)
```

Then compare them mathematically.

---

# 4.1 Simple Statistical Features

The simplest features are ordinary summary statistics.

Examples:

- Mean
- Median
- Minimum
- Maximum
- Quartiles

---

## Mean

Measures average level.

$$
\bar y
=
\frac1n
\sum y_t
$$

Interpretation:

```text
Typical value of the series
```

---

## Median

Middle observation.

Useful when outliers exist.

---

## Quartiles

Data divided into four equal parts.

| Statistic | Meaning |
|------------|------------|
| p25 | First quartile |
| Median | Middle |
| p75 | Third quartile |

Useful for understanding spread.

---

## Five Number Summary

Common descriptive summary:

```text
Minimum
Q1
Median
Q3
Maximum
```

Provides a quick description of the distribution.

---

# 4.2 ACF Features

Autocorrelation itself can be treated as a feature.

Recall:

```text
ACF measures relationship
between current observations
and past observations.
```

---

## First Autocorrelation

Feature:

```text
x_acf1
```

Measures relationship between:

$$
y_t
$$

and

$$
y_{t-1}
$$

Interpretation:

### Large positive value

```text
Strong persistence
```

### Near zero

```text
Little dependence
```

### Negative value

```text
Alternating behavior
```

---

## Sum of First 10 ACF Squares

Feature:

```text
x_acf10
```

Measures overall autocorrelation.

Large value:

```text
Lots of dependence
```

Small value:

```text
Series behaves more randomly
```

---

# Differenced Series Features

Sometimes we calculate ACF after differencing.

---

## First Difference

$$
y_t-y_{t-1}
$$

Measures change between consecutive observations.

Feature names:

```text
d1_acf1
d1_acf10
```

Purpose:

```text
Detect structure
remaining after differencing
```

---

## Second Difference

Difference of the differences.

Used less frequently.

Features:

```text
d2_acf1
d2_acf10
```

---

## Seasonal Difference

Example:

Monthly data

$$
y_t-y_{t-12}
$$

Quarterly data

$$
y_t-y_{t-4}
$$

Purpose:

```text
Measure year-to-year changes
instead of month-to-month changes.
```

---

# Why Are ACF Features Useful?

They help answer:

```text
How predictable is the series?
```

Strong autocorrelation:

```text
More predictable
```

Weak autocorrelation:

```text
More random
```

---

# 4.3 STL Features

One of the most important sections.

These features come from STL decomposition.

---

## STL Decomposition

Recall:

$$
y_t=T_t+S_t+R_t
$$

where:

- T = Trend
- S = Seasonal
- R = Remainder

---

# Trend Strength

Measures how important the trend is.

Feature:

```text
trend
```

Range:

```text
0 → 1
```

Interpretation:

### Trend ≈ 0

```text
Little trend
```

### Trend ≈ 1

```text
Very strong trend
```

---

## Formula (Conceptual)

Trend strength compares:

```text
Remaining noise
```

against

```text
Trend + noise
```

If trend explains a lot:

```text
Trend strength becomes large.
```

Do NOT memorize the formula.

Remember only:

```text
Closer to 1
=
Stronger trend
```

---

# Seasonal Strength

Measures how important seasonality is.

Feature:

```text
seasonal_strength
```

Range:

```text
0 → 1
```

Interpretation:

### Near 0

```text
No seasonality
```

### Near 1

```text
Strong seasonality
```

---

# Exam Interpretation

| Value | Meaning |
|---------|---------|
| 0.10 | Weak |
| 0.50 | Moderate |
| 0.90 | Strong |

---

# Trend vs Seasonal Strength

Often plotted together.

```text
High trend
Low seasonality
```

or

```text
Low trend
High seasonality
```

This helps classify series quickly.

---

# Peak Feature

Feature:

```text
peak
```

Represents:

```text
Which season contains
the highest seasonal effect
```

Example:

Quarterly data

```text
Peak = Q1
```

means seasonality is strongest in Quarter 1.

---

# Trough Feature

Feature:

```text
trough
```

Represents:

```text
Which season contains
the lowest seasonal effect
```

---

# Spike Feature

Measures unusual spikes in the remainder.

Feature:

```text
spike
```

Large value:

```text
Many unusual observations
```

Small value:

```text
Smooth behavior
```

---

# Linearity

Measures how linear the trend is.

Feature:

```text
linearity
```

Large value:

```text
Trend resembles a straight line
```

---

# Curvature

Measures how curved the trend is.

Feature:

```text
curvature
```

Large value:

```text
Trend bends significantly
```

Small value:

```text
Trend is approximately linear
```

---

# Residual ACF Features

Computed on STL remainder.

Features:

```text
e_acf1
e_acf10
```

Purpose:

```text
Measure remaining structure
after removing trend
and seasonality.
```

Small values are preferred.

---

# 4.4 Other Important Features

---

# Hurst Coefficient

Feature:

```text
hurst
```

Measures:

```text
Long memory
```

Long memory means:

```text
Observations remain correlated
for many lags.
```

Large Hurst:

```text
Strong persistence
```

---

# Spectral Entropy

Feature:

```text
entropy
```

Measures predictability.

Range:

```text
0 → 1
```

---

## Entropy Near 0

```text
Highly structured
Easy to forecast
```

Usually:

- strong trend
- strong seasonality

---

## Entropy Near 1

```text
Very noisy
Difficult to forecast
```

Think:

```text
Low entropy = easy forecasting

High entropy = hard forecasting
```

---

# Box-Pierce Feature

Based on:

```text
Box-Pierce test
```

Purpose:

```text
Check whether series
resembles white noise
```

---

# Ljung-Box Feature

Based on:

```text
Ljung-Box test
```

Usually preferred over Box-Pierce.

Tests:

```text
Is there autocorrelation?
```

---

# PACF Features

PACF = Partial Autocorrelation Function

Measures:

```text
Direct relationship
between observations
after removing intermediate effects.
```

Think:

```text
ACF = total relationship

PACF = direct relationship
```

Important later for ARIMA.

---

# Crossing Points

Feature:

```text
n_crossing_points
```

Counts:

```text
How many times the series
crosses its median.
```

Many crossings:

```text
Oscillating behavior
```

Few crossings:

```text
Persistent behavior
```

---

# Guerrero Feature

Feature:

```text
guerrero
```

Returns:

```text
Optimal Box-Cox λ
```

Used for selecting transformations.

Important later in forecasting.

---

# 4.5 Exploring Many Time Series

Main idea:

```text
Features turn
time series analysis
into a standard data analysis problem.
```

---

# Pair Plots

Plot features against each other.

Example:

```text
Trend Strength
vs
Seasonal Strength
```

Helps identify groups of series.

---

# Principal Component Analysis (PCA)

Problem:

```text
Many features
```

Solution:

```text
Compress them
into a few dimensions.
```

PCA creates:

```text
PC1
PC2
...
```

which summarize most variation.

---

# Interpretation of PCA

Points close together:

```text
Series behave similarly.
```

Points far apart:

```text
Series behave differently.
```

---

# Anomaly Detection

Features can identify unusual series.

Workflow:

```text
Time Series
→ Features
→ PCA
→ Outlier Detection
```

Outliers often indicate:

- unusual trend
- unusual seasonality
- unusual events
- data quality issues

---

# Key Exam Takeaways

1. A feature is any numerical summary of a time series.
2. Mean, median, min and max are simple features.
3. ACF features measure dependence over time.
4. STL decomposition produces trend and seasonal features.
5. Trend strength ranges from 0 to 1.
6. Seasonal strength ranges from 0 to 1.
7. Entropy measures forecasting difficulty.
8. Hurst measures long memory.
9. PACF measures direct relationships after removing intermediate effects.
10. PCA is used to visualize many features simultaneously.
11. Features allow thousands of time series to be compared efficiently.

---

# Quick Memory Sheet

```text
Trend Strength
→ How strong is trend?

Seasonal Strength
→ How strong is seasonality?

Entropy
→ How hard is forecasting?

Hurst
→ Long memory?

ACF
→ Overall dependence?

PACF
→ Direct dependence?

Peak
→ Strongest season?

Trough
→ Weakest season?

Spike
→ Outliers?

Crossing Points
→ Oscillation?

PCA
→ Reduce dimensions

Features
→ Convert time series into numbers
```


# Chapter 5 - The Forecaster's Toolbox

---

# 5.1 A Tidy Forecasting Workflow

Every forecasting project follows roughly the same process:

```text
1. Prepare data
2. Visualize data
3. Specify model
4. Train (fit) model
5. Check residuals
6. Produce forecasts
7. Evaluate accuracy
```

## Data Preparation

Tasks may include:

- Loading data
- Handling missing values
- Filtering observations
- Creating new variables
- Ensuring correct time ordering

Good forecasts start with clean data.

---

## Visualisation

Before fitting any model:

- Look for trend
- Look for seasonality
- Look for outliers
- Look for changing variance

Visualization helps choose an appropriate model.

---

## Model Specification

Examples:

- Mean
- Naive
- Seasonal Naive
- Drift
- Linear Regression
- ETS
- ARIMA

Choosing the correct model is one of the most important forecasting decisions.

---

## Model Estimation (Training)

The model learns patterns from historical data.

Example:

```python
sf.fit(train_df)
```

Training estimates unknown parameters from the data.

---

## Forecasting

Forecasts can be:

### Point Forecasts

Single best prediction.

Example:

```text
Forecast = 100
```

### Distributional Forecasts

Entire probability distribution of future values.

Example:

```text
Most likely value = 100

Possible range:
80 - 120
```

---

## Evaluation

Questions:

- Is the model biased?
- Did it capture all information?
- Is it more accurate than benchmark methods?

---

# 5.2 Simple Forecasting Methods

These are benchmark methods.

Any sophisticated forecasting model should outperform them.

---

## Mean Method

Future values equal historical average.

Formula:

$$
\hat y_{T+h|T} = \bar y
$$

Interpretation:

```text
Future = average of past values
```

Best for:

- Stable series
- No trend
- No seasonality

---

## Naive Method

Future values equal last observation.

Formula:

$$
\hat y_{T+h|T}=y_T
$$

Interpretation:

```text
Tomorrow = today
```

Often surprisingly difficult to beat.

Works especially well for:

- Stock prices
- Financial data
- Random walks

---

## Seasonal Naive Method

Forecast equals the most recent observation from the same season.

Example:

```text
Forecast next January
=
Last January
```

Quarterly example:

```text
Future Q1 = Previous Q1
Future Q2 = Previous Q2
```

Best for:

- Strong seasonality

---

## Drift Method

Naive forecast plus trend.

Formula:

$$
\hat y_{T+h|T}
=
y_T
+
h\left(
\frac{y_T-y_1}{T-1}
\right)
$$

Interpretation:

```text
Continue moving at the historical average rate
```

Equivalent to:

```text
Draw a line from first observation
to last observation
and extend it.
```

---

# 5.3 Fitted Values and Residuals

---

## Fitted Values

A fitted value is the model's estimate for a historical observation.

Notation:

$$
\hat y_t
$$

Interpretation:

```text
What would the model have predicted
for observation t?
```

Fitted values are usually one-step-ahead predictions.

---

## Residuals

Residuals measure forecasting mistakes.

Formula:

$$
e_t=y_t-\hat y_t
$$

where:

- Actual = $y_t$
- Predicted = $\hat y_t$

Example:

```text
Actual = 100
Predicted = 95

Residual = 5
```

Positive residual:

```text
Model underpredicted
```

Negative residual:

```text
Model overpredicted
```

---

## Innovation Residuals

When no transformation is used:

```text
Innovation Residuals
=
Residuals
```

If a transformation is used (e.g. log):

```text
Innovation residuals
are calculated on the transformed scale.
```

Innovation residuals are used for diagnostic checking.

---

# 5.4 Residual Diagnostics

Goal:

```text
Residuals should look like random noise.
```

If patterns remain:

```text
Model missed information.
```

---

## Property 1: Zero Mean

Good residuals satisfy:

$$
E(e_t)=0
$$

Interpretation:

```text
No systematic overforecasting
No systematic underforecasting
```

Otherwise:

```text
Forecasts are biased
```

---

## Property 2: No Autocorrelation

Residuals should not be predictable.

Good:

```text
Random scatter
```

Bad:

```text
Positive residuals followed by
positive residuals
```

Autocorrelation implies:

```text
Information remains in residuals.
```

The model can probably be improved.

---

## Property 3: Constant Variance

Also called:

```text
Homoscedasticity
```

Residual spread should remain approximately constant.

Bad example:

```text
Small residuals early
Huge residuals later
```

---

## Property 4: Normality

Not required.

Useful because:

```text
Prediction intervals become easier.
```

A model can still be good even if residuals are not normal.

---

# Residual Diagnostic Plots

---

## Time Plot

Questions:

- Is mean approximately zero?
- Is variance constant?
- Any obvious patterns?

---

## Histogram

Questions:

- Is distribution roughly symmetric?
- Are there outliers?
- Is distribution approximately normal?

---

## ACF Plot

Questions:

- Are residuals correlated?

Good result:

```text
All spikes inside confidence bands.
```

Bad result:

```text
Several spikes outside bands.
```

Meaning:

```text
Model missed structure.
```

---

# Portmanteau Tests

Used to test autocorrelation formally.

---

## Box-Pierce Test

Statistic:

$$
Q=T\sum_{k=1}^{\ell}r_k^2
$$

Large values suggest autocorrelation.

---

## Ljung-Box Test

Improved version of Box-Pierce.

Statistic:

$$
Q^*
=
T(T+2)
\sum_{k=1}^{\ell}
\frac{r_k^2}{T-k}
$$

Used much more often.

---

## Hypotheses

### Null

```text
Residuals are white noise.
```

### Alternative

```text
Residuals contain autocorrelation.
```

---

## Interpretation

### p-value > 0.05

```text
Fail to reject H0

Residuals behave like white noise.
```

Good.

### p-value < 0.05

```text
Reject H0

Residuals contain structure.
```

Bad.

---

# White Noise

White noise has:

- Mean = 0
- Constant variance
- No autocorrelation

A good forecasting model should leave residuals that resemble white noise.

---

# 5.5 Distributional Forecasts and Prediction Intervals

---

## Forecast Distribution

A forecast is not a single number.

Future observations are uncertain.

Instead we have:

```text
Probability distribution
of possible future values.
```

---

## Point Forecast

Usually:

$$
E(Y)
$$

The mean of the forecast distribution.

---

## Prediction Interval

Range where future observations are expected to fall.

General form:

$$
\hat y \pm c\sigma_h
$$

where:

- $\hat y$ = point forecast
- $\sigma_h$ = forecast standard deviation
- $c$ = multiplier

---

## Common Multipliers

| Level | Multiplier |
|---------|---------|
| 80% | 1.28 |
| 95% | 1.96 |

---

## Interpretation

95% interval:

```text
95% of future observations
should fall inside the interval.
```

---

## Multi-Step Forecasts

Key idea:

```text
Longer forecast horizon
=
More uncertainty
```

Therefore:

```text
Prediction intervals widen
as h increases.
```

---

# Forecast Standard Deviation

For benchmark methods:

### Naive

$$
\sigma_h=\sigma\sqrt h
$$

Uncertainty grows with horizon.

---

### Seasonal Naive

Depends on seasonal cycle.

---

### Drift

Uncertainty grows faster than Naive.

---

# Bootstrap Prediction Intervals

Used when residuals are not normal.

Idea:

1. Collect residuals
2. Randomly sample residuals
3. Generate many future paths
4. Calculate percentiles

Benefits:

- No normality assumption
- More flexible intervals

---

# Conformal Prediction

Modern distribution-free method.

Main idea:

```text
Use past forecast errors
to estimate future uncertainty.
```

Advantages:

- Model agnostic
- Distribution free
- Reliable coverage

Important assumption:

```text
Past forecast errors are representative
of future forecast errors.
```

---

# 5.6 Forecasting with Transformations

Common transformation:

$$
w_t=\log(y_t)
$$

Reasons:

- Stabilize variance
- Reduce skewness
- Keep forecasts positive

---

## Forecasting Process

```text
Transform
→ Model
→ Forecast
→ Back-transform
```

---

## Log Transformation

Back-transform:

$$
y_t=\exp(w_t)
$$

---

# Bias Adjustment

Important concept:

Back-transformed forecasts are usually:

```text
Median forecasts
```

not

```text
Mean forecasts
```

Because of asymmetry.

Bias adjustment corrects this difference.

Useful when forecasts must be aggregated.

---

# 5.7 Forecasting with Decomposition

Suppose:

$$
y_t = Trend + Seasonal + Residual
$$

---

## Procedure

### Step 1

Decompose series.

### Step 2

Forecast trend component.

### Step 3

Forecast seasonal component.

Usually:

```text
Seasonal Naive
```

### Step 4

Combine forecasts.

For additive decomposition:

$$
Forecast
=
Trend Forecast
+
Seasonal Forecast
$$

---

## Why Use Decomposition?

Makes complicated patterns easier to model.

---

# 5.8 Evaluating Point Forecast Accuracy

---

## Training Set

Used to estimate model parameters.

---

## Test Set

Used to evaluate forecasts.

Never use test data when fitting the model.

---

## Why Not Use Residuals?

Residuals are often optimistic.

We care about:

```text
Performance on unseen data.
```

---

# Forecast Errors

Forecast error:

$$
e_{T+h}
=
y_{T+h}
-
\hat y_{T+h|T}
$$

Calculated on:

```text
Test data
```

---

# Residuals vs Forecast Errors

| Residuals | Forecast Errors |
|------------|------------|
| Training data | Test data |
| One-step forecasts | Can be multi-step |
| Diagnostics | Evaluation |

---

# Accuracy Measures

---

## MAE

Mean Absolute Error

$$
MAE=mean(|e|)
$$

Interpretation:

```text
Average forecasting mistake.
```

Easy to understand.

---

## RMSE

Root Mean Squared Error

$$
RMSE=\sqrt{mean(e^2)}
$$

Characteristics:

```text
Punishes large errors heavily.
```

Sensitive to outliers.

---

## MAPE

Mean Absolute Percentage Error

$$
MAPE=mean(|p_t|)
$$

where

$$
p_t=100\frac{e_t}{y_t}
$$

Advantages:

- Unit free

Problems:

- Undefined when actual value is zero
- Unstable near zero

---

## sMAPE

Symmetric MAPE

Rarely recommended.

FPP3 explicitly discourages using it.

---

# Scaled Errors

Purpose:

```text
Compare accuracy
across different datasets.
```

---

## MASE

Mean Absolute Scaled Error

Most important scaled metric.

Interpretation:

### MASE < 1

```text
Better than Naive benchmark.
```

### MASE = 1

```text
Same as Naive benchmark.
```

### MASE > 1

```text
Worse than Naive benchmark.
```

---

## RMSSE

Scaled version of RMSE.

Used similarly to MASE but squares errors.

---

# Key Exam Takeaways

1. Residuals should resemble white noise.
2. Good residuals:
   - Mean ≈ 0
   - No autocorrelation
   - Constant variance
3. Ljung-Box:
   - p > 0.05 → good
   - p < 0.05 → bad
4. Longer forecast horizon → wider prediction intervals.
5. Forecast errors are calculated on test data.
6. Residuals are calculated on training data.
7. MASE < 1 means better than Naive.
8. Seasonal Naive is usually the benchmark for seasonal data.
9. Bootstrap intervals do not require normal residuals.
10. Decomposition forecasts components separately and then recombines them.