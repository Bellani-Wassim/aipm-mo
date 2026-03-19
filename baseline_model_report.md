# Model Performance Report: Baseline Prediction Algorithm

## 1. Executive Summary
This report outlines the configuration and initial performance metrics for the Minimum Viable Product (MVP) of the Air Quality Prediction Model. Our goal was to establish a fully functional, end-to-end data pipeline and a working baseline algorithm to predict PM2.5 levels.

## 2. Dataset Overview
We utilized a subset of the Seoul Air Quality dataset, focusing exclusively on the year 2021 to ensure relevance and manageability for the baseline phase.
* **Initial Raw Data (2021):** 213,414 records
* **Cleaned Data (Post-NaN removal & Noise Handling):** 208,779 records
* **Data Split (80/20):**
  * Training Set: 167,023 records
  * Testing Set: 41,756 records
* **Selected Features (Predictors):** SO2, NO2, CO, O3, PM10
* **Target Variable:** PM2.5

## 3. Model Configuration
* **Algorithm:** Random Forest Regressor
* **Hyperparameters:** `n_estimators=100` (100 decision trees), `random_state=42`
* **Preprocessing:** `StandardScaler` applied to normalize all pollutant concentrations prior to training.

## 4. Performance Metrics
The baseline model was evaluated against the unseen 20% testing data. 
* **R-squared ($R^2$): 0.8671** (The model successfully explains ~86.7% of the variance in PM2.5 levels, indicating a strong predictive capability for an initial baseline).
* **Mean Squared Error (MSE): 40.48** (Standard error metric required for academic benchmarking).
* **Mean Absolute Percentage Error (MAPE): 34.09%** (Average percentage by which the predictions deviate from the actual PM2.5 values).

## 5. Hyperparameter Optimization & Cross-Validation
To ensure the model's stability and improve its predictive power, we performed systematic hyperparameter tuning using cross-validation.
* **Optimal Configuration:** By restricting the maximum depth to 15 and increasing the forest size to 250 trees, we achieved our highest performance.
* **Optimized R-squared ($R^2$): 0.8812**.
* **Diminishing Returns:** Increasing the number of trees to 500 yielded only a marginal improvement (less than 0.0001 in $R^2$) while doubling the cross-validation time to 9 minutes, indicating that further increasing the model size does not provide a significant benefit relative to the increased computational cost.
* **Impact of Complexity:** Experiments with a higher depth (30 or unlimited) resulted in a regression of the $R^2$ score toward baseline levels and sharply increased computational time to approximately 17 minutes. These results indicate that excessive depth leads to overfitting, where the model captures noise rather than generalizable patterns.

## 6. Conclusion
The configuration consisting of 250 trees and a maximum depth of 15 was selected as the final baseline model. It offers the most efficient architecture while maintaining peak accuracy for our air quality predictions. 

In future sprints, the hybrid CNN-LSTM architecture will be rigorously evaluated against this highly robust Random Forest benchmark to quantify the specific improvements provided by the deep learning approach.
