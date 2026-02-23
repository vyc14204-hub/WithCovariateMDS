# WithCovariateMDS
A Python library for Covariate-Adjusted Maximum Likelihood Multidimensional Scaling (MDS)

# Covariate-Adjusted Multidimensional Scaling (MDS)

This repository provides a Python implementation of **Covariate-Adjusted Multidimensional Scaling (MDS)**, 
utilizing **Maximum Likelihood Estimation (MLE)** based on the log-linear model framework originally proposed by Ramsay (1977).

While standard MDS estimates psychological or physical distances purely from similarity/dissimilarity data, 
respondents' specific characteristics (e.g., age, specific psychological traits, lie scales) can systematically bias their responses. 

This class allows you to estimate the configuration of items by simultaneously estimating and controlling for these covariate biases 
via Maximum Likelihood, and visually comparing the structural shift before and after the adjustment using Procrustes alignment.

## Features
* **Maximum Likelihood Estimation (MLE):** Optimizes the negative log-likelihood function to estimate configurations and covariate parameters,
* providing a statistical foundation compared to non-metric or simple metric MDS.
*
* **Standard ML-MDS:** Baseline maximum likelihood multidimensional scaling without covariates.
*
* **Covariate-Adjusted ML-MDS:** Simultaneously estimates the item coordinates and the structural bias beta coefficients caused by specified covariates.
*
* **Statistical Inference:** Computes standard errors (via the inverse Hessian matrix), z-values, and p-values
* to test the statistical significance of each covariate's impact on item distances.
*
* **Procrustes Alignment:** Automatically rotates and aligns the adjusted configuration to the baseline for accurate visual comparison.
*
* **Rich Visualizations:** Multiple plotting options to visualize the structural shifts (e.g., overlay plots, movement arrows, no-text clean plots).

## Requirements
* `numpy`
* `pandas`
* `matplotlib`
* `scipy`

Quick Start / Usage
The repository includes an example_usage.py script that demonstrates the full pipeline using synthetic data.

1. Prepare your data
Your data should be a pandas.DataFrame where rows are respondents and columns are the variables (items) to be scaled,
along with any continuous or categorical covariates.

3. Initialize and Fit the ML Model
Import the class and pass your data, the names of the item columns, and the names of the covariate columns.
The fit method will perform the MLE optimization.

import pandas as pd
from WithCovariateMDS import WithCovariateMDS

# Load your data
df = pd.read_csv("dummy_data.csv")

# Specify the columns to be scaled and the covariates
traits = ['item_1', 'item_2', 'item_3', 'item_4', 'item_5', 'item_6']
covariates = ['covariate1', 'covariate2']

# Initialize the model (default is 2 dimensions)
model = WithCovariateMDS(n_dim=2)

# Fit the model using Maximum Likelihood
model.fit(df, trait_cols=traits, covariate_cols=covariates)
