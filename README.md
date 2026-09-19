# Biomass Prediction using Machine Learning (Regression)

This repository contains the R scripts and datasets developed for the final project of the Machine Learning course (Aprendizado de Máquina), part of the Applied Artificial Intelligence Specialization at the Federal University of Paraná (UFPR).

## Project Overview

The objective of this project is to perform a regression task to predict **Biomass** using various machine learning algorithms. Following the guidelines from the final assignment, multiple models were trained and evaluated to determine the best approach based on standard regression metrics.

Both Hold-Out and K-Fold Cross-Validation (CV) strategies were applied to ensure model robustness. A fixed random seed (`202650`) was used across all scripts to guarantee reproducibility, as required by the assignment specifications.

## Models Implemented

The predictive modeling was built using the `caret` package in R. The following algorithms were tested:

* **K-Nearest Neighbors (KNN):** Tuned over a grid of K values.
* **Random Forest (RF):** Implemented with both Hold-Out and 10-fold Cross-Validation, tuning the `mtry` parameter.
* **Artificial Neural Networks (ANN/RNA):** Implemented with both Hold-Out and 10-fold Cross-Validation, tuning the `size` (hidden units) and `decay` (weight decay) parameters.
* **Support Vector Machines (SVM):** Implemented using a Radial Basis Function (RBF) kernel with Hold-Out and 10-fold Cross-Validation, tuning the Cost (`C`) and `sigma` parameters.

## Evaluation Metrics

To rank and compare the models, the scripts calculate the following metrics on the test set:

* **R^2 (Coefficient of Determination):** Primary metric used to order model performance.
* **Syx (Standard Error of the Estimate):** Calculated with 1 degree of freedom.
* **Pearson Correlation (r):** Measures the linear correlation between observed and predicted values.
* **RMSE (Root Mean Square Error):** Measures the average magnitude of the errors.
* **MAE (Mean Absolute Error):** Measures the average absolute errors.

## Results and Conclusion

After evaluating all models on the test set, the models were ranked based on the `$R^2$` metric. The best performing technique was the **Artificial Neural Network with Cross-Validation (RNA - CV)**.

By utilizing a tuning grid to optimize the hyperparameters, the best configuration was found to be:
* **Size (hidden neurons):** 10
* **Decay:** 0.4

This specific RNA model achieved the highest `$R^2$` of **0.9736** and a Pearson correlation of **0.9867**. It also yielded the lowest error metrics among all tested models (RMSE = 224.3876, MAE = 96.3992). 

For comparison, the second-best model was the Random Forest with Cross-Validation (`mtry = 2`), which achieved an `$R^2$` of 0.9664.

### New Cases Prediction

As required by the assignment, the best model (RNA - CV) was used to predict the biomass for three new, unobserved cases (`novos_casos_biomassa.csv`). The model successfully outputted the estimated biomass values (e.g., 36.48, 71.31, and 633.26) based on the input features (`dap`, `h`, `Me`), demonstrating its practical applicability.

## Repository Structure

```
.
├── 5 - Biomassa - Dados.csv         # Original dataset used for training and testing
├── novos_casos_biomassa.csv         # Unseen data for prediction using the best model
├── Biomassa KNN.R                   # KNN training and evaluation script
├── Biomassa RF - CV.R               # Random Forest with Cross-Validation
├── Biomassa RF - Hold Out.R         # Random Forest with Hold-Out validation
├── Biomassa RNA - CV.R              # Neural Network with Cross-Validation
├── Biomassa RNA - Hold Out.R        # Neural Network with Hold-Out validation
├── Biomassa SVM - CV.R              # SVM with Cross-Validation
├── Biomassa SVM - Hold Out.R        # SVM with Hold-Out validation
└── APM-Trabalho Final (1).pdf       # Original assignment specifications
```

## Usage Instructions

### Prerequisites

To run the scripts, you will need R installed along with the following packages:

```R
install.packages(c("caret", "Metrics", "e1071", "kernlab", "mlbench", "mice", "randomForest", "nnet"))
```

### Running the Scripts

1. Clone this repository to your local machine.
2. Open RStudio or your preferred R environment.
3. Update the `setwd()` path in the chosen script to match your local directory where the dataset is stored.
4. Run the script. Each script will automatically split the data (80% training, 20% testing), train the model, predict on the test set, and output a data frame with the final calculated metrics.
