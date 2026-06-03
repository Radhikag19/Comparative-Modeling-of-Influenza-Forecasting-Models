# Influenza Forecasting Across US Regions Using Epidemiological and Time-Series Models

## Project Overview

Influenza remains one of the most significant seasonal infectious diseases, causing recurring outbreaks that place substantial pressure on healthcare systems worldwide. The timing, intensity, and spread of influenza vary across geographic regions due to differences in climate, demographics, healthcare accessibility, mobility patterns, and population behavior.

This project presents a comprehensive influenza forecasting framework that combines epidemiological modeling, statistical forecasting, geospatial analysis, and cross-region transferability assessment using multi-region influenza surveillance data from the United States.

Rather than relying on a single forecasting technique, this study compares multiple modeling families to understand how different approaches perform under varying epidemic conditions.

---

## Problem Statement

Accurate influenza forecasting is essential for:

* Hospital resource planning
* Medicine inventory management
* Early outbreak detection
* Public health intervention strategies
* Vaccination campaign planning

However, influenza forecasting is challenging because surveillance data contains:

* Strong seasonality
* Sudden epidemic peaks
* Regional variability
* Non-linear outbreak behavior
* Year-to-year fluctuations

To address these challenges, this project evaluates and compares multiple forecasting methodologies across different US healthcare regions.

---

# Project Workflow

```text
Raw Influenza Surveillance Data
                │
                ▼
Data Cleaning & Preprocessing
                │
                ▼
Geospatial Analysis
                │
                ▼
Exploratory Data Analysis
                │
                ▼
 ┌─────────────────────────────┐
 │ Epidemiological Models      │
 │ • SIR                       │
 │ • SEIR                      │
 │ • Seasonal SEIR             │
 └─────────────────────────────┘
                │
                ▼
 ┌─────────────────────────────┐
 │ Statistical Forecasting     │
 │ • ARIMA                     │
 │ • SARIMA                    │
 │ • Prophet                   │
 └─────────────────────────────┘
                │
                ▼
Model Disagreement Analysis
                │
                ▼
Cross-Region Transferability
                │
                ▼
Insights & Evaluation
```

---

# Repository Structure

```text
├── Step1_Data_Cleaning_Preprocessing.ipynb
├── Step2_Geospatial_Analysis.ipynb
├── Step3_EDA.ipynb
├── Step4_SIR_SEIR.ipynb
├── Step5_ARIMA.ipynb
├── Step5_SARIMA.ipynb
├── Step6_PROPHET.ipynb
├── Step7_Model_Disagreement.ipynb
├── Step8_Cross_Region.ipynb
└── README.md
```

---

# Methodology

## 1. Data Cleaning & Preprocessing

Utilized weekly Influenza-Like Illness (ILI) surveillance data from multiple US HHS regions (2019–2025), with detailed analysis focused on Region 4, Region 6, and Region 9 due to their diverse geographic and epidemiological characteristics.

The raw influenza surveillance data was transformed into a standardized weekly dataset.

### Tasks Performed

* Missing value handling
* Date normalization
* Region standardization
* Seasonal label generation
* Population integration
* Feature engineering

### Final Dataset Features

| Feature      | Description                  |
| ------------ | ---------------------------- |
| Year         | Observation year             |
| Week         | Epidemiological week         |
| Region       | HHS region                   |
| Season       | Influenza season             |
| Date         | Weekly timestamp             |
| ILI_Total    | Influenza-like illness count |
| Weighted_ILI | Weighted influenza activity  |
| Population   | Regional population          |
| ILI_per_100k | Population-normalized burden |

---

## 2. Geospatial Analysis

Geospatial analysis was conducted using HHS regions across the United States.

### Objectives

* Visualize influenza burden geographically
* Compare regional disease intensity
* Identify spatial hotspots
* Support regional forecasting analysis

### Visualizations

* Choropleth maps
* Regional burden comparison
* Per-capita influenza distribution

---

## 3. Exploratory Data Analysis (EDA)

EDA was performed to understand the temporal dynamics of influenza outbreaks.

### Key Analyses

* Weekly influenza trends
* Seasonal outbreak cycles
* Moving-average smoothing
* Peak intensity comparison
* Regional variability analysis

### Insights

* Strong annual seasonality observed
* Winter outbreaks dominate most seasons
* Significant variation in peak intensity across regions
* Clear evidence supporting seasonal forecasting models

---

# 4. Epidemiological Modeling

## SIR Model

The SIR model divides the population into:

* Susceptible (S)
* Infected (I)
* Recovered (R)

### Purpose

* Model disease transmission dynamics
* Estimate transmission and recovery rates
* Compute reproduction number (R₀)

### Advantages

* Highly interpretable
* Epidemiologically meaningful
* Useful baseline model

### Limitations

* Assumes homogeneous population mixing
* Struggles with abrupt fluctuations

---

## SEIR Model

The SEIR model introduces an additional compartment:

* Exposed (E)

to account for the incubation period before infection becomes infectious.

### Advantages

* More realistic disease dynamics
* Captures latent transmission phase
* Better biological interpretation

---

## Seasonal SEIR

To capture annual influenza seasonality, transmission rates are allowed to vary over time.

### Benefits

* Models winter outbreak amplification
* Captures seasonal epidemic behavior
* Improves realism over standard SEIR

---

# 5. Statistical Forecasting Models

## ARIMA

AutoRegressive Integrated Moving Average

### Strengths

* Captures temporal dependencies
* Effective short-term forecasting
* Strong statistical baseline

### Limitations

* Limited seasonal awareness
* Underperforms on strongly seasonal outbreaks

---

## SARIMA

Seasonal ARIMA extends ARIMA by incorporating seasonal components.

### Why SARIMA?

Influenza exhibits annual recurrence patterns.

### Strengths

* Captures yearly outbreak cycles
* Improved forecast accuracy
* Better seasonal representation

### Observation

SARIMA emerged as one of the strongest forecasting models in this study.

---

## 6. Prophet

Prophet decomposes a time series into:

* Trend
* Seasonality
* Residual effects

### Advantages

* Interpretable forecasting
* Robust seasonal modeling
* Handles trend shifts effectively

---

# 7. Model Disagreement Analysis

Forecasting uncertainty does not arise solely from noisy data.

Different models often produce different future trajectories even when trained on the same historical observations.

This stage compares:

* SIR forecasts
* SEIR forecasts
* ARIMA forecasts
* SARIMA forecasts
* Prophet forecasts

### Goal

Understand how model assumptions influence predictions.

### Key Finding

Mechanistic models generated smoother epidemic curves, while statistical models responded more strongly to recent observations.

---

# 8. Cross-Region Transferability Analysis

A unique aspect of this project is the investigation of whether forecasting knowledge learned in one region can generalize to another.

### Questions Explored

* Can a model trained on Region A perform well in Region B?
* Do influenza dynamics transfer across geographies?
* Which regions exhibit similar epidemic behavior?

### Findings

* Regions with smoother seasonal patterns demonstrated higher transferability.
* Highly volatile regions required region-specific calibration.
* Partial transferability is achievable under compatible epidemic conditions.

---

# Evaluation Metrics

Model performance was evaluated using:

## Root Mean Square Error (RMSE)

Measures the magnitude of forecasting error while penalizing larger mistakes.

## Mean Absolute Error (MAE)

Measures average absolute deviation between predictions and actual observations.

These metrics were used consistently across all forecasting models.

---

# Key Findings

### Epidemiological Models (SIR & SEIR)
* The SIR model served as a useful mechanistic baseline, capturing the broad progression of influenza outbreaks and providing interpretable estimates of disease transmission dynamics.
* Incorporating an exposed compartment through the SEIR framework improved epidemiological realism by accounting for the latent phase of infection.
* While SEIR produced more biologically meaningful outbreak trajectories, the increase in model complexity did not consistently translate into substantially better forecasting performance across all regions.

### Statistical Forecasting Models
* ARIMA provided a reasonable non-seasonal forecasting baseline but struggled to fully capture the strong seasonal patterns present in influenza surveillance data.
* SARIMA generally produced more reliable forecasts by explicitly modeling annual seasonality, demonstrating the importance of seasonal components in influenza prediction.
* Prophet generated competitive forecasts and offered clear decomposition of trend and seasonal effects, making the resulting predictions easier to interpret.
* Comparative Modeling Insights
Different model families exhibited distinct forecasting behaviors, even when trained on the same historical data.

Mechanistic models emphasized disease dynamics and interpretability, whereas statistical models were often more effective at capturing recurring temporal patterns.

The study reinforces the value of evaluating multiple forecasting approaches rather than relying on a single modeling framework.

### Cross-Region Transferability
* Some forecasting structures showed potential for transfer across regions with similar seasonal characteristics and outbreak behavior.
* However, forecasting performance remained sensitive to regional variability, indicating that local calibration is still important for robust predictions.
* These findings suggest that transferability is feasible under certain conditions, but cannot be assumed universally across all regions.

---

# Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* GeoPandas
* SciPy
* Statsmodels
* Prophet
* Scikit-learn

---