# Blockbuster Box Office Revenue Predictor 🎬

## Overview
This repository contains a high-scale machine learning pipeline designed to forecast the first-week US and Canadian theatrical revenue for major blockbuster motion pictures. By modeling historical performance data, the project accounts for franchise momentum, star bankability, and macroeconomic factors, culminating in a specific revenue prediction for the upcoming *Avatar: Fire and Ash* (Avatar 3).

## Data Sources
The dataset covers the modern box office ecosystem (2009–2025), specifically isolating the era defined by the rise of Digital 3D Cinema and the structural disruptions of the streaming era. Data was aggregated and web-scraped from multiple financial and film databases:
* **Box Office Mojo:** Daily financial performance, opening theater counts, and cumulative gross.
* **IMDb:** Title basics and unique movie identifiers.
* **TMDB:** Production budgets, franchise/collection IDs, MPAA ratings, and star/director popularity metrics.

## Project Workflow
The analysis and modeling pipeline is divided into three main Jupyter Notebooks:

### 1. Creating the Fact Table (`1_Creating_the_Fact_Table.ipynb`)
* Aggregates daily financial charts to calculate the target variable: **first-week theatrical revenue**.
* Constructs the primary fact table by mapping unique IMDb IDs to the Box Office Mojo data to ensure seamless merges across different databases.

### 2. EDA & Feature Engineering (`2_EDA_and_Feature_Engineering.ipynb`)
* Refines the dataset to isolate high-stakes theatrical releases (budgets > $100,000 and opening day screens > 100) to remove low-budget indie noise.
* Conducts Exploratory Data Analysis (EDA) on release day impacts (e.g., standard Friday drops vs. Wednesday holiday releases).
* Engineers robust predictive features while mitigating the curse of dimensionality and data leakage:
  * **Franchise Strength:** `has_prequel`, `prequel_revenue_fixed`, `years_since_last_installment`, and `franchise_position`.
  * **Bankability:** Rolling historical revenue averages for directors and lead actors, with smart imputation for first-time directors.
  * **Economic Landscape:** Adjusted average ticket prices, inflation scaling, and macro consumer sentiment.
  * **Interaction Features:** Budget-per-theater ratios to capture niche vs. wide-release launch strategies.

### 3. Modeling & Avatar Prediction (`3_Modeling_and_Avatar_Prediction.ipynb`)
* Evaluates multiple algorithms including **Linear Regression, CatBoost, and XGBoost**.
* Applies log transformations to heavily right-skewed budget and revenue data, and utilizes quantile regression objective functions to handle heteroskedasticity when predicting massive outliers.
* Implements rigorous 10-fold cross-validation to ensure the model generalizes well to unprecedented blockbusters.
* **Performance:** The final XGBoost model achieved a robust 10-fold CV R² score of ~0.743.
* **Deployment:** Uses the tuned XGBoost model to generate a data-driven opening week forecast for *Avatar: Fire and Ash*.

## Technologies & Libraries
* **Language:** Python 3
* **Data Manipulation:** `pandas`, `numpy`, `statsmodels`
* **Visualization:** `matplotlib`, `seaborn`, `shap`
* **Machine Learning:** `scikit-learn`, `xgboost`, `catboost`, `lightgbm`

## Disclaimer
The analyses, feature engineering logic, and modeling architectures within this project are my own original work. AI assistance was utilized to optimize specific code blocks and explore implementation strategies for complex feature interactions.
