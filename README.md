# Predicting PFOA Contamination in Groundwater Wells — A Machine Learning Approach

## Overview
This project investigates PFOA (perfluorooctanoic acid) contamination in groundwater 
wells across 32 U.S. states using a socioeconomic and environmental machine learning 
framework. The goal was to identify the best-performing classification model to predict 
whether a groundwater well tests positive for PFOA contamination, and to surface the 
key environmental, geographic, and demographic factors driving that risk.

## Research Question
**Can we predict PFOA contamination in groundwater wells using environmental, 
hydrological, and socioeconomic predictors — and which machine learning model 
does it best?**

## Data Sources
- **EPA groundwater well records** — PFOA concentration values and well characteristics
- **U.S. Census Bureau ACS (2019–2022)** — socioeconomic indicators by state 
  (income, poverty, race, education, population density)
- **Cancer incidence data** — average annual cancer rates by state
- **USGS/Tigris** — state-level geographic coordinates (latitude/longitude centroids)

## Project Files
| File | Description |
|------|-------------|
| `Pfoa_Cleaning.Rmd` | Full data pipeline: loading, merging, cleaning, feature engineering, and export |
| `Models.Rmd` | Exploratory analysis, correlation matrix, and all machine learning models |
| `final_data_clean.csv` | Final cleaned and merged dataset ready for modeling |
| `PFAS_project_proposal.pptx` | Project presentation with findings and recommendations |

## Methodology

### Data Preparation (`Pfoa_Cleaning.Rmd`)
- Merged EPA environmental records with groundwater well data on `WELL_ID`
- Integrated U.S. Census ACS socioeconomic variables (2019–2022) by state and year
- Added state-level cancer incidence rates; imputed missing Indiana values with mean
- Extracted geographic centroids (latitude/longitude) using `tigris` and `sf`
- Engineered binary target variable `pfoa_detected` (1 = detected at or above 
  laboratory reporting limit, 0 = not detected)
- Handled placeholders, type conversions, missing values, and unused factor levels
- Final dataset: **22 predictors** across environmental, hydrological, 
  socioeconomic, and geographic domains

### Key Predictors
- **Hydrological:** well depth, tritium concentration, tritium category, water use type
- **Socioeconomic:** median income, poverty rate, unemployment rate, racial composition, 
  education level, population density
- **Geographic:** state, latitude, longitude
- **Health:** cancer rate
- **Temporal:** month, year

### Models Compared (`Models.Rmd`)
| Model | Notes |
|-------|-------|
| Linear Regression | Baseline on log-transformed PFOA values; stepwise selection applied |
| Logistic Regression | Standard and regularized (Elastic Net via `glmnet`) to handle separation |
| XGBoost | Gradient boosting with SHAP values for interpretability |
| Random Forest | Primary classification model; run on both imbalanced and ROSE-balanced data |

## Key Results
- Corrected 95% of data errors across 15,000+ records before modeling
- Identified **tritium concentration, well depth, state, and cancer rate** 
  as top predictors of PFOA detection
- Applied **ROSE oversampling** to address class imbalance in the training data
- Used **SHAP values** to interpret XGBoost feature directions
- Recommendations prioritized **3 sites for immediate remediation** and 
  **5 for long-term aquifer monitoring**
- Awarded **3rd Place at the FEDITC National Competition, UTSA (2025)**

## Tools & Technologies
- **Language:** R
- **Libraries:** `randomForest`, `xgboost`, `glmnet`, `caret`, `pROC`, `ROSE`, 
  `SHAPforxgboost`, `tidycensus`, `tigris`, `sf`, `ggplot2`, `corrplot`, `gt`
- **Methods:** Binary classification, log transformation, elastic net regularization, 
  ROSE balancing, SHAP interpretation, correlation analysis, stepwise regression

## Author
Doris Mbitazi Asongafac
[linkedin.com/in/doris-asongafac](https://linkedin.com/in/doris-asongafac) | 
[rpubs.com/DorisAsongafac](https://rpubs.com/DorisAsongafac)
