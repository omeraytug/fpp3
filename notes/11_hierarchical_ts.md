# FPP3 Chapter 11.2 & 11.3 Notes

# Hierarchical Forecasting

## Goal

Produce **coherent forecasts**, meaning forecasts satisfy the aggregation constraints.

Example:

```
        Total
       /     \
      A       B
    / | \    / \
  AA AB AC BA BB
```

A coherent forecast always satisfies:

```
Total = A + B
A = AA + AB + AC
B = BA + BB
```

---

# 11.2 Single-Level Approaches

Traditional methods only forecast **one level** of the hierarchy and derive the remaining levels.

There are three classical approaches:

- Bottom-up
- Top-down
- Middle-out

---

## Bottom-up

### Workflow

1. Forecast every bottom-level series.
2. Sum forecasts upwards.

Example:

```
Forecast:

AA = 10
AB = 15
AC = 20
BA = 30
BB = 25
```

Then

```
A = 45
B = 55
Total = 100
```

### Advantages

- Uses all bottom-level information.
- Captures local trends and seasonality.
- No information is lost due to aggregation.
- Forecasts are automatically coherent.

### Disadvantages

- Bottom-level series are often noisy.
- Harder to model accurately.

---

## Top-down

### Workflow

1. Forecast only the total series.
2. Split the forecast into lower levels using proportions.

Example:

```
Forecast Total = 100
```

Historical proportions:

```
AA = 10%
AB = 15%
AC = 20%
BA = 30%
BB = 25%
```

Result:

```
AA = 10
AB = 15
AC = 20
BA = 30
BB = 25
```

### Advantages

- Only one model required.
- Aggregate series is smoother and easier to forecast.

### Disadvantages

- Loses information from lower levels.
- Cannot capture local behaviour.
- Lower-level forecasts are usually less accurate.

---

## Historical Proportion Methods

### 1. Average Historical Proportions

Compute the proportion at every time period:

```
Store / Total
```

Then average these proportions.

Example:

```
Month 1: 20%
Month 2: 10%
Month 3: 50%

Average proportion

=(20%+10%+50%)/3
```

Every period contributes equally.

---

### 2. Proportion of Historical Averages

Average the values first.

```
Average Store

/

Average Total
```

Large observations naturally have more influence.

Difference:

```
Average(Store / Total)

≠

Average(Store)
/ Average(Total)
```

---

## Forecast Proportions

Instead of using historical proportions:

1. Produce initial forecasts for every series.
2. Calculate proportions using those forecasts.
3. Split the total forecast according to these forecast-based proportions.

Generally more accurate because proportions can change over time.

---

## Middle-out

Forecast only a middle level.

```
Top
 ↑
Bottom-up

Middle
 ↓

Top-down

Bottom
```

Above the middle:

- Aggregate upward.

Below the middle:

- Disaggregate downward.

---

# Limitation of Single-Level Methods

Bottom-up:

- Ignores forecasts above the bottom level.

Top-down:

- Ignores forecasts below the top level.

Middle-out:

- Ignores forecasts outside the chosen middle level.

All three discard potentially useful information.

---

# 11.3 Forecast Reconciliation

## Main Idea

Instead of using forecasts from only one level:

Forecast **every series**.

Then adjust them so they become coherent.

---

## Base Forecasts

Each series has its own forecast.

Example:

```
Total = 100

A = 47

B = 56

AA = 11

AB = 15

AC = 20

BA = 31

BB = 24
```

These are usually **not coherent**.

Example:

```
A + B = 103

≠

Total = 100
```

---

## Forecast Reconciliation

Rather than throwing forecasts away:

Adjust every forecast slightly until:

```
Total = A + B

A = AA + AB + AC

B = BA + BB
```

All forecasts become coherent.

---

# Summing Matrix (S)

The summing matrix stores the aggregation structure.

Conceptually:

```
Bottom forecasts

↓

Sum according to hierarchy

↓

All upper levels
```

S does **not** forecast.

It only performs the aggregation.

---

# Mapping Matrix (G)

G determines how bottom-level forecasts are obtained.

Examples:

Bottom-up:

- Keep bottom forecasts.
- Ignore higher-level forecasts.

Top-down:

- Keep top forecast.
- Split downward.

MinT:

- Use information from every forecast.

---

# General Reconciliation Formula

```
Coherent Forecasts

=

S G Base Forecasts
```

Interpretation:

```
Base forecasts

↓

G chooses/adjusts bottom forecasts

↓

S rebuilds hierarchy

↓

Coherent forecasts
```

---

# MinT (Minimum Trace)

Modern reconciliation method.

Instead of trusting only one level:

Uses **all base forecasts**.

Adjusts them optimally while maintaining coherence.

Objective:

- Keep forecasts coherent.
- Minimize total forecast uncertainty.

---

## Why MinT is Better

Bottom-up:

Uses only bottom forecasts.

Top-down:

Uses only top forecasts.

MinT:

Uses forecasts from every level simultaneously.

This generally improves forecast accuracy.

---

# Estimating Forecast Error Covariance

MinT needs information about historical forecast errors.

Several approximations exist:

- OLS
- WLS (variance scaling)
- WLS (structural scaling)
- MinT covariance
- MinT shrinkage

These differ only in how the forecast error covariance matrix is estimated.

---

# Key Takeaways

- Hierarchical forecasting requires coherent forecasts.
- Bottom-up, top-down and middle-out use only one level.
- Forecast reconciliation combines forecasts from all levels.
- MinT is the modern optimal reconciliation approach.
- S represents the hierarchy.
- G determines how forecasts are reconciled.
