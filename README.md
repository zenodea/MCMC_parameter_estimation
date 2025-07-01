# COVID-19 MCMC Analysis
Analysing Government Policies on reproduction of COVID-19 via Parameter Estimation Methods

## Overview
This project analyzes the effectiveness of government policies on COVID-19 transmission using epidemiological modeling and Markov Chain Monte Carlo (MCMC) parameter estimation methods. The analysis covers multiple European countries and examines how lockdown policies affected disease spread patterns.

## Project Structure
```
├── notebooks/               # Jupyter notebooks for analysis
│   ├── MCMC_analysis.ipynb             # Main MCMC analysis
│   ├── MCMC_parameter_evaluation.ipynb  # Parameter evaluation
│   ├── MCMC_sird_evaluation.ipynb      # SIRD model evaluation
│   ├── extended_objective_evaluation.ipynb # Extended analysis
│   ├── realData_analysis.ipynb         # Real data analysis
│   └── [country].ipynb                 # Country-specific data preparation
├── data/                    # Data files
│   ├── raw_data/           # Original datasets
│   └── processed_data/     # Cleaned and processed data
├── results/                 # Analysis outputs
│   ├── result_graphs/      # Generated plots and visualizations
│   └── mcmc_data/         # MCMC analysis results by country
└── README.md               # This file
```

## Methodology
A slightly modified version of the epidemiological SIR model is utilised, the SIRD model. This model splits the Removed compartment into: Removed (Alive) and Dead. This is useful to us since deaths recorded is one of the more common data available to us.

### SIRD Model Equations

$\dfrac{dS}{dt} = -\dfrac{\beta I S}{N}$

$\dfrac{dI}{dt} = \dfrac{\beta I S}{N} - \gamma I - \rho I$

$\dfrac{dR}{dt} = \gamma I$ 

$\dfrac{dD}{dt} = \rho I $

Using ordinary differential equation integration, we can write the following SIRD model in python:
```python
def deriv(y, t, N, beta, gamma, rho):
    S, I, R, D = y
    dSdt = -(beta * S * I) / N
    dIdt = (beta * S * I / N) - (gamma * I) - (rho * I)
    dRdt = gamma * I
    dDdt = rho * I
    return dSdt, dIdt, dRdt, dDdt
```

### Model Parameters
The model estimates the following key parameters:

- $\beta$ = Infection Rate (transmission rate)
- $\gamma$ = Recovery Rate
- $\rho$ = Death Rate
- $I_0$ = Initial number of infected individuals

The basic reproduction number is calculated as:
- $R_0 = \frac{\beta}{\gamma+\rho}$

### Parameter Estimation with MCMC
Markov Chain Monte Carlo is used for Bayesian parameter estimation with the following priors:

#### Prior Distributions
- $\beta$ ~ Inverse Gamma
- $\gamma$ ~ Inverse Gamma  
- $\rho$ ~ Truncated Normal
- $I_0$ ~ Poisson

#### Likelihood Function
The likelihood function for cumulative deaths over time is given by:

$D(t) = I_0(1+k)^{\frac{\beta}{\beta-\gamma}}(1+ke^{(\beta-\gamma)(t-t_0)})^{-\frac{\beta}{\beta-\gamma}}e^{(\beta-\gamma)(t-t_0)}$

Where: $k = \dfrac{I_0}{S_0}$

## Countries Analyzed
- France
- Germany  
- Italy
- Netherlands
- Spain
- Sweden
- Switzerland
- United Kingdom

## Key Features
- **Policy Impact Analysis**: Comparison of transmission rates before and after lockdown implementations
- **Bayesian Parameter Estimation**: Robust parameter estimation using MCMC methods
- **Cross-Country Comparison**: Analysis across multiple European countries
- **Uncertainty Quantification**: Credible intervals for all estimated parameters
- **Model Validation**: Posterior predictive checks and convergence diagnostics

## Requirements
- Python 3.x
- Jupyter Notebook
- NumPy
- Pandas
- Matplotlib/Seaborn
- PyMC3/PyMC4
- SciPy
- ArviZ (for MCMC diagnostics)

## Usage
1. Start with country-specific data preparation notebooks in `notebooks/`
2. Run the main MCMC analysis using `notebooks/MCMC_analysis.ipynb`
3. Evaluate results using the parameter evaluation notebooks
4. View generated plots and results in the `results/` directory

## Results
The analysis generates:
- Parameter posterior distributions
- Convergence diagnostics (trace plots, R-hat statistics)
- Posterior predictive checks
- Comparative analysis across countries and time periods
- Visualization of policy impact on transmission dynamics
