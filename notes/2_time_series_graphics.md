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