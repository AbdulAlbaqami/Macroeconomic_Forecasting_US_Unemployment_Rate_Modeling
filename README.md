# Macroeconomic Forecasting: US Unemployment Rate Modeling

## Executive Summary

This project forecasts the monthly U.S. unemployment rate by evaluating the predictive power of key macroeconomic indicators. By transitioning from baseline seasonal models to a Lagged SARIMAX framework, the analysis identifies delayed economic effects that drive labor market dynamics. The final model utilizes optimal lags for Initial Jobless Claims (1-month), Federal Funds Rate (12-month), and Industrial Production (6-month), reducing forecast error (RMSE) from 0.18 to 0.07.

## Project Structure

The repository is organized into a clean, modular structure for reproducibility:

unemployment-forecasting/
├── Data/                           # Raw CSV datasets from FRED
├── Notebooks/                      # Core analysis and modeling
│   ├── EDA.ipynb                   # Exploratory data analysis and stationarity testing
│   └── TS_Modeling_Final.ipynb     # Model selection and evaluation
├── .gitignore                      # Prevents pushing .venv and temporary files
└── README.md                       # Project documentation

## Methodology
The modeling strategy followed a systematic progression of increasing complexity:
* Exploratory Data Analysis: Conducted stationarity checks and identified a strong seasonal structure at lag 12.  
* Univariate Baselines: Established naive benchmarks and a SARIMA(1,0,0)(1,0,0,12) model to capture seasonal persistence.  
* SARIMAX Integration: Incorporated contemporaneous macroeconomic predictors—Initial Jobless Claims (ICSA), Federal Funds Rate (FEDFUNDS), and Industrial Production (INDPRO)—to leverage broader labor market conditions.  
* Lagged Effect Optimization: Tested various lag combinations to account for the delayed impact of monetary policy and industrial activity on employment.  
* Robustness Testing: Evaluated the impact of a COVID-19 dummy variable to determine if explicit shock modeling improved forecast accuracy over standard macroeconomic predictors.
  
## Key Results
The Lagged SARIMAX model outperformed all other specifications by capturing the gradual adjustment of the labor market to economic shifts.

Model | MAE | RMSE | MAPE
| :--- | :---: | :---: | :---: |
Naive | 0.233 | 0.292 | 5.63%
Seasonal Naive | 0.250| 0.277 | 5.92%
SARIMA | 0.157 | 0.178 | 3.64%
SARIMAX (Contemporaneous) | 0.077 | 0.086 | 1.79%
SARIMAX (Optimal Lags) | 0.047 | 0.068 | 1.10%

## Major Insight: The "COVID Effect"

The analysis found that adding a COVID-period dummy variable actually decreased forecast accuracy. This indicates that the chosen macroeconomic predictors already captured the pandemic-induced volatility, making additional binary indicators redundant.

## Technical Stack

*    Language: Python

*   Libraries: Pandas, NumPy, Statsmodels (SARIMAX), Scikit-learn (Metrics), Matplotlib, Seaborn   

*    Data Source: Federal Reserve Economic Data (FRED)

## Installation & Usage 
1- Clone the repository
2- Create and activate a virtual environment
3- Install dependencies
4- Run the Notebooks/TS_Modeling_Final.ipynb file to reproduce the analysis

