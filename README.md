# WithCovariateMDS
A Python library for Covariate-Adjusted Maximum Likelihood Multidimensional Scaling (MDS)

　This repository provides a Python implementation of Covariate-Adjusted Multidimensional Scaling (MDS), 
utilizing Maximum Likelihood Estimation (MLE) based on the log-linear model framework originally proposed by Ramsay (1977).

　This ML-based approach allows for statistical inference. Furthermore, while standard MDS estimates 
psychological or physical distances purely from similarity/dissimilarity data,
respondents' specific characteristics (e.g., age, specific psychological traits, lie scales) can systematically bias their responses.
This class allows you to estimate the configuration of items by simultaneously estimating and controlling 
for these covariate biases via Maximum Likelihood, and visually comparing the structural shift before and 
after the adjustment using Procrustes alignment.

Features
　Maximum Likelihood Estimation (MLE): Optimizes the negative log-likelihood function to estimate configurations
and covariate parameters, providing a statistical foundation.

Standard ML-MDS: Baseline maximum likelihood multidimensional scaling without covariates.

Covariate-Adjusted ML-MDS: Simultaneously estimates the item coordinates and the structural bias beta　coefficients
　caused by specified covariates.
 
Statistical Inference: Computes standard errors (via the inverse Hessian matrix), z-values, and p-values to test the statistical 
 significance of each covariate's impact on item distances.

Procrustes Alignment: Automatically rotates and aligns the adjusted configuration to the baseline for accurate visual comparison.

Visualizations: Multiple plotting options to visualize the structural shifts (e.g., overlay plots, movement arrows).

Requirements
 numpy
 pandas
 matplotlib
 scipy

 
Quick Start / UsageThe repository
 includes an example_usage.py script that demonstrates the full pipeline using synthetic data.
 
 Prepare your dataYour data should be a pandas.DataFrame where rows are respondents and columns are the variables (items) to be scaled, 
along with any continuous or categorical covariates. Initialize and Fit the ML ModelImport the class and pass your data, 
the names of the item columns, and the names of the covariate columns. The fit method will perform the MLE optimization.

     
 import pandas as pd
 
 from WithCovariateMDS import WithCovariateMDS
 
 df = pd.read_csv("dummy_data.csv")

 Pythontraits = ['item_1', 'item_2', 'item_3', 'item_4', 'item_5', 'item_6']
 
 covariates = ['covariate1', 'covariate2']

 model = WithCovariateMDS(n_dim=2)
 
 model.fit(df, trait_cols=traits, covariate_cols=covariates)

 model.summary()

 model.plot_standard()
 
 model.plot_covariate()
 
 model.plot_overlay()
 
 model.plot_overlay_with_arrows()
 
 model.plot_overlay_arrows_no_text()
 
 model.plot_overlay_no_text_no_arrow()

