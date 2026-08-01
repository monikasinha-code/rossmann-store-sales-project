# Rossmann Sales Prediction - Final End-to-End Data Science Project

## 1. Business Problem & Objectives
* **The Business Problem:** Rossmann operates over 3,000 drugstores across 7 European countries. Store managers need to predict daily sales up to six weeks in advance to optimize staff scheduling and operational efficiency.
* **Primary Objective:** Build an end-to-end machine learning regression pipeline to forecast daily sales (`Sales`), evaluated using RMSPE.

## 2. Core Hypotheses
* **Promotions:** Stores with active promotions (`Promo`) will show significantly higher sales volume.
* **Competition:** Stores with closer competitors (`CompetitionDistance`) may experience lower individual sales unless offset by location traffic.
* **Holidays:** Sales will drop to zero during store closures and fluctuate based on school and state holidays.
