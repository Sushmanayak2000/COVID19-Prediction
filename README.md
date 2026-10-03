# COVID-19 Forecasting: Deaths, Cases & Hospitalizations

A time-series forecasting project for predicting COVID-19 outcomes across **Bavaria, Germany, Italy, and the United Kingdom** using lagged epidemiological, clinical, policy, and vaccination-related features.

## Project Overview

The project focuses on forecasting COVID-19 outcomes for **January 2022** while simulating a realistic surveillance setting.

A key design constraint was the **14-day lag rule**:

> All predictive features are lagged by at least 14 days to avoid using future information.

This constraint was used to reduce data leakage and reflect the delay between observed health indicators and operational decision-making.

## Regions

- Bavaria (Bayern), Germany
- Germany (national level)
- Italy
- United Kingdom

## Forecasting Strategy

The project uses chronological time splits rather than random shuffling:

- **Training:** 2020 – October 31, 2021
- **Validation:** November 1 – December 31, 2021
- **Test:** January 1 – January 31, 2022

### Evaluation Metric

The primary evaluation metric is:

- **Mean Absolute Error (MAE)**

MAE measures the average absolute difference between predicted and actual values.

## Feature Engineering

The forecasting pipelines use region-specific feature engineering, including:

- Lagged target and predictor variables
- Rolling averages and statistics
- Growth rates and acceleration features
- Clinical ratios
- ICU and hospitalization indicators
- Vaccination-related features
- Policy stringency indicators
- Exponential/log-space transformations
- Momentum and EMA-based indicators for the UK analysis

## Models

Baseline and machine-learning approaches were compared, including:

- Linear Regression
- Ridge Regression
- Lasso Regression
- Random Forest
- Gradient Boosting
- XGBoost
- LightGBM
- Persistence / Naive forecasting

The UK pipeline additionally uses an ensemble strategy combining multiple XGBoost models with validation-based weighting.

## Regional Analysis

### Bavaria

Forecasting targets include:

- Deaths (`Todesfaelle`)
- 7-day hospitalization cases (`7T_Hospitalisierung_Faelle`)

The Bavaria analysis compares baseline models with multiple machine-learning approaches using lagged deaths, cases, ICU-related variables, rolling statistics, and clinical ratios.

### Germany

The Germany pipeline forecasts:

- Daily deaths
- Daily cases

It uses smoothed targets, log-space features, growth dynamics, policy indicators, ICU/hospitalization variables, and vaccination-related features.

### Italy

The Italy analysis forecasts:

- Daily deaths
- Daily cases

Additional features include ICU occupancy, test positivity, vaccination and booster coverage, and robust scaling.

### United Kingdom

The UK pipeline forecasts:

- Daily deaths
- Daily cases

It includes advanced temporal features such as:

- Second-order acceleration
- EMA crossovers
- Rolling slopes
- Log-space transformations
- Multi-seed XGBoost ensemble modeling

## Key Findings

The project compares model behavior across different epidemiological conditions.

Important observations from the analysis include:

- Structural changes such as the transition from Delta to Omicron can reduce the reliability of historical relationships.
- Lagged target variables are consistently important predictors.
- ICU and hospitalization indicators can provide useful information for death forecasting.
- Exponential case growth can require models capable of extrapolating beyond historical ranges.
- Ensemble approaches can be useful under high volatility.
- Model selection depends on the characteristics of the forecasting problem rather than one universally optimal algorithm.

## Limitations

The project has several limitations:

- Variant transitions can create structural breaks.
- Some healthcare-system variables were unavailable.
- Variant prevalence and age-specific vaccination information were not fully incorporated.
- The forecasts are point predictions and do not provide uncertainty intervals.

## Future Improvements

Potential extensions include:

- Probabilistic forecasting and uncertainty intervals
- Regime-detection and automatic model switching
- Additional healthcare-capacity features
- Real-time variant surveillance data
- Quantile regression or Bayesian forecasting approaches

### How to Run
1. Clone the repository
git clone <your-github-repository-url>
cd COVID19-Prediction

2. Install dependencies
pip install -r requirements.txt

3. Run the notebooks
Open the notebooks in Jupyter Notebook or VS Code and run them in this order:
1. Bayern_14day_lags_new.ipynb
2. Germany_14day_lags.ipynb
3. Italy_14day_lags.ipynb
4. UK_14day_lags.ipynb
The notebooks use the datasets stored in the data/ directory.

Notes
The project uses chronological validation and a minimum 14-day feature lag to make the forecasting setup more representative of real-world prediction under reporting delays.