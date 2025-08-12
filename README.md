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

## User Stories

### Story 1 — Amelia, Public Health Analyst
**As** Amelia (Public Health Analyst), **I want** to see how diabetes prevalence varies by age and BMI, **so that** I can target prevention programmes to the highest-risk groups.

**Acceptance criteria**
- **Given** the dashboard is open, **when** I select an **Age** group, **then** I see **diabetes prevalence (%)** update for that group.
- **Given** the **BMI vs Diabetes** chart, **when** I compare diabetics vs non-diabetics, **then** I can see a **clear difference in median and spread** (boxplot line/whiskers + tooltip).
- **Given** a **Sex** filter, **when** I apply it, **then** both visuals update with correct counts and percentages.

**Mapped visual(s):**  
- **Bar chart:** Age vs Diabetes Prevalence (%)  
- **Boxplot:** BMI by Diabetes status (No/Yes)  

**Mapped data:** `data/combined_cleaned_final.csv`


### Story 2 — Ravi, Policy Planner
**As** Ravi (Policy Planner), **I want** to understand how modifiable behaviours relate to diabetes (physical activity, smoking, high blood pressure), **so that** I can prioritise prevention messaging.

**Acceptance criteria**
- **Given** the **HighBP vs Diabetes** view, **when** I hover a bar, **then** the tooltip shows **count** and **% diabetic** for that category (Yes/No).
- **Given** the **PhysActivity × Smoker** view, **when** I read the cells, **then** each shows **diabetes prevalence (%)** and I can **spot the highest-risk combination** at a glance.
- **Given** the **Sex** filter, **when** I change it, **then** both visuals **recalculate correctly**.

**Mapped visual(s):**  
- **100% Stacked Bar:** HighBP (Yes/No) split by Diabetes (Yes/No)  
- **Heatmap (Highlight Table):** Diabetes Prevalence (%) by PhysActivity (Yes/No) × Smoker (Yes/No)  

**Mapped data:** `data/combined_cleaned_final.csv`

### Story 3 — Grace, Programme Lead
**As** Grace (Programme Lead), **I want** the dashboard to communicate insights clearly to non-technical stakeholders, **so that** decisions can be made quickly.

**Acceptance criteria**
- **Given** any chart, **when** I hover a mark, **then** the tooltip explains metrics in **plain English** (e.g., “% with diabetes”) and shows counts.
- **Given** the dashboard on a laptop, **when** I view titles/axes/legends, **then** text is **readable** with **high-contrast** colours and no truncation.
- **Given** filters are applied, **when** I look at chart titles, **then** the **active filter context** is visible (e.g., “Sex: Female”).

**Mapped visual(s):** All visuals above with accessible titles, legends, tooltips, and filters  
**Mapped data:** `data/combined_cleaned_final.csv`

## Agile user stories

**As a Public Health Analyst (Amelia),** I want to explore diabetes prevalence across age groups and BMI distributions, **so that** I can target prevention programmes at the highest-risk segments.

**As a Policy Planner (Ravi),** I want to compare diabetes prevalence across modifiable behaviours (physical activity, smoking, high blood pressure), **so that** I can prioritise effective prevention messaging and resource allocation.

**As a Programme Lead (Grace),** I want a clear, accessible dashboard with readable labels, meaningful tooltips, and simple filters, **so that** non-technical stakeholders can quickly understand insights and make informed decisions.

## Hypothesis and How to Validate Them
Following the EDA, we formalised five hypotheses focused on lifestyle/health factors and diabetes status.  
All tests use the cleaned, human-readable dataset: `data/combined_cleaned_final.csv`.  
Target variable: **`Diabetes_binary`** (0 = No, 1 = Yes). We report both **statistical significance** and **effect size**.

> **Decision rules:** primary α = 0.05; we also report a Bonferroni-adjusted threshold of 0.01 (for 5 tests) to guard against multiple comparisons.

---

### H1 — Smoking and Diabetes
- **Question:** Are smokers more likely to have diabetes than non-smokers?
- **Variables:** `Smoker` (0/1) vs `Diabetes_binary` (0/1)
- **H0:** Smoking status is independent of diabetes.  
  **H1:** Smoking status is associated with diabetes.
- **Test:** Chi-square test of independence  
  **Effect size:** Cramér’s V
- **Validation procedure:** Build a 2×2 contingency table (`pd.crosstab`), run Chi-square, compute Cramér’s V; record p-value and effect size.
- **Status:** *Tested* → see `data/hypothesis_results_summary.csv`.

### H2 — BMI and Diabetes
- **Question:** Do BMI values differ between diabetic and non-diabetic respondents?
- **Variables:** `BMI` (numeric) vs `Diabetes_binary` (0/1)
- **H0:** BMI distributions are the same across groups.  
  **H1:** BMI distributions differ.
- **Test:** Mann–Whitney U (non-parametric)  
  **Effect size:** Rank-biserial correlation (direction & magnitude)
- **Validation procedure:** Split `BMI` by outcome, run Mann–Whitney U, compute rank-biserial; report medians and n per group.
- **Status:** *Tested* → see `data/hypothesis_results_summary.csv`.

### H3 — Physical Activity and Diabetes
- **Question:** Do physically active respondents have different diabetes prevalence than inactive respondents?
- **Variables:** `PhysActivity` (0/1) vs `Diabetes_binary` (0/1)
- **H0:** Physical activity is independent of diabetes.  
  **H1:** Physical activity is associated with diabetes.
- **Test:** Chi-square test of independence  
  **Effect size:** Cramér’s V
- **Validation procedure:** 2×2 crosstab, Chi-square, Cramér’s V; record p-value and effect size.
- **Status:** *Tested* → see `data/hypothesis_results_summary.csv`.

### H4 — High Blood Pressure and Diabetes
- **Question:** Is high blood pressure associated with diabetes?
- **Variables:** `HighBP` (0/1) vs `Diabetes_binary` (0/1)
- **H0:** High blood pressure is independent of diabetes.  
  **H1:** High blood pressure is associated with diabetes.
- **Test:** Chi-square test of independence  
  **Effect size:** Cramér’s V
- **Validation procedure:** 2×2 crosstab, Chi-square, Cramér’s V; record p-value and effect size.
- **Status:** *Tested* → see `data/hypothesis_results_summary.csv`.

### H5 — Age Group and Diabetes
- **Question:** Does diabetes prevalence differ across age groups?
- **Variables:** `Age` (ordered categories) vs `Diabetes_binary` (0/1)
- **H0:** Diabetes prevalence is the same across age groups.  
  **H1:** Diabetes prevalence differs across age groups.
- **Test:** Chi-square across categories (treat `Age` as categorical)  
  **Effect size:** Cramér’s V
- **Validation procedure:** Crosstab (`Age` × outcome), Chi-square, Cramér’s V; also compute prevalence by `Age` for interpretation.
- **Status:** *Tested* (optional to visualise) → see `data/hypothesis_results_summary.csv`.

---

### Outputs & Traceability
- A consolidated results file is exported for transparency and dashboarding:  
  **`data/hypothesis_results_summary.csv`** → includes hypothesis ID, test used, p-value (`p`), effect size (`effect_value`), interpretation (`effect_note`), and notes.
- These hypotheses directly inform the planned Tableau visuals:
  - **Bar:** Age vs Diabetes Prevalence (%) → *H5*
  - **Boxplot:** BMI by Diabetes status → *H2*
  - **100% Stacked Bar:** HighBP split by Diabetes → *H4*
  - **Heatmap (Highlight Table):** PhysActivity × Smoker prevalence → *H1 & H3 combined context*

> **Interpretation note:** We distinguish between “statistically significant” and “practically meaningful.” Where effect sizes are negligible/small, we avoid over-claiming and rely on multivariate ML models for richer patterns.

## Project Plan

**Overview of Key Steps Completed**

### 1 – ETL (Extract, Transform, Load)  
- Extracted the 2015 BRFSS Diabetes Health Indicators dataset from Kaggle.  
- Merged datasets, removed duplicates, and standardized column names for consistency.  
- Cleaned the data by addressing invalid values (e.g., replacing “0” in medically impossible fields), validating completeness, and renaming fields to human-friendly labels.  
- Saved the cleaned output as `combined_cleaned_final.csv` for downstream EDA and hypothesis testing.

### 2 – Feature Engineering  
- Encoded categorical variables: Label Encoding for binaries, One-Hot for multi-category features.  
- Scaled numeric features (e.g., BMI, glucose) for machine learning readiness.  
- Documented all features in a data dictionary for transparency.  
- Produced two ML-ready datasets:  
  - `combined_ml_ready.csv` (full)  
  - `combined_ml_ready_sample.csv` (smaller preview for GitHub use)

### 3 – Exploratory Data Analysis (EDA) & Hypothesis Testing  
- Conducted visualisation and summary statistics to identify patterns (e.g., age bands, BMI distributions, prevalence trends).  
- Mapped business hypotheses (e.g., associations between smoking, activity, BP and diabetes) to appropriate statistical tests:  
  - Chi-square tests for categorical relationships  
  - Mann–Whitney U for BMI distribution differences  
- Recorded p-values and effect sizes (e.g., Cramér’s V, rank-biserial) in `hypothesis_results_summary.csv` for transparency.

### 4 – Machine Learning Modeling  
- Split data into training and test sets (e.g., 80/20 split).  
- Evaluated multiple classifiers: Logistic Regression, Random Forest, and others.  
- Assessed performance using metrics such as Accuracy, Precision, Recall, F1-score, and ROC-AUC.  
- Compared models and documented findings (report or notebook summary).

### 5 – Tableau Dashboard Development  
- Built an interactive dashboard using produced charts and KPIs:  
  - “Total Respondents” and “Diabetes Prevalence (%)” KPI tiles  
  - Age vs Diabetes Prevalence bar chart  
  - BMI Box Plot by Diabetes status  
  - High Blood Pressure vs Diabetes (100% stacked bar)  
  - Smoking × Physical Activity heatmap (prevalence highlight table)  
- Incorporated global filters (Sex, Age), accessible tooltips, high-contrast palettes, and ethical disclaimers.  
- Published two dashboard views on Tableau Public:  
  - **[Overview](https://public.tableau.com/app/profile/nasra.ibrahim/viz/DiabetesAnalysisOverview/Overview)**  
  - **[Main Analysis Dashboard](https://public.tableau.com/app/profile/nasra.ibrahim/viz/DiabetesAnalysisDashboard_17549758193010/DiabetesAnalysisDashboard)**

## Data Management Practices:
Large datasets tracked with Git LFS.

Version-controlled outputs at each stage (cleaned, ml_ready, sample).

Documented transformations for reproducibility.

## Methodology Rationale:
Selected survey-based dataset for public health relevance.

Used encoding and scaling to prepare data for classification models.

Generated a sample dataset to support reproducibility and reduce repository size.

## The Rationale to Map the Business Requirements to the Data Visualisations

The Tableau visuals were designed to directly address the project's business requirements and agile user stories.  
Each visual provides a clear link between the analytical goals and the dataset’s available features.

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
### 1) Data privacy & governance
- **Source & identifiability:** This project uses a publicly available, de-identified survey dataset (BRFSS 2015, via Kaggle). No direct personal identifiers are included.  
- **Data minimisation:** Only fields necessary for analysis were retained; derived/aggregated outputs are shared (e.g., charts, summary CSVs).  
- **Repository hygiene:** No sensitive credentials or private data are stored in the repo. Large raw files are avoided; only the cleaned dataset required for reproducibility is included.  
- **GDPR mindset (good practice):** Although data are de-identified, we follow the principles of **lawfulness, fairness, transparency**, **data minimisation**, **storage limitation**, and **integrity/confidentiality**.

### 2) Bias, fairness & representativeness
- **Sampling bias:** BRFSS is a telephone survey. Certain groups may be under/over-represented; results may not perfectly reflect the entire population.  
- **Weights not applied:** Unless survey weights are applied, reported prevalence is **dataset-level**, not a population estimate. The dashboard will phrase results accordingly (e.g., “in this dataset”).  
- **Self-report bias:** Health behaviours (e.g., smoking, physical activity) are self-reported and can suffer from recall or social desirability bias.  
- **Model fairness:** Predictive performance can vary across subgroups (e.g., Sex, Age). We plan to **slice metrics by subgroup** (recall, precision) to check for disparities and document them in the report/dashboard.

### 3) Appropriate use & harm reduction
- **No clinical use:** The dashboard and models are **educational** and **exploratory**; they are **not** medical devices and must not be used for diagnosis or treatment decisions.  
- **Association ≠ causation:** The dataset is cross-sectional. Hypothesis tests and models show associations, **not** causal effects.  
- **Threshold trade-offs:** Classification thresholds affect false positives/negatives. Any recommended threshold should be motivated by the chosen objective (e.g., prioritising recall to reduce missed high-risk cases) and clearly communicated.  
- **Transparency:** We report model metrics (Accuracy, Precision, Recall, F1, ROC-AUC) and provide plain-English summaries so non-technical readers understand limitations.

### 4) Governance, licensing & attribution
- **Attribution:** Dataset source and tools (e.g., Python libraries, AI assistants) are credited in the *Credits* section.  
- **Permissible use:** Data are used for non-commercial, educational purposes in line with the source’s terms.  
- **Version control:** Changes are tracked via Git with meaningful commit messages to ensure accountability and reproducibility.

### 5) What we implemented in this project
- Used a **cleaned, de-identified** dataset and stored only what’s required for reproducibility.  
- Reported **statistical significance and effect sizes** to avoid over-claiming results.  
- Compared multiple models and exported metrics transparently; avoided presenting predictions as clinical advice.  
- Ensured dashboard copy will state “**in this dataset**” and avoid population-level claims unless weights are applied.

### 6) Planned before submission (quality checks)
- Add a short **disclaimer card** on the dashboard (educational use, association ≠ causation).  
- **Subgroup fairness check:** compute and document model metrics by Sex and Age bands; comment on any notable disparities.  
- Review colour choices and labels for **accessibility** (high contrast, no red/green dependence, readable titles/tooltips).

# Dashboard Design

## Dashboard Design (Tableau)

**Data source:** `data/combined_cleaned_final.csv` (single source for all visuals)  
**Global filters:** Sex (optional), Age (optional)  
**Prevalence calculation:** create a calculated field `Diabetes Prevalence % = AVG([Diabetes_binary]) * 100` (since 0/1). Show counts in tooltips.

### Planned visuals (4 distinct types)

1) **Age vs Diabetes Prevalence (%) — Bar chart**
   - Columns: Age (ordered category)
   - Rows: `Diabetes Prevalence %`
   - Marks: Bar; show % labels; tooltip includes count and %
   - *Maps to Amelia*

2) **BMI Distribution by Diabetes Status — Boxplot**
   - Columns: Diabetes_binary (alias to No/Yes)
   - Rows: BMI
   - Marks: Box-and-whisker; tooltip shows median, IQR, n
   - *Maps to Amelia*

3) **High Blood Pressure vs Diabetes — 100% Stacked Bar**
   - Columns: HighBP (No/Yes)
   - Color: Diabetes_binary (No/Yes)
   - Quick table calc: Percent of Column; show % labels
   - *Maps to Ravi*

4) **PhysActivity × Smoker — Diabetes Prevalence (%) Heatmap**
   - Columns: Smoker (No/Yes)
   - Rows: PhysActivity (No/Yes)
   - Text/Color: `Diabetes Prevalence %`
   - Marks: Square (highlight table); show % labels
   - *Maps to Ravi*

### UX & accessibility
- Plain-English titles (e.g., “Diabetes Prevalence by Age (%)”).
- High-contrast palette; avoid red/green.
- Tooltips explain metrics (“% with diabetes”) and show counts.
- Titles display active filter context (e.g., “Sex: Female”).

**Ethical notice on dashboard**
A small disclaimer card is displayed on the dashboard:
“Educational use only. Association ≠ causation. Not medical advice.
BRFSS 2015 (self-reported, de-identified); unweighted percentages.”

Rationale: Communicates dataset limits and appropriate use to non-technical audiences. 

# Tableau Dashboards
To view the interactive visualisations built for this project:

Diabetes Analysis Overview — High-level summary of key insights, KPIs (Total Respondents, Diabetes Prevalence), and context for the analysis- https://public.tableau.com/app/profile/nasra.ibrahim/viz/DiabetesAnalysisOverview/Overview 

Main Analysis Dashboard — Detailed interactive dashboard answering the defined business requirements and user stories- https://public.tableau.com/app/profile/nasra.ibrahim/viz/DiabetesAnalysisDashboard_17549758193010/DiabetesAnalysisDashboard

# Unfixed Bugs
- **GitHub large file limit:** Full dataset (`combined_ml_ready.csv`) tracked with Git LFS but cannot be previewed in GitHub.
- **Tableau KPI formatting:** Titles and percentage alignment required multiple adjustments; some minor misalignment may still occur.
- **Title truncation in Tableau:** Longer titles can be cut off in published view on smaller screens.
- **Separate dashboards:** Overview and Main Dashboard are published separately; could be combined into a Tableau Story for smoother navigation.
- **Mobile responsiveness:** Some visuals may require scrolling or lose detail on smaller devices.

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

