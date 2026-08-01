# Rossmann Sales Prediction - Final End-to-End Data Science Project

## Phase 1: Business Problem, Objectives & Hypotheses

### 1. The Business Problem
Rossmann operates over 3,000 drugstores across 7 European countries. Store managers are tasked with predicting their daily sales for up to six weeks in advance. Accurate sales forecasts allow managers to create reliable staff schedules that match customer demand, ultimately improving operational efficiency and reducing costs. Currently, predicting sales across thousands of individual stores with varying promotions, local holidays, and competitor distances is a complex challenge.

### 2. The Objectives
* **Primary Goal:** Build a robust, end-to-end machine learning regression pipeline to predict daily sales (Sales) for Rossmann stores up to 6 weeks into the future.
* **Metric Target:** Minimize the evaluation error using RMSPE (Root Mean Square Percentage Error) and $R^2$ to ensure accurate forecasting.
* **Productization:** Package the pipeline into modular Python scripts and deliver clean insights via a visual dashboard or report.

### 3. Core Hypotheses (What we will test during EDA)
* **Hypothesis 1 (Promotions):** Stores with active promotions (Promo) will show a significantly higher sales volume compared to non-promo days.
* **Hypothesis 2 (Competition):** Stores with a closer competitor (CompetitionDistance) might experience lower sales initially, unless compensated by high foot traffic.
* **Hypothesis 3 (School/State Holidays):** Sales will drop or spike dramatically depending on whether a state holiday or school holiday forces store closures.
