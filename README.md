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
4. **Model Evaluation:** Selected the tuned **Gradient Boosting** model as the champion based on high accuracy ($R^2$ = 90.49%) and low error metrics (MAE: 657.74, RMSE: 958.17).
5. **Business Insights & Visualization:** Mapped feature importances, analyzed residuals, and translated technical findings into actionable retail strategies.

---

## 3. Key Findings & Feature Importance
* **Store Baseline & Location (`Store` & `CompetitionDistance`):** Individual store identity (**21.4%**) and distance to the nearest competitor (**20.5%**) serve as the most critical structural factors establishing baseline sales capacity and local market competition.
* **Promotional Impact (`Promo`):** Active promotional campaigns account for (~**16.8%**) of the model's decision-making power, capturing immediate customer surges during marketing windows.
* **Temporal & Operational Cycles (`DayOfWeek`, `Month`, & Competition Open Dates):** Day-of-week shopping patterns, seasonal months, and competitor tenure provide the remaining essential signals to fine-tune daily store forecasts.

---

## 4. Business Insights & Recommendations

Based on our best-performing **Tuned Gradient Boosting** model ($R^2$ = 90.49%), here are the key insights and actionable recommendations for store management, organized by strategic category:

<details>
<summary><b>Category 1: Workforce & Operational Scheduling</b> (Click to expand)</summary>

* **Staffing Based on Store Capacity & Timing**
  * *Analytical Finding:* Individual store identity and local market context (`Store` and `CompetitionDistance`) account for a major share of the model's predictive power.
  * *Actionable Recommendation:* Management should schedule staff shifts dynamically based on store-specific historical traffic patterns and local market demand rather than relying on blanket company-wide averages.
* **Weekly Traffic & Operating Patterns**
  * *Analytical Finding:* Average sales peak sharply on Monday and Sunday, with a dip midweek. Sundays spike because only specialized transit-hub stores operate, while Mondays experience a major rush right after Sunday closures.
  * *Actionable Recommendation:* Store managers must align staffing levels with these weekly cyclical surges—ensuring peak support on Mondays for the post-closure rush, and staffing Sunday operations in transit hubs to capture commuter spending.

</details>

<details>
<summary><b>Category 2: Calendar & Seasonal Planning</b> (Click to expand)</summary>

* **Targeted Promotional Planning**
  * *Analytical Finding:* Active promotions (`Promo`) provide a reliable, powerful boost to daily sales, accounting for nearly 17% of the model's decision-making power.
  * *Actionable Recommendation:* Marketing teams should time campaigns strategically during slower days to increase revenue and smooth out traffic dips.
* **Holiday Impact & Public Holiday Operations**
  * *Analytical Finding:* Average sales spike notably when select stores open on state or public holidays, whereas normal operating days average lower revenue.
  * *Actionable Recommendation:* Because only specific locations (such as travel hubs or tourist zones) open on holidays, management must ensure these open stores are fully staffed to capture heavy holiday spending.
* **Seasonal Surge & December Planning**
  * *Analytical Finding:* Sales remain steady throughout most of the year, but experience a massive surge in December (Month 12) due to Christmas preparations and holiday shopping.
  * *Actionable Recommendation:* Leadership must prepare early for the year-end peak by ramping up logistics, scheduling extra seasonal floor staff well in advance, and launching targeted holiday gift campaigns.

</details>

<details>
<summary><b>Category 3: Store Format, Assortment & Layout</b> (Click to expand)</summary>

* **Assortment Type Strategy**
  * *Analytical Finding:* Assortment type `b` achieves the highest average sales, outperforming both basic (`a`) and extended (`c`) assortments.
  * *Actionable Recommendation:* Offering optimized product variety plays a major role in driving higher customer spending. Store management should evaluate rolling out similar optimized product assortments across more locations.
* **Store Format & Layout Optimization**
  * *Analytical Finding:* Store format and layout heavily influence baseline sales performance.
  * *Actionable Recommendation:* Management should analyze store layout structures (such as product placement, promotional island displays, and checkout queue positioning) to optimize customer flow and improve overall sales conversion across different store types.

</details>

<details>
<summary><b>Category 4: Advanced Location-Specific & Supply Chain Strategies</b> (Click to expand)</summary>

* **Inventory & Supply Chain Optimization**
  * *Analytical Finding:* The model achieves a reliable daily error baseline (MAE of 657.74), providing strong support for demand planning.
  * *Actionable Recommendation:* Supply chain teams can fine-tune daily stock orders to prevent empty shelves and reduce excess inventory waste.
* **The Traffic vs. Basket-Size Split (Store-Specific Strategy)**
  * *Analytical Finding:* Location and store format heavily influence baseline performance, meaning a one-size-fits-all approach doesn't work.
  * *For Busy (High-Traffic) Stores:* Instead of trying to get more people through the door, train staff to encourage shoppers to buy more items per visit using **up-selling** and **cross-selling**:
    * *Rossmann Up-Sell Example:* A customer picks up a standard shampoo (€2.50), and the cashier or display highlights a larger, premium/organic shampoo for €4.50. Persuading the customer to choose the slightly higher-end or larger product to increase their total basket value.
    * *Rossmann Cross-Sell Example:* A customer brings a hair dye kit to the counter, and the cashier suggests complementary items like protective gloves or a mixing brush. Recommending useful companion items that naturally match what the customer is already buying to make their purchase complete while increasing total sales.
  * *For Slow (Low-Traffic) Stores:* Focus all marketing and ads purely on getting people to physically walk inside.
* **Localized Competitive Defense Zoning**
  * *Analytical Finding:* Proximity to competitors (`CompetitionDistance`) heavily impacts baseline performance as one of our top predictive drivers.
  * *Actionable Recommendation:* Don't waste money running the same discount sales across every single store in the company. Instead, segment stores into **"High-Threat Zones"** (competitors right next door) and **"Isolated Zones,"** deploying special promotional discounts only where needed to protect your customers and save your budget everywhere else.

</details>

---

## 📊 5. Tableau Presentation & Dashboard
*(Link to the interactive Tableau presentation and dashboard will be added here soon)*

---

## 🚀 6. Tech Stack
* **Language:** Python
* **Libraries:** Pandas, NumPy, Scikit-Learn, Matplotlib, Seaborn
* **Tools:** Jupyter Notebook, Git, GitHub, Tableau