# Bayesian Data Analysis for Stroke Prediction

## 🚀 Introduction

[cite_start]This project presents a comprehensive Bayesian data analysis to predict the probability of stroke in patients based on a range of demographic, lifestyle, and clinical factors[cite: 6, 7]. [cite_start]Stroke is a critical medical condition and a leading cause of death and disability worldwide, making early risk identification essential for preventive care[cite: 7, 8]. [cite_start]This analysis leverages a dataset of 5,110 patients to build and compare two distinct Bayesian logistic regression models, aiming to identify the most significant predictors of stroke[cite: 9, 11].

The entire analysis, from data preprocessing and feature selection to model implementation and evaluation, is documented in the accompanying R Markdown notebook and detailed in the project report.

***

## 🎯 Project Goal

[cite_start]The primary objective of this project is to develop a robust Bayesian logistic regression model to predict an individual's stroke risk[cite: 11]. The project focuses on:

1.  **Feature Selection**: Identifying the most statistically significant covariates that influence the probability of stroke.
2.  **Model Comparison**: Building and comparing two distinct models to determine the most effective combination of features for prediction.
3.  **Bayesian Inference**: Using MCMC methods to estimate model parameters and evaluate the model's predictive performance.
4.  **Posterior Predictive Checks**: Assessing the model's fit and its ability to accurately predict outcomes, particularly for the minority class (stroke patients).

***

## 📊 Dataset

[cite_start]The analysis utilizes a healthcare dataset containing information on 5,110 patients, with 12 variables for each individual[cite: 9]. The key features include:

* [cite_start]**Demographics**: Age, gender, marital status, and residence type[cite: 10].
* [cite_start]**Medical History**: Hypertension, heart disease, and smoking status[cite: 10].
* [cite_start]**Occupation**: Type of work (e.g., Private, Self-employed, Govt_job)[cite: 10].
* [cite_start]**Health Indicators**: Average glucose level and Body Mass Index (BMI)[cite: 10].

***

## 🛠️ Methodology

The project follows a structured analytical approach, from data preparation to model evaluation, to ensure the reliability of the findings.

### 1. Data Preprocessing & Feature Engineering

* [cite_start]**Handling Missing Values**: Missing values in the `bmi` column were imputed with the mean to preserve the sample size[cite: 14]. [cite_start]Features with "other" or "unknown" labels were treated as valid categories[cite: 15].
* [cite_start]**Categorical Variable Encoding**: All categorical variables were label-encoded to manage the high dimensionality of the dataset[cite: 16].
* **SMOTE for Class Imbalance**: The dataset exhibited a significant class imbalance, with only 5% of patients having experienced a stroke. [cite_start]To address this, **SMOTE (Synthetic Minority Over-sampling Technique)** was applied to the training data, increasing the proportion of the minority class to create a more balanced dataset for model training[cite: 45, 46].

### 2. Feature Selection

Two distinct models were developed based on different feature selection strategies:

* **Model 1 (Full Model)**: This model includes a comprehensive set of features, with numerical variables like `age`, `bmi`, and `avg_glucose_level` scaled using robust scaling.
* [cite_start]**Model 2 (Reduced Model)**: For this model, numerical variables were first grouped into meaningful categories (e.g., age in 10-year intervals, standard BMI categories)[cite: 30, 31, 32]. A **chi-square test** was then performed to identify and retain only the most statistically significant features. [cite_start]Based on the p-values, `gender` and `Residence_type` were excluded, while `work_type` was kept due to its relevance in previous studies[cite: 33, 34, 43, 44].

### 3. Bayesian Logistic Regression Model

[cite_start]Both models were implemented using a **Bayesian logistic regression** framework in **JAGS (Just Another Gibbs Sampler)**[cite: 51].

* [cite_start]**Likelihood**: The stroke status of each individual was modeled as a Bernoulli random variable[cite: 13, 53].
* [cite_start]**Priors**: Weakly informative normal priors (mean 0, precision 0.01) were assigned to the intercept and all regression coefficients, allowing the data to drive the posterior estimates[cite: 55, 56, 57, 58].
* [cite_start]**MCMC Simulation**: Four independent Markov chains were run for 8,000 iterations each, with the first 1,000 discarded as a burn-in period to ensure convergence[cite: 60, 61].

***

## 📈 Results & Analysis

### 1. Convergence Diagnostics

* [cite_start]**Model 1** demonstrated excellent convergence across all four chains, with both **Geweke** and **Gelman-Rubin** diagnostics confirming stability and an Effective Sample Size (ESS) greater than 1,000[cite: 65, 67, 69, 77].
* [cite_start]**Model 2**, while passing the Gelman-Rubin test, showed poor convergence in two of its chains according to the Geweke diagnostic, suggesting potential biases in the posterior estimates[cite: 70, 73, 78].

### 2. Model Comparison

[cite_start]Model 1 was consistently favored by both the **Deviance Information Criterion (DIC)** and the **Watanabe-Akaike Information Criterion (WAIC)**[cite: 80].

* [cite_start]**DIC**: Model 1 had a lower penalized deviance (3989) compared to Model 2 (4057), indicating a better balance of fit and complexity[cite: 80, 87, 90].
* [cite_start]**WAIC**: Model 1 also achieved a higher expected log pointwise predictive density (-1994.8 vs. -2028.4), confirming its superior predictive performance[cite: 81].

[cite_start]Based on these results, **Model 1 was selected as the superior model** for this analysis[cite: 91].

### 3. Posterior Predictive Checks

The posterior predictive checks for Model 1 revealed:

* [cite_start]A **Bayesian p-value of 0.5054**, suggesting that the model provides a good overall fit to the data[cite: 93, 122].
* [cite_start]However, the model tends to **underestimate the minority class (stroke patients)**, as indicated by the discrepancy between observed and simulated data for Y=1[cite: 94, 97, 99, 122]. [cite_start]This is likely due to the residual class imbalance and overlapping feature distributions, even after applying SMOTE[cite: 98, 123].

***

## 💡 Conclusion

The analysis successfully developed and compared two Bayesian logistic regression models for stroke prediction. [cite_start]**Model 1**, which utilized a broader set of features, demonstrated superior convergence and predictive accuracy, making it the preferred model[cite: 121, 91]. [cite_start]Key predictors such as age and blood pressure were identified as significant factors in stroke risk[cite: 121, 79].

[cite_start]While the chosen model shows a good overall fit, it struggles with accurately predicting the minority class (stroke occurrences)[cite: 122]. [cite_start]Future work should focus on enhancing the model's sensitivity through advanced feature engineering, the use of stronger priors, or exploring alternative modeling approaches to better capture the complexities of stroke prediction[cite: 124, 125].

***
