# 📈 Rossmann Store Sales Forecasting

## 1. Business Problem, Objectives & Hypotheses

### The Business Problem
Rossmann operates over 3,000 drugstores across 7 European countries. Store managers are tasked with predicting their daily sales for up to six weeks in advance. Accurate sales forecasts allow managers to create reliable staff schedules that match customer demand, ultimately improving operational efficiency and reducing costs. Currently, predicting sales across thousands of individual stores with varying promotions, local holidays, and competitor distances is a complex challenge.

### Objectives
* **Primary Goal:** Build a robust, end-to-end machine learning regression pipeline to predict daily sales (Sales) for Rossmann stores up to 6 weeks into the future.
* **Metric Target:** Minimize evaluation error using RMSE, MAE, and $R^2$ to ensure accurate forecasting.
* **Productization:** Package the pipeline into modular Python scripts and deliver clean insights via a visual dashboard or report.

### Core Hypotheses
* **Hypothesis 1 (Promotions):** Stores with active promotions (`Promo`) will show a significantly higher sales volume compared to non-promo days.
* **Hypothesis 2 (Competition):** Stores with a closer competitor (`CompetitionDistance`) might experience lower sales initially, unless compensated by high local demand.
* **Hypothesis 3 (Holidays):** Sales will drop or spike dramatically depending on whether a state holiday or school holiday forces store closures.

---

## 2. Project Workflow & Methodology
1. **Data Preprocessing & Cleaning:** Handled missing values, engineered date/time features, encoded categorical variables, and prepared robust training/validation datasets.
2. **Exploratory Data Analysis (EDA):** Uncovered trends related to store types, promotional impact, competitive pressures, and seasonal shopping cycles.
3. **Machine Learning Model Training & Tuning:** Evaluated multiple regression models, including Random Forest and Gradient Boosting, and optimized hyperparameters using `RandomizedSearchCV`.
4. **Model Evaluation & Residual Diagnostics:** Selected the tuned **Gradient Boosting** model as the champion based on high accuracy ($R^2$ = 90.49%) and low error metrics (MAE: 657.74, RMSE: 958.17). Performed rigorous residual error distribution analysis across over 168,000 validation records.
5. **Business Insights & Visualization:** Mapped feature importances, analyzed residuals (identifying directional bias, temporal variance, and outliers), and translated technical findings into actionable retail strategies.

---

## 3. Key Findings & Feature Importance & Error Analysis
* **Store Baseline & Location (`Store` & `CompetitionDistance`):** Individual store identity (**21.4%**) and distance to the nearest competitor (**20.5%**) serve as the most critical structural factors establishing baseline sales capacity and local market competition.
* **Promotional Impact (`Promo`):** Active promotional campaigns account for (~**16.8%**) of the model's decision-making power. Residual analysis reveals that while promos drive sales, they also introduce behavioral volatility that increases absolute error (733.92 vs. 596.56 units).
* **Temporal, Seasonal & Error Volatility:** Day-of-week shopping cycles, monthly trends, and specialized error tracking highlight peak variance on start/end-of-week days and a massive December error outlier spike (MAE of 1,160 units) due to holiday shopping behavior.

---

## 4. Business Insights & Recommendations

Based on our best-performing **Tuned Gradient Boosting** model ($R^2$ = 90.49%) and thorough error analysis, here are the key insights and actionable recommendations for store management, organized by strategic category:

<details>
<summary><b>Category 1: Workforce & Operational Scheduling</b> (Click to expand)</summary>

* **Staffing Based on Store Capacity & Timing**
  * *Analytical Finding:* Individual store identity and local market context (`Store` and `CompetitionDistance`) account for a major share of the model's predictive power.
  * *Actionable Recommendation:* Management should schedule staff shifts dynamically based on store-specific historical traffic patterns and local market demand rather than relying on blanket company-wide averages.
* **Weekly Traffic & Operating Patterns**
  * *Analytical Finding:* Average sales peak sharply on Monday and Sunday, with a dip midweek. Error analysis further proves that prediction variance and volatility spike on these start-and-end-of-week days.
  * *Actionable Recommendation:* Store managers must align staffing levels with these weekly cyclical surges—ensuring peak support on Mondays for the post-closure rush, and staffing Sunday operations in transit hubs to capture commuter spending.

</details>

<details>
<summary><b>Category 2: Calendar & Seasonal Planning</b> (Click to expand)</summary>

* **Targeted Promotional Planning**
  * *Analytical Finding:* Active promotions (`Promo`) provide a powerful boost to sales, but error analysis shows they introduce behavioral demand spikes that elevate average absolute error (733.92 vs 596.56 units).
  * *Actionable Recommendation:* Marketing teams should time campaigns strategically during slower days, while store managers must introduce a manual inventory and staffing buffer during active promotional windows.
* **Holiday Impact & Public Holiday Operations**
  * *Analytical Finding:* Average sales spike notably when select stores open on state or public holidays, whereas normal operating days average lower revenue.
  * *Actionable Recommendation:* Because only specific locations (such as travel hubs or tourist zones) open on holidays, management must ensure these open stores are fully staffed to capture heavy holiday spending.
* **Seasonal Surge & December Planning**
  * *Analytical Finding:* Sales experience a massive surge in December (Month 12)—which simultaneously introduces our highest residual error outlier spike (MAE of 1,160 units) due to complex holiday shopping behavior.
  * *Actionable Recommendation:* Leadership must prepare early for the year-end peak by ramping up logistics, scheduling extra seasonal floor staff well in advance, and building a predictive error buffer into Q4 inventory planning.

</details>

<details>
<summary><b>Category 3: Store Format, Assortment & Layout</b> (Click to expand)</summary>

* **Assortment Type Strategy**
  * *Analytical Finding:* Assortment type `b` achieves the highest average sales, outperforming both basic (`a`) and extended (`c`) assortments.
  * *Actionable Recommendation:* Offering optimized product variety plays a major role in driving higher customer spending. Store management should evaluate rolling out similar optimized product assortments across more locations.
* **Store Format & Layout Optimization**
  * *Analytical Finding:* Store format heavily influences baseline performance. Furthermore, our error breakdown reveals that **Store Type 1** experiences the highest average forecast error (839.71 units), indicating greater customer traffic volatility.
  * *Actionable Recommendation:* Management should apply closer operational oversight, layout optimization, and targeted manual inventory buffers specifically for Store Type 1 locations to handle demand unpredictability.

</details>

<details>
<summary><b>Category 4: Advanced Location-Specific & Supply Chain Strategies</b> (Click to expand)</summary>

* **Inventory & Supply Chain Optimization**
  * *Analytical Finding:* The model achieves a reliable daily error baseline centered tightly around zero, providing strong support for demand planning with a slight over-prediction buffer (53.55%) to prevent stockouts.
  * *Actionable Recommendation:* Supply chain teams can fine-tune daily stock orders to prevent empty shelves and reduce excess inventory waste.
* **The Traffic vs. Basket-Size Split (Store-Specific Strategy)**
  * *Analytical Finding:* Location and store format heavily influence baseline performance, meaning a one-size-fits-all approach doesn't work.
  * *For Busy (High-Traffic) Stores:* Instead of trying to get more people through the door, train staff to encourage shoppers to buy more items per visit using **up-selling** and **cross-selling**:
    * *Rossmann Up-Sell Example:* A customer picks up a standard shampoo (€2.50), and the cashier or display highlights a larger, premium/organic shampoo for €4.50, increasing total basket value.
    * *Rossmann Cross-Sell Example:* A customer brings a hair dye kit to the counter, and the cashier suggests complementary items like protective gloves or a mixing brush to complete their purchase.
  * *For Slow (Low-Traffic) Stores:* Focus all marketing and ads purely on getting people to physically walk inside.
* **Localized Competitive Defense Zoning**
  * *Analytical Finding:* Proximity to competitors (`CompetitionDistance`) heavily impacts baseline performance as one of our top predictive drivers.
  * *Actionable Recommendation:* Segment stores into **"High-Threat Zones"** (competitors right next door) and **"Isolated Zones,"** deploying special promotional discounts only where needed to protect market share and save marketing budget everywhere else.

</details>

---

## 📊 5. Tableau Presentation & Dashboard
*(Link to the interactive Tableau presentation and dashboard will be added here soon)*

---

## 🚀 6. Tech Stack
* **Language:** Python
* **Libraries:** Pandas, NumPy, Scikit-Learn, Matplotlib, Seaborn
* **Tools:** Jupyter Notebook, Git, GitHub, Tableau