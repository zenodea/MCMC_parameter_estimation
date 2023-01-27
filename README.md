# Dissertation
Analysing Government Policies on reproduction of COVID-19 via Parameter Estimation Methods

## Methodology
A slightly modified version of the epidemiological SIR model is utilised, the SIRD model. This model splits the Removed compartment into: Removed (Alive) and Dead. This is useful to us since deaths recorded is one of the more common data available to us. 

### Parameters
We can then utilise this information to do parameter estimation to obtain the parameters of the model:
- $\gamma$ = Recovery Rate
- $\beta$ = Infection Rate

This is helpful to know since the Reproduction Rate of COVID-19 can then be obtained by the following equation:
- $R_0 = \frac{\beta}{\gamma}$

### Parameters Estimation
To predict the information, we will utilise Markov Chain Monte Carlo to do the parameter estimation.
