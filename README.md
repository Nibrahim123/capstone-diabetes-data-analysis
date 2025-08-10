# ![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)

# Diabetes Health Indicators Analysis

## Overview

This project analyses the 2015 Behavioral Risk Factor Surveillance System (BRFSS) Diabetes Health Indicators dataset from Kaggle to identify key patterns and risk factors for diabetes.

The objective is to generate actionable public health insights and build predictive models that can classify individuals’ diabetes risk based on health and lifestyle variables.

The work follows the full data analytics pipeline: Extract, Transform, Load (ETL) → Feature Engineering → Exploratory Data Analysis (EDA) → Hypothesis Testing → Machine Learning (ML) → Tableau Dashboard → Ethics & Governance.

## Dataset Content
The dataset used is the 2015 Behavioral Risk Factor Surveillance System (BRFSS) Diabetes Health Indicators from Kaggle. It contains health and lifestyle survey data from over 250,000 respondents, including variables such as BMI, smoking status, physical activity, general health, mental health, and income.

This project uses:

Full ML-ready dataset (combined_ml_ready.csv) — tracked using Git LFS due to size.

Sample ML-ready dataset (combined_ml_ready_sample.csv) — created for testing and GitHub preview.

Cleaned dataset (combined_cleaned_final.csv) — contains human-readable feature names and values, with no missing data, and is fully suitable for hypothesis testing and EDA.

Raw data is anonymised, publicly available, and licensed for research purposes.

## Business Requirements
The primary business requirement is to identify the most significant health and lifestyle factors associated with diabetes to help public health analysts and policymakers develop targeted prevention strategies.

Specifically, this project aims to:

Explore relationships between health indicators (BMI, smoking, physical activity, general health, etc.) and diabetes prevalence.

Statistically validate whether these relationships are significant.

Build a predictive model to estimate diabetes risk based on health indicators.

Present results in an interactive Tableau dashboard for both technical and non-technical audiences.

## Hypothesis and How to Validate Them
(To be completed after EDA stage)

## Project Plan

High-level Steps Taken so Far:

1- ETL

Imported raw BRFSS datasets from Kaggle.

Merged and cleaned data, removed duplicates, and standardised column names.

Checked for missing values and confirmed dataset completeness.

Saved cleaned output as combined_cleaned_final.csv — this file contains human-readable features and is ready for hypothesis testing and EDA.

2- Feature Engineering

Encoded categorical features using One-Hot and Label Encoding.

Scaled numerical features for machine learning.

Created a data dictionary for all processed features.

Saved ML-ready datasets:

combined_ml_ready.csv (full version)

combined_ml_ready_sample.csv (small preview version for GitHub)

## Data Management Practices:
Large datasets tracked with Git LFS.

Version-controlled outputs at each stage (cleaned, ml_ready, sample).

Documented transformations for reproducibility.

## Methodology Rationale:
Selected survey-based dataset for public health relevance.

Used encoding and scaling to prepare data for classification models.

Generated a sample dataset to support reproducibility and reduce repository size.

## The Rationale to Map the Business Requirements to the Data Visualisations
(To be completed after EDA & Tableau dashboard design)

## Analysis Techniques Used
Completed:
* Data Cleaning: Removed duplicates, standardised column names, ensured consistent data types.

* Feature Engineering: Encoding categorical variables, scaling numeric features.

* Preliminary ML Testing: Logistic Regression for initial accuracy benchmark.

Limitations:
* Class imbalance (non-diabetic vs diabetic respondents).

* Dataset from 2015 — potential limitations in real-world application today.

AI Tools:
* Used AI assistance to generate code explanations, improve markdown documentation, and plan project structure.

# Ethical Considerations
(To be completed — will include privacy, bias, and governance considerations)

# Dashboard Design
(To be completed after Tableau dashboard is built)

# Unfixed Bugs
(To be completed — will include any unresolved code issues or dashboard display limitations)

# Development Roadmap
1- Perform EDA in Python and export summary tables for Tableau.

2- Define and test hypotheses statistically.

3- Train and evaluate multiple ML classification models.

4- Build Tableau dashboards with ≥4 chart types answering business requirements.

5- Document ethics and governance considerations.

6- Finalise README with all completed sections.

# Deployment
This project does not use Heroku as the final dashboard will be built in Tableau Public. Deployment instructions will instead cover publishing to Tableau Public.

# Main Data Analysis Libraries
These were the primary tools used for data cleaning, transformation, analysis, and modelling:

* pandas — Data loading, cleaning, transformation, and manipulation.

* numpy — Numerical operations and array manipulation.

* matplotlib — Static visualisations for EDA and results presentation.

* seaborn — Statistical visualisations such as correlation heatmaps and boxplots.

* scikit-learn — Feature encoding, scaling, model training, and evaluation.

* plotly (planned for EDA) — Interactive visualisations for deeper exploration.

* Tableau Public (planned for final stage) — Interactive dashboard creation and presentation of insights.

# Additional Libraries Used
These supported project setup, file management, and workflow:

os — For file path handling and directory operations.

# Credits

Content:

* Dataset: Kaggle – Diabetes Health Indicators- https://www.kaggle.com/datasets/alexteboul/diabetes-health-indicators-dataset

* Code Institute tutor guidance

* AI assistance:

1- ChatGPT — for project planning, code explanation, documentation drafting, and workflow structuring.

2- GitHub Copilot — for code suggestions, code refinement, optimisation, and syntax completion during development.

# Media:

All visuals created in Python or Tableau during project development.

# Acknowledgements:
Special thanks to tutors, peers, and Code Institute resources for feedback and support.

