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
The Ornstein-Uhlenbeck Model is a continous time Gaussian process governed by the stochastic differential equation: 

$$
dX_t = \theta (\mu - X_t) dt + \sigma dW_t
$$

The brownian motion given by the variable $dW_t$ follows a Gaussian process whose increments only depend on the time dependence between them. The brownian increment here ensures the process is markovian and exhibits the traditional randomness at any given moment for a stochastic differential equation (SDE).

The key feature of this process is the mean-reversion tendency given by a rate of decay (Rate of Reversion) $\theta$, making it highly applicable in financial modelling. Its parameters are best estimated through Maximum Likelihood Estimation but in this case of this project was estimated through linear regression and autcorrelation. 

Simulations of the process allow us to model temperature itself as a stochastic process with a mean-reverting property (Weather Seasons) with a rate parameter given by $\theta$ where $\theta$ is calculated as the rate of decay of autocorrelation from lag 0 to the nth lag.

<img width="419" alt="Screenshot 2024-07-15 at 4 16 16 PM" src="https://github.com/user-attachments/assets/1d8ed57b-8eea-4f4e-9234-c642b70b3165">




<img width="1052" alt="Screenshot 2024-07-15 at 4 41 02 PM" src="https://github.com/user-attachments/assets/6a252141-935b-4a60-be99-09c8f75c193f">


Data Sources: 




References:








  
