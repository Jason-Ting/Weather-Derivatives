# Weather-Derivatives
Project that aims to determine the fair value of weather-related options which are contracts based on Cooling Day Degrees &amp; Heating Day Degrees. 
List of models used include: 

List of models used include:
- ARIMA: Standard Autoregressive Integrated Moving Average
- SARIMAX: ARIMA with extended seasonality in dataset and influence of exogenous variables
- CARMA: Continous time ARIMA Process
- Ornstein Uhlenbeck Process: Mean-reverting stochastic/markov process

Techniques used include:
- Cholesky Decomposition: Used to generate multiple correlated Brownian Motions, can be extended to correlate two stochastic differential equations
- Seasonal Decomposition: Simplified fast-fourier transform using seasonal decomposition
- Partial Autocorrelations & Autocorrelations: Used to determine the order of Autoregressive and Moving Average terms
  
