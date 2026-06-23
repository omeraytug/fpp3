# Simple Linear Regression and Least Squares Estimation

## Simple Linear Regression Model

A Simple Linear Regression Model describes the relationship between:

- One predictor variable (`x`)
- One target (forecast) variable (`y`)

The model is:

$$
y = \beta_0 + \beta_1x + \varepsilon
$$

Where:

- `y` = target / forecast variable
- `x` = predictor variable
- `β₀` = intercept
- `β₁` = slope coefficient
- `ε` = random error term

The model assumes there is a linear relationship between `x` and `y`.

---

## What are Coefficients?

Coefficients are the numbers that define the regression line.

Example:

$$
\hat{y} = 20 + 0.6x
$$

The coefficients are:

- Intercept = 20
- Slope = 0.6

---

## Intercept (β₀)

The intercept is the predicted value of `y` when `x = 0`.

Example:

$$
\hat{y} = 20 + 0.6(0) = 20
$$

Interpretation:

> When x = 0, the predicted value of y is 20.

---

## Slope Coefficient (β₁)

The slope coefficient tells us how much `y` changes when `x` increases by 1 unit.

Example:

$$
\hat{y} = 20 + 0.6x
$$

Interpretation:

> For every 1-unit increase in x, y increases by 0.6 units on average.

---

## What is Least Squares Estimation?

Least Squares Estimation (Ordinary Least Squares, OLS) is the method used to estimate the coefficients.

The regression model tells us the form of the line:

$$
y = \beta_0 + \beta_1x + \varepsilon
$$

But we do not know the values of `β₀` and `β₁`.

Least Squares finds the values that create the best-fitting line.

---

## Residuals

A residual is:

$$
e_i = y_i - \hat{y}_i
$$

Where:

- `yᵢ` = actual value
- `ŷᵢ` = fitted (predicted) value

Residual = Actual − Predicted

---

## Least Squares Objective

Least Squares chooses the coefficients that minimize the sum of squared residuals:

$$
\sum_{i=1}^{n} (y_i - \hat{y}_i)^2
$$

This is called the Residual Sum of Squares (RSS).

Goal:

$$
\min \sum_{i=1}^{n} (y_i - \hat{y}_i)^2
$$

Interpretation:

> Find the line that makes the squared prediction errors as small as possible.

---

## Why Square the Residuals?

1. Prevents positive and negative errors from cancelling out.
2. Penalizes large errors more heavily.
3. Produces a mathematically convenient optimization problem.

Example:

| Error | Squared Error |
|------:|--------------:|
| 2 | 4 |
| 10 | 100 |

Large errors receive much larger penalties.

---

## Relationship Between Regression and Least Squares

### Regression Model

Defines the relationship:

$$
y = \beta_0 + \beta_1x + \varepsilon
$$

### Least Squares Estimation

Finds:

$$
\hat{\beta}_0, \hat{\beta}_1
$$

These estimated coefficients produce the fitted regression line:

$$
\hat{y} = \hat{\beta}_0 + \hat{\beta}_1x
$$

---

## Example

Suppose Least Squares estimates:

$$
\hat{\beta}_0 = 5
$$

and

$$
\hat{\beta}_1 = 0.75
$$

The fitted model becomes:

$$
\hat{y} = 5 + 0.75x
$$

Interpretation:

- Predicted y is 5 when x = 0.
- For every 1-unit increase in x, y increases by 0.75 units on average.

---

## Workflow

### Step 1: Assume a Model

$$
y = \beta_0 + \beta_1x + \varepsilon
$$

### Step 2: Use Least Squares Estimation

Find:

$$
\hat{\beta}_0, \hat{\beta}_1
$$

that minimize:

$$
\sum_{i=1}^{n} (y_i - \hat{y}_i)^2
$$

### Step 3: Build the Fitted Model

$$
\hat{y} = \hat{\beta}_0 + \hat{\beta}_1x
$$

### Step 4: Make Predictions

Plug new values of `x` into the fitted equation.

---

## Scikit-Learn Example

```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(X, y)
```

The `.fit()` method performs Least Squares Estimation.

Estimated coefficients:

```python
model.intercept_   # β̂₀
model.coef_        # β̂₁
```

Predictions:

```python
y_hat = model.predict(X)
```

Where:

- `y_hat` = fitted values
- `y - y_hat` = residuals

---

## Key Takeaways

- A Simple Linear Regression Model describes a linear relationship between one predictor (`x`) and one target (`y`).
- Coefficients are the numbers that define the regression line.
- The intercept (`β₀`) is the predicted value when `x = 0`.
- The slope (`β₁`) tells us how much `y` changes when `x` increases by 1 unit.
- Least Squares Estimation (OLS) is the method used to estimate the coefficients.
- OLS chooses the coefficients that minimize the sum of squared residuals (RSS).
- Fitted values are predictions from the regression line.
- Residuals are the differences between actual and fitted values.


### P-values and Forecasting

A p-value measures how much evidence we have that a predictor's coefficient is different from zero after accounting for the other predictors in the model.

A small p-value suggests that the predictor contributes information beyond the other predictors already included in the model.

A large p-value suggests that there is not enough evidence that the predictor adds unique information to the model.

Statistical significance and forecasting usefulness are not the same thing. A predictor can have a large p-value and still improve forecast accuracy.

P-values are mainly used for inference, where the goal is to understand the relationship between predictors and the target variable.

Forecasting focuses on predictive performance rather than statistical significance.

When predictors are highly correlated, p-values can become misleading because the model struggles to separate the contribution of each predictor.

This phenomenon is known as multicollinearity.

A predictor with a large p-value should not automatically be removed from a forecasting model.

For forecasting, predictor selection should be based on predictive accuracy measures such as CV, AIC, AICc, RMSE, or other out-of-sample evaluation metrics.

The predictor that gives the best forecasts is not always the predictor with the smallest p-value.

FPP3 recommends using AICc, AIC, or Cross-Validation for selecting predictors instead of relying on p-values.

A p-value asks "Does this predictor have a statistically detectable effect?", while AICc and CV ask "Does this predictor help me forecast better?".