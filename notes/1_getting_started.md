# Easy to forecast if

- we have a good understanding of the factors that contribute to
- lots of data available
- future is somewhat similar to the past
- the forecasts cannot affect the thing that we are trying to forecast -

The 4th one is strong case for financial forecasting: forecast on a stock could nudge people into investing which would affect the forecast itself in either a positive or a negative way. especially if its a long term forecast. a financial forecast of 30-min on a stock exchange will be less difficult compared to a 6-month forecast

Many people wrongly assume that forecasts are not possible in a changing environment. Every environment is changing, and a good forecasting model captures the way in which things are changing.

#

Sometimes, there will be no data available at all. For example, we may wish to forecast the sales of a new product in its first year, but there are obviously no data to work with. In situations like this, we use judgmental forecasting

If there are no data available, or if the data available are not relevant to the forecasts, then **qualitative forecasting** methods must be used. These methods are not purely guesswork—there are well-developed structured approaches to obtaining good forecasts without using historical data.

Quantitative forecasting can be applied when two conditions are satisfied:

1. numerical information about the past is available;
2. it is reasonable to assume that some aspects of the past patterns will continue into the future.

Most quantitative prediction problems use either time series data (collected at regular intervals over time) or cross-sectional data (collected at a single point in time)

#

- Short-term forecasts
  are needed for the scheduling of personnel, production and transportation. As part of the scheduling process, forecasts of demand are often also required.
- Medium-term forecasts
  are needed to determine future resource requirements, in order to purchase raw materials, hire personnel, or buy machinery and equipment.
- Long-term forecasts
  are used in strategic planning. Such decisions must take account of market opportunities, environmental factors and internal resources.

#

Examples of time series data include:

- Annual Google profits
- Quarterly sales results for Amazon
- Monthly rainfall
- Weekly retail sales
- Daily IBM stock prices
- Hourly electricity demand
- 5-minute freeway traffic counts
- Time-stamped stock transaction data

#

- Explanatory model: helps explain what causes the variation in the electricty demand. The relationship is not exact, there will always be changes in the electricty demand that cannot be accounted by the predictor variables. The “error” term on the right allows for random variation and the effects of relevant variables that are not included in the model

  $$
  ED = f(\text{current temperature}, \text{strength of economy}, \text{population}, \text{time of day}, \text{day of week}, \text{error})
  $$

- Because the electricity demand data form a time series, we could also use a **time series model** for forecasting. In this case, a suitable time series forecasting equation is of the form where t is the present hour;

$$
ED_{t+1} = f(ED_t, ED_{t-1}, ED_{t-2}, ED_{t-3}, \ldots, \text{error})
$$

- Mixed models: combines the features of the above two models. They are known as dynamic regression models, panel data models, longitudinal models, transfer function models, and linear system models (assuming that f is linear)

$$
ED_{t+1} = f(ED_t, \text{current temperature}, \text{time of day}, \text{day of week}, \text{error})
$$

##### An explanatory model includes information from other variables instead of relying only on past values of the variable being forecasted. However, forecasters may still prefer time series models because the system may not be fully understood, relationships between variables can be difficult to measure, and predicting future values of predictor variables may be too challenging. In some cases, the main objective is simply to make accurate predictions rather than understand the reasons behind them. Additionally, time series models can sometimes provide more accurate forecasts than explanatory or mixed models.

#

Basic steps in a forecasting task:

1. Problem definition - most difficult part. Defining the problem requires the way of the forecasts will be used, who requires, how the forecasting function fits within the org
2. Gathering information - at least two kinds of information required: (a) statistical data, (b) the accumulated expertise of the people who collect the data and use the forecasts.
3. Preliminary (exploratary) analysis - always start by graphing the data. Consistent patterns? Significant trend? Seasonality important? Business cycles? Outliers that need to be explained by expert knowledge?
4. Choosing and fitting models
5. Using and evaluating a forecasting model - when using a forecasting model in practice; numerous practical issues such as how to handle missing values and outliers or how to deal with short time series

#

## Statistical Forecasting

In forecasting, the value we want to predict is treated as a **random variable** because its future value is unknown. A forecast estimates a **range of possible future values** rather than one exact number. The further into the future we forecast, the **higher the uncertainty** becomes.

The **forecast distribution** represents all possible future values and their probabilities based on the information available. If all known information is represented by `I`, then:

$$
y_t \mid I
$$

means the random variable \( y_t \) given everything we know in `I`.

The **point forecast** is the average (or median) of the forecast distribution and is written as:

$$
\hat{y}_t
$$

where the "hat" (`^`) means forecasted or estimated value.

A **prediction interval** gives a range where the future value is likely to fall with high probability. For example, a **95% prediction interval** means there is a 95% chance that the actual future value falls within the interval.

In time series forecasting:

$$
\hat{y}_{t|t-1}
$$

means forecasting time \( t \) using all previous observations:

$$
\{y_1, y_2, \ldots, y_{t-1}\}
$$

Similarly:

$$
\hat{y}_{T+h|T}
$$

means an **h-step ahead forecast** using all observations up to time \( T \).
