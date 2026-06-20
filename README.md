# Retail Promotion Response Optimization & Customer Modeling
**Domain:** E-Commerce & Retail Marketing Analytics | **Role:** Business Analyst

---

## 📌 Executive Summary & Business Recommendations
An analysis of 2,240 customer encounters was conducted using structural SQL querying, advanced Excel descriptive profiling, and Power BI interactive dashboards to evaluate historical campaign performance, web platform engagement, product preferences, and demographic purchasing distributions.

### Key Business Insights:
* **Product Performance Optimization:** **Wines** and **Meat** products dominate revenue streams, driving **$680,816** and **$373,968** in expenditures respectively. Fruits ($58,917) and Sweets ($60,621) lag behind significantly.
* **Campaign Conversion Benchmarking:** Historically, **Campaign 4** was the most successful iteration with **167** conversions. The latest marketing initiative captured a **14.9% response rate** (334 engaged customers out of 2,240), signaling a clear requirement for stricter demographic targeting or enhanced value propositions.
* **Digital Traffic Trends:** Customers aged **46 to 60** display the highest online web interaction, averaging **5.65 website visits per month**, followed closely by the 30–45 age cohort (5.44 visits). Senior customers (Over 60) visit least frequently (4.88 visits).
* **Household Demographics:** The typical consumer household reflects an average of **0.44 children** and **0.51 teenagers**, marking a clear opportunity to pitch bundle offers catered to small family segments.

### Strategic Recommendations:
1. **Cross-Product Bundling Strategy:** Leverage high-volume segments (Wines and Meats) by building cross-promotional bundles featuring low-performing items (Fruits/Sweets) to clear stagnating inventory.
2. **Targeted Digital Campaigns:** Focus high-frequency, mid-week online advertisement spending specifically toward the 46–60 age group, maximizing ROI where natural web traffic is strongest.
3. **Re-engagement Tactics:** Develop a specialized retention campaign mimicking the mechanics of historic Campaign 4, specifically isolating the 1,906 non-responsive users from the last campaign loop.

---

## 📋 Section 1: Business Requirements Document (BRD)
*This document outlines the standard 7-part business requirement framework used to align cross-functional tech stakeholders and define the analytical project delivery scope.*

* **Project Name:** Retail Promotion Response Optimization Dashboard
* **Project Manager:** Saurabh
* **Date Submitted:** June 21, 2026
* **Document Status:** [X] Approved

---

### 1. Executive Summary
PromoScope Insights is experiencing declining customer conversion rates and increased promotional waste across its retail marketing operations. This project delivers an integrated business analytics framework—leveraging SQL relational database structuring, Excel diagnostics, and interactive Power BI dashboards. By transforming data from 2,240 customer interactions into structured insights, this framework enables marketing strategists to perform precise behavioral micro-segmentation, improve promotional conversion rates above the baseline 14.9%, and recover marketing ROI.

### 2. Project Objectives
* **Data Integration:** Clean, format, and ingestion a relational customer database containing 2,240 distinct customer touchpoints into a centralized environment.
* **Exploratory Profiling:** Use structured SQL aggregations and advanced Excel logic features to isolate peak-spending products and segment web interaction trends by age tiers.
* **Interactive Business Intelligence:** Construct a dynamic, executive-ready Power BI reporting platform to visualize multi-tiered socio-demographic intersections and clear bottlenecks in promotional outreach campaigns.

### 3. Project Scope
* **In-Scope (Included):**
  * Drafting business requirement blueprints and data dictionaries.
  * Relational SQL schema design, type-casting temporal attributes (`ct_customer`), and executing diagnostic database queries.
  * Excel descriptive statistical analysis, anomaly profiling, and feature engineering.
  * Constructing dynamic DAX visual variables and interactive reporting layouts in Power BI Desktop.
* **Out-of-Scope (Excluded):**
  * Automated real-time streaming integrations with external CRM software engines.
  * Creating autonomous programmatic advertising triggers or email-sending applications.
  * Managing financial transaction records, invoicing logs, or billing gateway microservices.

### 4. Business Requirements

| Priority Level | Critical Level | Requirement Description |
| :--- | :--- | :--- |
| **High** | Critical | Standardize historical customer transaction data schemas and properly transform data columns into valid timestamp attributes (`DATETIME`). |
| **High** | High | Perform multi-tiered behavioral aggregations isolating historical campaign performance counts alongside web visitation metrics across binned age brackets. |
| **Medium** | High | Build a robust Power BI application containing functional filters for education and marital metrics to track luxury category spending trends against household income levels. |

### 5. Key Stakeholders

| Name | Job Role | Duties |
| :--- | :--- | :--- |
| **Saurabh** | Project Manager | Provides overarching timeline tracking, project roadmap sign-off, and scope evaluation governance. |
| **Campaign Strategist** | Marketing Lead / End-User | Consumes interactive reporting matrices to adjust active inventory bundles and execute target promotional tracks. |
| **BI Developer** | Data Engineer / Analyst | Builds structural back-end SQL query streams, designs data pipelines, and deploys DAX data visualization layers. |

### 6. Project Constraints

| Constraint | Description |
| :--- | :--- |
| **Data Recency** | Insights are bounded entirely by the offline historical marketing campaign dataset; live automated streaming infrastructure is omitted from this cycle. |
| **Security & Privacy** | Consumer identity details must be fully pseudonymized through individual identification markers (`ID`) to adhere strictly to regional data privacy laws. |

### 7. Cost-Benefit Analysis
* **Cost:** Development overhead, business analysis design cycles, and internal Power BI cloud workspace subscription requirements.
* **Benefit:** Eliminates marketing budget waste by restricting poor promotional matches, targets high-frequency consumer groups (Ages 46-60), and accelerates executive decision-making.
* **Expected ROI:** Projected 15% reduction in promotional overhead within the first two operational fiscal quarters post-dashboard launch.

## 🗄️ Section 2: Data Loading & Preprocessing (SQL)
*Engineered structured relational database pipelines to standardize raw transaction layers.*

### 1. Total Customer Encounters
```sql
SELECT 
    COUNT(*) AS total_encounters
FROM 
    retail_data.marketing_campaign;
```

| total_encounters |
| :--- |
| 2,240 |

### 2. Product Spending Performance Analysis
```sql
SELECT Product, SUM(Amount) AS Total_Spent 
FROM (
    SELECT 'Wines' AS Product, MntWines AS Amount FROM retail_data.marketing_campaign 
    UNION ALL
    SELECT 'Fruits', MntFruits FROM retail_data.marketing_campaign 
    UNION ALL
    SELECT 'Meat', MntMeatProducts FROM retail_data.marketing_campaign 
    UNION ALL
    SELECT 'Fish', MntFishProducts FROM retail_data.marketing_campaign 
    UNION ALL
    SELECT 'Sweets', MntSweetProducts FROM retail_data.marketing_campaign 
    UNION ALL
    SELECT 'Gold', MntGoldProds FROM retail_data.marketing_campaign
) t 
GROUP BY Product 
ORDER BY Total_Spent DESC;
```

| Product | Total_Spent |
| :--- | :--- |
| Wines | 680,816 |
| Meat | 373,968 |
| Gold | 96,609 |
| Fish | 84,057 |
| Sweets | 60,621 |
| Fruits | 58,917 |

### 3. Customer Demographic Breakdown
```sql
SELECT 
    education, 
    marital_status, 
    COUNT(*) AS customer_count
FROM 
    retail_data.marketing_campaign
GROUP BY 
    education, 
    marital_status
ORDER BY 
    education, 
    customer_count DESC;
```

| education | marital_status | customer_count |
| :--- | :--- | :--- |
| 2n Cycle | Married | 81 |
| 2n Cycle | Together | 57 |
| Graduation | Married | 433 |
| Graduation | Together | 286 |
| Graduation | Single | 252 |
| Master | Married | 138 |
| PhD | Married | 192 |

### 4. Average Customer Income
```sql
SELECT 
    AVG(income) AS average_income
FROM 
    retail_data.marketing_campaign;
```

| average_income |
| :--- |
| 52,247 |

### 5. Historic Campaign Performance
```sql
SELECT
    SUM(CAST(AcceptedCmp1 AS INT)) AS campaign_1,
    SUM(CAST(AcceptedCmp2 AS INT)) AS campaign_2,
    SUM(CAST(AcceptedCmp3 AS INT)) AS campaign_3,
    SUM(CAST(AcceptedCmp4 AS INT)) AS campaign_4,
    SUM(CAST(AcceptedCmp5 AS INT)) AS campaign_5
FROM 
    retail_data.marketing_campaign;
```

| campaign_1 | campaign_2 | campaign_3 | campaign_4 | campaign_5 |
| :--- | :--- | :--- | :--- | :--- |
| 144 | 30 | 163 | 167 | 163 |

### 6. Last Campaign Response Distribution
```sql
SELECT 
    response AS last_campaign_response, 
    COUNT(*) AS total_customers
FROM 
    retail_data.marketing_campaign
GROUP BY 
    response;
```

| last_campaign_response | total_customers |
| :--- | :--- |
| 0 (No Response) | 1,906 |
| 1 (Responded) | 334 |

### 7. Household Composition Analysis
```sql
SELECT
    AVG(CAST(kidhome AS DECIMAL(10,2))) AS avg_children,
    AVG(CAST(teenhome AS DECIMAL(10,2))) AS avg_teenagers
FROM 
    retail_data.marketing_campaign;
```

| avg_children | avg_teenagers |
| :--- | :--- |
| 0.444 | 0.506 |

### 8. Digital Engagement by Age Groups
```sql
SELECT
    CASE
        WHEN age < 30 THEN 'Under 30'
        WHEN age BETWEEN 30 AND 45 THEN '30-45'
        WHEN age BETWEEN 46 AND 60 THEN '46-60'
        ELSE 'Over 60'
    END AS age_group,
    AVG(CAST(NumWebVisitsMonth AS DECIMAL(10,2))) AS avg_visits_per_month
FROM 
    retail_data.marketing_campaign
GROUP BY
    CASE
        WHEN age < 30 THEN 'Under 30'
        WHEN age BETWEEN 30 AND 45 THEN '30-45'
        WHEN age BETWEEN 46 AND 60 THEN '46-60'
        ELSE 'Over 60'
    END;
```

| age_group | avg_visits_per_month |
| :--- | :--- |
| 30-45 | 5.436 |
| 46-60 | 5.647 |
| Over 60 | 4.880 |

---

## 📊 Section 3: Exploratory Data Analysis (Excel)
*Deep-dive diagnostics, statistical distributions, and automated calculations executed inside Microsoft Excel.*

### Core Analytical Operations Performed:
* **Descriptive Statistics:** Generated mean, median, standard deviation, and data range metrics to analyze customer income and spending dispersion.
* **Outlier Profiling:** Constructed box-and-whisker plots on the Income variable to isolate and flag extreme data skewness.
* **Time-Series Cohorts:** Built historical line charts tracking monthly customer enrollment velocities based on the transformed registration dates.
* **Demographic Cross-Tabulations:** Formulated custom Pivot Tables mapping multi-tiered campaign response frequencies across varying customer education levels and marital statuses.

📁 *The full analytical workbook file is uploaded and available in the [3_Exploratory_Analysis_Excel](./3_Exploratory_Analysis_Excel/) directory.*

---

## 📉 Section 4: Interactive Dashboard Design (Power BI / Tableau)
*Transforming structured calculation tables into responsive executive storytelling dashboards.*

### Analytical Models & DAX Measures Constructed:
1. **Dynamic Customer Ingestion Profile (Stacked Column Chart):** Binned baseline incomes into static $5,000 increments, mapping distinct counts of active customer IDs against their registration years.
2. **Socioeconomic Matrix (Clustered Bar Chart):** Evaluated macro-demographic intersections by grouping total client counts by highest education tier alongside marital status groupings.
3. **Core Purchasing Correlation Model (Scatter Chart):** Evaluated spending paths by plotting overall consumer income relative to a custom-engineered DAX feature tracking the percentage of income spent on luxury items.
4. **Category Spend Aggregation (Clustered Column Chart):** Deployed robust category evaluation measures tracking precise average product investments across separate groups:
   ```dax
   Sum of MntWines average per Education = 
   AVERAGEX(
       KEEPFILTERS(VALUES('marketing_campaign'[Education])),
       CALCULATE(SUM('marketing_campaign'[MntWines]))
   )
   ```

📁 *The interactive report model file is uploaded and available in the [4_Dashboards_PowerBI](./4_Dashboards_PowerBI/) directory.*


