# Dissertation
Analysing Government Policies on reproduction of COVID-19 via Parameter Estimation Methods

## Methodology
A slightly modified version of the epidemiological SIR model is utilised, the SIRD model. This model splits the Removed compartment into: Removed (Alive) and Dead. This is useful to us since deaths recorded is one of the more common data available to us. 

SIRD:


$\dfrac{dS}{dt} = -\dfrac{\beta I S}{N}$


$\dfrac{dI}{dt} = \dfrac{\beta I S}{N} - \gamma I - \rho I$


$\dfrac{dR}{dt} = \gamma I$ 


$\dfrac{dD}{dt} = \rho I $


Using ordinary differential equation integration, we can write the following SIRD model in python, allowing us to plot the model:
```
def deriv(y, t, N, beta, gamma, rho):
    S, I, R, D = y
    dSdt = -(beta * S * I) / N
    dIdt = (beta * S * I / N) - (gamma * I) - (rho * I)
    dRdt = gamma * I
    dDdt = rho * I
    return dSdt, dIdt, dRdt, dDdt
```
### Parameters
We can then utilise this information to do parameter estimation to obtain the parameters of the model:

- $\gamma$ = Recovery Rate
- $\beta$ = Infection Rate
- $\rho$ = Death Rate

This is helpful to know since the Reproduction Rate of COVID-19 can then be obtained by the following equation:

- $R_0 = \frac{\beta}{\gamma+\rho}$

### Parameters Estimation
To predict the information, we will utilise Markov Chain Monte Carlo to do the parameter estimation. To do so, a number of priors and a likelihood function have been chosen to allow for the MCMC model to work:

#### Priors

- $\beta$ = Inverse Gamma
- $\gamma$ = Inverse Gamma
- $\rho$ = Truncated Normal
- $I_0$ = Poisson

#### Likelihood Function

For the likelihood function, we need to chose an equation that allows MCMC to estimate all the necessary parameters, thanks to this paper, we can write $D(t)$ as such:

$D(t) = I_0(1+k)^{\frac{\beta}{\beta-\gamma}}(1+ke^{(\beta-\gamma)(t-t_0)})^{-\frac{\beta}{\beta-\gamma}}e^{(\beta-\gamma)(t-t_0)}$

Where $k$ is:

$k = \dfrac{I_0}{S_0}$
