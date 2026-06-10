- Trend: A trend exists when there is a long-term increase or decrease in the data. It does not have to be linear. Sometimes we will refer to a trend as “changing direction”, when it might go from an increasing trend to a decreasing trend.
- Seasonal: A seasonal pattern occurs when a time series is affected by seasonal factors such as the time of the year, the day of the week or the hour of the day. 
- Cyclic: A cycle occurs when the data exhibit rises and falls that are not of a fixed frequency. These fluctuations are usually due to economic conditions, and are often related to the “business cycle”. The duration of these fluctuations is usually at least 2 years.

differences between seasonal and cyclic patters:
- seasonal patterns constant length; cyclic pattern variable length
- average length of cycle longer than length of seasonal pattern
- magnitude of cycle more variable than magnitude of seasonal pattern

The timing of peaks and troughs is predictable with seasonal data, but unpredictable in the long term with cyclic data

- seasonal plots enable the underlying seasonal pattern to be seen more clearly, and also allows any substantial depatures from the seasonal pattern to be 
easily identified

# 

correlation coefficient: measures the extent of linear relationshop between two variables (y and x): 
- lies between -1 and 1
- 
$$
r = \frac{\sum_{t=1}^{T}(y_t-\bar{y})(x_t-\bar{x})}
{\sqrt{\sum_{t=1}^{T}(y_t-\bar{y})^2}\sqrt{\sum_{t=1}^{T}(x_t-\bar{x})^2}}
$$

#

- Lag Plots: A lag plot is a scatter plot that helps you see whether a time series is related to its past values. A lag plot compares the series with itself shifted by k periods. A clear pattern means correlation at that lag; a cloud means little or no correlation. Multiple lag plots help reveal how dependence changes across different lags and can expose seasonality.
- When you see a lag plot, ask: "Can the past values of this series help predict future values of this same series?": If the lag plot show strong patters -> probably yes. If the lag plots look like random clouds -> probably not
- A lag of 1 means one time step back. A lag is the past value itself, not the difference


# 

Autocorrelation
- Just as correlation measures the extent of a linear relationship between two variables, autocorrelation measures the linear relationship between lagged values of a time series.

- There are several autocorrelation coefficients, corresponding to each panel in the lag plot. For example, $r_1$ measures the relationship between $y_t$ and $y_{t-1}$, $r_2$ measures the relationship between $y_t$ and $y_{t-2}$, and so on.

- The value of $r_k$ can be written as

$$
r_k =
\frac{
\sum_{t=k+1}^{T}
(y_t - \bar{y})(y_{t-k} - \bar{y})
}{
\sum_{t=1}^{T}
(y_t - \bar{y})^2
}
$$

where $T$ is the length of the time series. The autocorrelation coefficients make up the **autocorrelation function (ACF)**.


- when data have a trend, the autocorrelations for small lags tend to be large and positive
- when data are seasonal, the autocorrelations will be larget at the seasonal lags (i.e., at multiples of the seasonal frequancy)
- when data are tranded and seasonal, you see a combination of these affects

# 

Time series that show no autocorrelation are called white noise.


- In an ACF (Autocorrelation Function) plot, the blue bounds represent the 95% confidence interval. They act as a significance threshold to determine whether the correlation between a time series and its lagged values is statistically meaningful
    - Inside the blue bounds: Any lag (bar) that falls completely within the blue area is considered statistically insignificant. These correlations are close to zero and are likely just random noise.
    - Outside the blue bounds: Any lag that extends beyond the blue limits is considered statistically significant. This means there is a strong, meaningful correlation between the data point and its past value at that specific lag.
- It might be important to do an ACF plotting even though the actual time plot could look like a white noise series. The ACF plot might show significat autocorrelation for seasonal lags such as 3 (quarterly) or 12 (yearly).