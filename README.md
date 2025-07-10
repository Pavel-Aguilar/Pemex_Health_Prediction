# Predictive Analysis of Chronic Disease Morbidity

## Project Overview
This project presents a comprehensive analysis of morbidity data from Petróleos Mexicanos (PEMEX), sourced from official public records spanning from 2016 to the first quarter of 2025. The primary objective is to develop a dual-pronged analytical framework:

  1. Explanatory Analysis: To identify the key pathological drivers and conditions that most       significantly influence the incidence of chronic diseases within the population.
  
  2. Predictive Forecasting: To accurately forecast the volume of chronic disease cases for the       next two years (8 quarters), providing valuable insights for resource planning and               preventive healthcare strategies.

The final results are consolidated and presented in a 3-page interactive Power BI dashboard, offering a clear and accessible overview of historical trends, key drivers, and future forecasts.

## Methodology
The project was executed in two major phases, leveraging distinct datasets and modeling techniques to address the core objectives.

### Part 1: Explanatory Modeling with LightGBM & SHAP
This phase focused on understanding the "why" behind chronic disease cases using annual data from 2016 to 2022.

  ### Data Preprocessing & Feature Engineering:
  
  The raw data was systematically cleaned to remove non-relevant information such as headers,      totals, and descriptive text.
  
  Age-based columns were consolidated into 8 distinct demographic groups (e.g., 0-15_F, 60+_M)     to create meaningful segments for analysis.
  
  A target variable, cronicas, was engineered by aggregating a curated list of relevant chronic    diseases.
  
  Padecimientos considered fortuitous (e.g., dog bites) or irrelevant were discarded, while        pathologies with known correlations to chronic conditions were retained as features.
  
  ### Modeling and Interpretation:
  
  A LightGBM Regressor model was trained to predict the cronicas target variable. The model's      hyperparameters were optimized using RandomizedSearchCV.
  
  The model was rigorously validated through learning curves, validation curves, and residual      analysis to ensure robustness and prevent overfitting.
  
  SHAP (SHapley Additive exPlanations) was employed to interpret the "black box" model,            providing clear, quantitative insights into which features had the most significant impact on    predicting chronic diseases. The analysis revealed that conditions indicating general frailty,   such as malnutrition and pneumonia, were surprisingly strong predictors.

### Part 2: Time Series Forecasting with Prophet
This phase focused on predicting future trends using a consistent, quarterly time series.

  ### Temporal Disaggregation:

  A challenge was the differing granularity of the data: annual from 2016-2022 and quarterly       from 2023-2025.

  To create a unified time series, a temporal disaggregation process was implemented. The real     seasonal patterns observed in the 2023-2024 quarterly data were used as a reference to           intelligently break down the annual totals from 2016-2022 into quarterly estimates.

  This resulted in a single, consistent dataset (pemex_trimestres_all.csv) with a quarterly        frequency from 2016 to Q1 2025, suitable for time series modeling.

  ### Model Selection and Optimization:
  
  Both SARIMA and Prophet models were initially tested with baseline parameters. Prophet           demonstrated superior performance and stability on this dataset.
  
  A grid search was performed to find the optimal hyperparameters for Prophet for each of the 8    demographic groups, tuning parameters like changepoint_prior_scale, seasonality_prior_scale,     and seasonality_mode.

  ### Forecasting:
  
  With the optimized parameters, a final Prophet model was trained for each demographic group.
  
  A forecast was generated for the next 8 quarters (2025-Q2 to 2027-Q1), complete with             prediction intervals to quantify uncertainty.

# Deliverables

  1. Explanatory Insights: The LightGBM and SHAP analysis identified the top predictors for       chronic disease incidence, providing a clear hierarchy of influential factors.
  
  2. Time Series Forecast: A robust 2-year forecast for chronic disease cases for 8 distinct       demographic groups, visualized through a master chart and individual component plots (trend      and seasonality).
  
  3. Interactive Power BI Dashboard: A comprehensive 3-page dashboard that serves as the primary   deliverable for this project. It includes:
  
  Page 1: Historical Analysis: An interactive view of the historical data.

  Page 2: Predictive Drivers: A visualization of the feature importances from the LightGBM model.

  Page 3: Future Forecast: An interactive chart displaying the Prophet forecast for the next two   years.
  
  -The dashboard file (.pbix) and screenshots are available in this repository.

Exported Data: The key data artifacts, including feature importances (importancias_lightgbm.csv) and the final forecast (pronostico_prophet.csv), have been exported for use in the dashboard and for further analysis.
