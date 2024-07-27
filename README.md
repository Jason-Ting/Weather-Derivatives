# A Rigorous Approach to Valuing Weather Derivatives Through Integrative Time-Series Analysis and Stochastic Weather Forecasting Models
Project that aims to determine the fair value of weather-related options which are contracts based on Cooling Day Degrees &amp; Heating Day Degrees. 

## Table of Contents

- [Overview](#models-used)
- [Data Sources](#data-sources)
- [Preliminary Observations](#preliminary-observations)
- [Stochastic Modeling - Ornstein-Uhlenbeck](#ornstein-uhlenbeck-model)
    - [Closed Form Solutions](#closed-form-solutions)     
    - [Correlated Brownian Motions](#correlated-brownian-motions)
- [Time-Series Modeling](#time-series-modeling)
    - [ARIMA](#arima)
    - [SARIMAX](#sarimax)
    - [CARMA](#carma)
        - [Intuitive Explanations](#intuitive-explanations)
      


## Models Used: 
- Ornstein Uhlenbeck Process: Mean-reverting stochastic/markov process, with drift and standard brownian motion
- ARIMA: Standard Autoregressive Integrated Moving Average
- SARIMAX: ARIMA with extended seasonality in dataset and influence of exogenous variables
- CARMA: Continous time ARIMA Process

Techniques Used:
- Cholesky Decomposition: Used to generate multiple correlated Brownian Motions, can be extended to correlate two seperate stochastic differential equations
- Seasonal Decomposition: Using an additive model to convert a seasonal dataset to a stationary process
- Partial Autocorrelations & Autocorrelations: Used to determine the order of Autoregressive and Moving Average terms


## Data Sources:
Data for the project conists of CSV file containing the daily maximum and minimum temperatures in Abilene Regional Airport in Texas from 1985 - 2024. The location is chosen because of its geographical signficance since many weather futures are traded in the state of Texas.


## Preliminary Observations:
After some data-cleaning we can begin to do some preliminary analysis of our dataset. Firstly from observing the distribution of our initial raw dataset, its clear that the data has some inherent seasonality to it. To convert the dataset to a stationary process we must initially remove this cycliality. This is done through an additive model that assumes the dataset is composed of a trend, stochastic (residual), and seasonal component. 

### Additive Model

$$ Y(t) = T(t) + S(t) + R(t) $$

Where:
- $Y(t)$ is the observed time series at time $t$.
- $T(t)$ is the trend component at time $t$, representing the long-term progression in the data.
- $S(t)$ is the seasonal component at time $t$, capturing the repeating patterns or cycles.
- $R(t)$ is the residual component at time $t$, representing the random noise or irregular fluctuations.

The difficulty in this decomposition is determining the seasonal component as the residual can be determined once the seasonality is found. Because the detrending needs to account for varying time trends, we subtract the values of Y(t) by the rolling mean values instead of just the long-run average. The seasonal component can be obtained through an average of the detrended values for the same day but varying years. The average of these values will provide us the seasonality component.

After we have detrended our dataset, we should test it for stationarity if we are to do some time-series modelling.
<p>&nbsp;</p>
<img width="347" alt="Screenshot 2024-07-26 at 4 42 19 PM" src="https://github.com/user-attachments/assets/55dd7d80-e0ad-4d47-8e26-5b854ee6c8cb">
<p>&nbsp;</p>
The output of the ADFuller test indeed shows that the data follows a stationary process and thus proper time-series modelling techniques can be applied.
Secondly, we should determine if our dataset still has inter-temporal dependence after detrending. We plot the partial autocorrelations and autocorrelations here. These will also assist us in determining the lag of our time-series models. 
<p>&nbsp;</p>
<img width="967" alt="Screenshot 2024-07-26 at 4 44 51 PM" src="https://github.com/user-attachments/assets/b793aaa8-072a-44b5-aadc-10c0e903af10">
<p>&nbsp;</p>
Sure enough there is signficant lags above the test-statistic indicating the data contains some inter-temporal dependence.


## Ornstein-Uhlenbeck Model
A key feature of our model is the usage of stochastic weather forecasting that aims to simulate weather temperatures over time. For that, we use an OU model which is a continous time Gaussian process governed by the stochastic differential equation: 

$$
dX_t = \theta (\mu - X_t) dt + \sigma dW_t
$$

The brownian motion given by the variable $dW_t$ follows a Gaussian process whose increments only depend on the time dependence between them. The brownian increment here ensures the process is markovian and exhibits the traditional randomness at any given moment for a stochastic differential equation (SDE).

The key feature of this process is the mean-reversion tendency given by a rate of decay (Rate of Reversion) $\theta$, making it highly applicable in financial modelling. Its parameters are best estimated through Maximum Likelihood Estimation but in this case of this project was estimated through linear regression and autcorrelation. 

Simulations of the process allow us to model temperature itself as a stochastic process with a mean-reverting property (Weather Seasons) with a rate parameter given by $\theta$ where $\theta$ is calculated as the rate of decay of autocorrelation from lag 0 to the nth lag.

The Simulated path forecast is shown below where the temperature follows a mean-reverting behavior towards its long-term average.
<p>&nbsp;</p>
<img width="419" alt="Screenshot 2024-07-15 at 4 16 16 PM" src="https://github.com/user-attachments/assets/1d8ed57b-8eea-4f4e-9234-c642b70b3165">

### Closed Form Solutions: 
There also lies a closed form solution to the Ornstein-Uhlenbeck Process. The mathematics follow this line of reasoning where 



### Correlated Brownian Motions: 
A significant modeling tool that is used frequently when dealing with financial derivatives is the need to create correleated brownian motions. This arises frequently in situations when an assets price follows a stochastic process and another variable within the pricing equation itself also follows its own stochastic process. This is observed keenly in options pricing like the Heston model or in interest rate models. For our case, we can generate two correlated brownian motions that help to create the required equations. This can be done through a cholesky decomposition of a correlation matrix. 
We can specify the correlation coefficient we wish to have for our two equations in this case lets say p = 0.7. Our correlation matrix then would look like this: [[1.0, 0.7], [0.7, 1.0]]. 
<p>&nbsp;</p>
<img width="637" alt="Screenshot 2024-07-27 at 7 31 39 PM" src="https://github.com/user-attachments/assets/72473936-e3f7-4774-8d49-e7bd933cce65">
<p>&nbsp;</p>


## Time Series Modeling

### ARIMA
<img width="1052" alt="Screenshot 2024-07-15 at 4 41 02 PM" src="https://github.com/user-attachments/assets/6a252141-935b-4a60-be99-09c8f75c193f">




<p>&nbsp;</p>
<img width="925" alt="Screenshot 2024-07-26 at 3 19 15 PM" src="https://github.com/user-attachments/assets/fd53cb6f-884b-482d-9a35-052f77a7de1b">
<p>&nbsp;</p>

### SARIMAX


### CARMA:
CARMA is a continous-time autoregressive moving average model that follows the same format of a typical ARIMA/ARMA model with the exception that values are continous and non-discrete. This makes it very valuable when modelling minute time intervals or in-between time intervals that would otherwise require interpolation. The CARMA(2,0) used in the code follows this format: (Where 2 is the order of the autoregressive component) 
$$
a_2 \frac{d^2 X_t}{dt^2} + a_1 \frac{dX_t}{dt} + a_0 X_t = Z_t 
$$

#### Intuitive Explanations
The reason the formula uses differentiated polynomials for its autoregressive term can be intuitevly explained through several properties.
1) Taylor Series Expansion: Like a taylor series expansion, the polynomials here represent the order of derivatives and coefficients centered around a certain point used to approximate the curvature of a function. In this case, because we are trying to approximate the seasonality aspect of temperature, which closely resembles a cubic function, the 3rd order derivative to the 1st order derivative is required.
2) ARIMA in the Limit: If we were to think of the alpha coefficients as the weighted effects of prior lags (AR Beta's) like in a traditional ARIMA process, we can ask what the prior effect of yesterday's value has on today's value. Now if we were to convert the discretized process into a continous time process and ask what the effect is of a second prior on the value right now, in the limit this becomes instantaneous rate of change and is the definition of a derivative. 
3) Through integrating this process, we can find the path that the temperature takes 


References:








  
