# A Rigorous Approach to Valuing Weather Derivatives Through Integrative Time-Series Analysis and Stochastic Weather Forecasting Models
Project that aims to determine the fair value of weather-related options which are contracts based on Cooling Day Degrees &amp; Heating Day Degrees. 


Models Used: 
- Ornstein Uhlenbeck Process: Mean-reverting stochastic/markov process, with drift and standard brownian motion
- ARIMA: Standard Autoregressive Integrated Moving Average
- SARIMAX: ARIMA with extended seasonality in dataset and influence of exogenous variables
- CARMA: Continous time ARIMA Process
  
Techniques Used:
- Cholesky Decomposition: Used to generate multiple correlated Brownian Motions, can be extended to correlate two seperate stochastic differential equations
- Seasonal Decomposition: Simplified fast-fourier transform using seasonal decomposition
- Partial Autocorrelations & Autocorrelations: Used to determine the order of Autoregressive and Moving Average terms

# Ornstein-Uhlenbeck Model

$$
dX_t = \theta (\mu - X_t) dt + \sigma dW_t
$$

This stochastic equation is governed by a brownian motion $$ dW_t $$ drawn from a normal distribution








Data Sources: 



References:








  
