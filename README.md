# A Rigorous Approach to Valuing Weather Derivatives Through Integrative Time-Series Analysis and Stochastic Weather Forecasting Models
Project that aims to determine the fair value of weather-related options which are contracts based on Cooling Day Degrees &amp; Heating Day Degrees. 

## Table of Contents

- [Overview](#models-used)
- [Data Sources](#data_sources)
- [Preliminary Observations](#preliminary-observations)
- [Stochastic Modeling - Ornstein-Uhlenbeck](#ornstein-uhlenbeck-model)
    - [Correlated Brownian Motions](#correlated-brownian-motions)
- [Time-Series Modeling](time-series-modeling)


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
After some data-cleaning we can begin to do some preliminary analysis of our dataset. Firstly from observing the distribution of our initial raw dataset, its clear that the data has some inherent seasonality to it. To convert the dataset to a stationary process we must initially remove this cycliality. This is done through an additive model based on: 
$$ 
Y(t) = T(t) + S(t) + R(t)
$$

Where:
- $ Y(t) $ is the observed time series at time $ t $.
- $ T(t) $ is the trend component at time $ t $, representing the long-term progression in the data.
- $ S(t) $ is the seasonal component at time $ t $, capturing the repeating patterns or cycles.
- $ R(t) $ is the residual component at time $ t $, representing the random noise or irregular fluctuations.


Firstly we run an ADFuller Test to determine if our data is stationary. 
<p>&nbsp;</p>
<img width="347" alt="Screenshot 2024-07-26 at 4 42 19 PM" src="https://github.com/user-attachments/assets/55dd7d80-e0ad-4d47-8e26-5b854ee6c8cb">
<p>&nbsp;</p>
The output of the test indeed shows that the data follows a stationary process and thus proper time-series modelling techniques can be applied.
Secondly, we should determine if our dataset 
<img width="967" alt="Screenshot 2024-07-26 at 4 44 51 PM" src="https://github.com/user-attachments/assets/b793aaa8-072a-44b5-aadc-10c0e903af10">
<p>&nbsp;</p>


<img width="925" alt="Screenshot 2024-07-26 at 3 19 15 PM" src="https://github.com/user-attachments/assets/fd53cb6f-884b-482d-9a35-052f77a7de1b">


## Ornstein-Uhlenbeck Model
The Ornstein-Uhlenbeck Model is a continous time Gaussian process governed by the stochastic differential equation: 

$$
dX_t = \theta (\mu - X_t) dt + \sigma dW_t
$$

The brownian motion given by the variable $dW_t$ follows a Gaussian process whose increments only depend on the time dependence between them. The brownian increment here ensures the process is markovian and exhibits the traditional randomness at any given moment for a stochastic differential equation (SDE).

The key feature of this process is the mean-reversion tendency given by a rate of decay (Rate of Reversion) $\theta$, making it highly applicable in financial modelling. Its parameters are best estimated through Maximum Likelihood Estimation but in this case of this project was estimated through linear regression and autcorrelation. 

Simulations of the process allow us to model temperature itself as a stochastic process with a mean-reverting property (Weather Seasons) with a rate parameter given by $\theta$ where $\theta$ is calculated as the rate of decay of autocorrelation from lag 0 to the nth lag.

<p>&nbsp;</p>

The Simulated path forecast is shown below where the temperature follows a mean-reverting behavior towards its long-term average.
<p>&nbsp;</p>
<img width="419" alt="Screenshot 2024-07-15 at 4 16 16 PM" src="https://github.com/user-attachments/assets/1d8ed57b-8eea-4f4e-9234-c642b70b3165">



### Correlated Brownian Motions: 
A significant modeling tool that is used frequently when dealing with financial derivatives is the need to create correleated brownian motions. This arises frequently in situations when an assets price follows a stochastic process and another variable within the pricing equation itself also follows its own stochastic process. This is observed keenly in options pricing like the Heston model or in interest rate models. For our case, we can generate two correlated brownian motions that help to create the required equations. This can be done through a cholesky decomposition of a correlation matrix. 
We can specify the correlation coefficient we wish to have for our two equations in this case lets say p = 0.7. Our correlation matrix then would look like this: [[1.0, 0.7], [0.7, 1.0]]. 



## Time Series Modeling

<img width="1052" alt="Screenshot 2024-07-15 at 4 41 02 PM" src="https://github.com/user-attachments/assets/6a252141-935b-4a60-be99-09c8f75c193f">









References:








  
