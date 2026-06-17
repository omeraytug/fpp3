- error: forecast error

ME = Mean Error: mean(error) - you take average of them and some of these will be positive, some will be negative - good for detecting bias, bad for measuring accuracy
MAE = Mean Absolute Error: You take absolute of each error and then the average of them
MSE = Mean Squared Error: you square all the forecast errors and take the mean - scaled to square - large errors get punished heavily
RMSE: Root Mean Squared Error - original scale of the MSE
MAPE: Mean Absolute Percantage Error: You take the absolute of the errors divide by the actual observations and multiply by 100
MASE: Mean Absolute Scaled Error
RMSSE: Root Mean Squared Scaled Error


MAE, MSE, RMSE are all scale dependent
MAPE is scale independent but is only sensible if y_t >> 0 for all t, and y has a natural zero


ME = Mean Error: mean(error) - you take the average of all forecast errors, so some errors will be positive and some negative. Good for detecting bias (whether forecasts are systematically too high or too low). Bad for measuring accuracy because positive and negative errors can cancel each other out.

MAE = Mean Absolute Error: you take the absolute value of each forecast error and then compute the average. Easy to understand and interpret because it tells you the average size of the forecast error in the original units. Bad because it treats all errors equally and does not penalize very large errors much more than small errors.

MSE = Mean Squared Error: you square all forecast errors and then take the average. Good because large errors are punished heavily, making it useful when large mistakes are especially costly. Bad because the result is in squared units, making it difficult to interpret directly.

RMSE = Root Mean Squared Error: the square root of MSE, bringing the metric back to the original scale of the data. Good because it is interpretable and still penalizes large errors more than MAE. Bad because it can be heavily influenced by a few large forecast errors.

MAPE = Mean Absolute Percentage Error: you take the absolute forecast error, divide it by the actual observation, multiply by 100, and then average across all observations. Good because it is scale-independent and easy to communicate as a percentage. Bad because it breaks when actual values are zero and can become extremely large when actual values are close to zero.

MASE = Mean Absolute Scaled Error: MAE scaled by the MAE of a simple benchmark forecast (usually the Naive forecast). Good because it is scale-independent, works with zeros, and immediately tells you whether your model is better than a simple benchmark. A value below 1 means the model outperforms the benchmark. Bad because it is slightly less intuitive for non-technical audiences than MAE or MAPE.

RMSSE = Root Mean Squared Scaled Error: RMSE scaled by the RMSE of a benchmark forecast (usually the Naive forecast). Good because it is scale-independent, works with zeros, and penalizes large errors while allowing comparison across different time series. A value below 1 means the model outperforms the benchmark. Bad because it is less intuitive to explain and can still be sensitive to large outliers due to the squared errors.