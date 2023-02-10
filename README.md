# Dissertation
Analysing Government Policies on reproduction of COVID-19 via Parameter Estimation Methods

## Methodology
A slightly modified version of the epidemiological SIR model is utilised, the SIRD model. This model splits the Removed compartment into: Removed (Alive) and Dead. This is useful to us since deaths recorded is one of the more common data available to us. 

SIRD:


$\dfrac{dS}{dt} = S-\dfrac{\beta I S}{N}$


$\dfrac{dI}{dt} = \dfrac{\beta I S}{N} - \gamma I - \rho I$


$\dfrac{dR}{dt} = \gamma I$ 


$\dfrac{dD}{dt} = \rho I $


### Parameters
We can then utilise this information to do parameter estimation to obtain the parameters of the model:
- $\gamma$ = Recovery Rate
- $\beta$ = Infection Rate
- $\rho$ = Death Rate

This is helpful to know since the Reproduction Rate of COVID-19 can then be obtained by the following equation:
- $R_0 = \frac{\beta}{\gamma+\rho}$

### Parameters Estimation
To predict the information, we will utilise Markov Chain Monte Carlo to do the parameter estimation. To do so, a number of priors and a likelihood function have been chosen to allow for the MCMC model to work:

Priors:
- $\beta$ = Inverse Gamma
- $\gamma$ = = Inverse Gamma
- $\rho$ = Truncated Normal
- $I_0$ = Poisson

For the likelihood function, we need to chose an equation that allows MCMC to estimate all the necessary parameters, thanks to this paper, we can write $D(t)$ as such:

$ D(t) = I_0(1+k)^{\dfrac{\beta}{\beta-\gamma}}(1+ke^{(\beta-\gamma)(t-t_0)})^{-\dfrac{\beta}{\beta-\gamma}}e^{(\beta-\gamma)(t-t_0)} $

Likelihood Function:
- Truncated Normal
### Comparison
Once parameter estimation is complete, the $R_0$ values will be compared, utilising a heatmap of Europe to see the decrease, or increase, in the value.

### Forecasting
Lastly, forecasting, utilising the recently obtained parameters, will be done to show what would've happened if governments had not intervened. To do so, SIRD models will be plotted to obtained the necessary data (cumulative deaths). The predicted data will then be compared with the real life data, to understand the different trends.
