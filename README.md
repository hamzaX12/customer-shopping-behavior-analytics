<div align="center">

# 🛍️ Customer Shopping Behavior Analytics

**End-to-End Retail Data Analytics Pipeline: Python • MySQL • Power BI**

[![Python](https://img.shields.io/badge/Python-3.13-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data_Cleaning-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![MySQL](https://img.shields.io/badge/MySQL-EDA_&_SQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Power BI](https://img.shields.io/badge/Power_BI-Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-ETL-D71F00?style=for-the-badge&logo=sqlalchemy&logoColor=white)](https://www.sqlalchemy.org/)

*Uncovering revenue drivers, subscription impact, discount effectiveness, and customer loyalty segments across 3,900 retail transactions.*

</div>

---

## 📑 Table of Contents

- [Project Overview](#-project-overview)
- [Architecture & Workflow](#-architecture--workflow)
- [Repository Structure](#-repository-structure)
- [Data Dictionary](#-data-dictionary)
- [Data Cleaning & Feature Engineering (Python)](#-data-cleaning--feature-engineering-python)
- [Exploratory Data Analysis (MySQL)](#-exploratory-data-analysis-mysql)
- [Power BI Dashboard & Key Insights](#-power-bi-dashboard--key-insights)
- [How to Run Locally](#-how-to-run-locally)
- [Author & Connect](#-author--connect)

---

## 🎯 Project Overview

This project delivers a complete real-world data analytics workflow—from raw transactional data ingestion to executive-ready business intelligence. Using a dataset of **3,900 customer transactions**, the pipeline cleans and enriches the data in **Python**, loads it into a relational **MySQL** database for structured business querying, and visualizes core KPIs in an interactive **Power BI** dashboard.

### Core Business Questions Answered
- How does revenue break down across gender, age groups, and product categories?
- Do subscribed customers spend more than non-subscribers, and are repeat buyers more likely to subscribe?
- Which products rely most heavily on discounts, and which high-value customers still outspend the average when using discounts?
- How are customers distributed across **New**, **Returning**, and **Loyal** segments?

---

## 🏗️ Architecture & Workflow

```mermaid
flowchart LR
    A[("Raw CSV Dataset\n(3,900 rows, 18 cols)")] --> B["Python & Pandas\n• Median Imputation\n• Feature Engineering\n• Column Standardization"]
    B --> C["SQLAlchemy + PyMySQL\nETL Load"]
    C --> D[("MySQL Database\ncustomer table")]
    D --> E["SQL Business Queries\n• CTEs & Window Functions\n• Customer Segmentation"]
    D --> F["Power BI Dashboard\n• KPI Cards & Slicers\n• Interactive Visuals"]
    E --> G["Executive Presentation\n& Strategic Insights"]
    F --> G
```

---

## 📁 Repository Structure

| Folder / File | Description |
| :--- | :--- |
| `data/customer_shopping_behavior.csv` | Raw transactional dataset (3,900 records, 18 columns). |
| `data/customer_shopping_behavior_cleaned.csv` | Cleaned and feature-engineered dataset ready for BI and SQL. |
| `notebooks/customer_shopping_behavior_analysis.ipynb` | Jupyter Notebook covering EDA, missing value imputation, feature engineering, and MySQL ETL. |
| `sql/queries.sql` | 10 structured MySQL queries answering key business questions using CTEs, aggregations, and window functions. |
| `powerbi/customer_shopping_behavior.pbix` | Interactive Power BI Desktop dashboard file. |
| `powerbi/customer_shopping_behavior.pdf` | Static PDF export of the Power BI dashboard. |
| `powerbi/dashboard_preview.png` | High-resolution preview image of the Power BI dashboard. |
| `presentation/Customer_Shopping_Behavior_Analytics.pdf` | Executive slide deck summarizing the full analytics lifecycle and business recommendations. |
| `README.md` | Project documentation. |

---

## 📖 Data Dictionary

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `customer_id` | `INT` | Unique identifier for each customer transaction. |
| `age` | `INT` | Age of the customer. |
| `gender` | `VARCHAR` | Customer gender (`Male`, `Female`). |
| `item_purchased` | `VARCHAR` | Specific product purchased (e.g., Blouse, Sweater, Dress). |
| `category` | `VARCHAR` | Product category (`Clothing`, `Accessories`, `Footwear`, `Outerwear`). |
| `purchase_amount` | `INT` | Transaction value in USD (renamed from `Purchase Amount (USD)`). |
| `location` | `VARCHAR` | U.S. state where the purchase occurred. |
| `size` | `VARCHAR` | Product size (`S`, `M`, `L`, `XL`). |
| `color` | `VARCHAR` | Product color. |
| `season` | `VARCHAR` | Season of purchase (`Spring`, `Summer`, `Fall`, `Winter`). |
| `review_rating` | `FLOAT` | Customer rating (1.0–5.0); 37 missing values imputed via category median. |
| `subscription_status` | `VARCHAR` | Whether the customer has an active subscription (`Yes`, `No`). |
| `shipping_type` | `VARCHAR` | Delivery method (`Standard`, `Express`, `2-Day Shipping`, `Store Pickup`, etc.). |
| `discount_applied` | `VARCHAR` | Indicates if a discount was applied (`Yes`, `No`). |
| `previous_purchases` | `INT` | Total count of prior purchases by the customer. |
| `payment_method` | `VARCHAR` | Payment method used (`Venmo`, `Cash`, `Credit Card`, `Debit Card`, `PayPal`, etc.). |
| `frequency_of_purchases` | `VARCHAR` | Categorical shopping cadence (`Weekly`, `Bi-Weekly`, `Monthly`, `Quarterly`, `Annually`, etc.). |
| `age_groups` *(Engineered)* | `CATEGORY` | Quartile-based age segments (`Teenager`, `Adult`, `Middle_age`, `Old`). |
| `purchest_frequency_days` *(Engineered)* | `INT` | Numeric conversion of purchase frequency into days (`7`, `14`, `30`, `90`, `365`). |

---

## 🐍 Data Cleaning & Feature Engineering (Python)

Key preprocessing steps performed in `notebooks/customer_shopping_behavior_analysis.ipynb`:

1. **Missing Value Imputation:** Filled 37 null values in `Review Rating` using the **category-level median** to preserve distribution integrity and resist outliers.
2. **Schema Standardization:** Converted all column names to `snake_case` and renamed `purchase_amount_(usd)` to `purchase_amount`.
3. **Redundancy Removal:** Verified that `discount_applied` and `promo_code_used` were 100% identical across all rows and dropped `promo_code_used`.
4. **Feature Engineering:** Created quartile-based `age_groups` and mapped text frequencies to numeric `purchest_frequency_days`.
5. **Database Loading:** Exported the cleaned DataFrame directly to MySQL via `SQLAlchemy` and `PyMySQL`.

```python
import pandas as pd
from sqlalchemy import create_engine

# Impute missing review ratings with category-level median
df['Review Rating'] = df.groupby('Category')['Review Rating'].transform(
    lambda x: x.fillna(x.median())
)

# Standardize column names
df.columns = df.columns.str.lower().str.replace(" ", "_")
df = df.rename(columns={'purchase_amount_(usd)': 'purchase_amount'})

# Feature Engineering: Quartile Age Groups
df['age_groups'] = pd.qcut(
    df['age'], q=4, labels=['Teenager', 'Adult', 'Middle_age', 'Old']
)

# Drop redundant column
if (df['discount_applied'] == df['promo_code_used']).all():
    df.drop('promo_code_used', axis=1, inplace=True)

# Load cleaned data into MySQL
engine = create_engine("mysql+pymysql://root:password@localhost:3306/customer_behivior")
df.to_sql('customer', engine, if_exists='replace', index=False)
```

---

## 🗄️ Exploratory Data Analysis (MySQL)

Ten business-driven SQL queries were executed in `sql/queries.sql` to extract actionable insights.

### Example 1: Customer Loyalty Segmentation (CTE)
```sql
WITH cte AS (
    SELECT previous_purchases,
        CASE 
            WHEN previous_purchases = 1 THEN 'new' 
            WHEN previous_purchases BETWEEN 2 AND 10 THEN 'returning' 
            ELSE 'loyal'
        END AS segments
    FROM customer
)
SELECT segments, COUNT(*) AS count
FROM cte
GROUP BY segments;
```

### Example 2: Top 3 Most Purchased Products per Category (Window Function)
```sql
WITH cte AS (
    SELECT 
        category,
        item_purchased,
        COUNT(item_purchased) AS total_count,
        ROW_NUMBER() OVER (
            PARTITION BY category 
            ORDER BY COUNT(item_purchased) DESC
        ) AS rank_num
    FROM customer
    GROUP BY category, item_purchased
)
SELECT * 
FROM cte 
WHERE rank_num < 4;
```

---

## 📊 Power BI Dashboard & Key Insights

The interactive Power BI dashboard (`powerbi/customer_shopping_behavior.pbix`) provides dynamic filtering by **Subscription Status**, **Gender**, and **Category**.

### Executive KPIs
| Metric | Value |
| :--- | :---: |
| **Total Customers** | **3,900 (~4K)** |
| **Average Purchase Amount** | **$59.76** |
| **Average Review Rating** | **3.75 / 5.0** |
| **Subscription Rate** | **26.88% Yes** / **73.12% No** |

### Key Takeaways & Recommendations
- **Clothing Dominates Revenue & Volume:** Clothing leads both sales volume and total revenue (exceeding $100K), followed by Accessories, Footwear, and Outerwear. Prioritize inventory depth and cross-selling bundles around Clothing and Accessories.
- **Untapped Subscription Opportunity:** With **73.12%** of customers currently unsubscribed, converting repeat buyers (>5 previous purchases) through targeted subscription perks (e.g., free Express shipping or exclusive discounts) represents a major recurring-revenue lever.
- **Balanced Age Demographics:** Revenue is led by the **Teenager** and **Middle_age** cohorts, closely followed by **Adult** and **Old**, indicating broad demographic appeal that warrants tailored seasonal campaigns per age bracket.

---

![Customer Behavior Dashboard Preview](powerbi/dashboard_preview.png)
*Click the image above or [view the full Dashboard PDF here](powerbi/customer_shopping_behavior.pdf).*

## 🚀 How to Run Locally

1. **Clone the repository**
   ```bash
   git clone [https://github.com/hamzaX12/customer-shopping-behavior-analytics.git](https://github.com/hamzaX12/customer-shopping-behavior-analytics.git)
   cd customer-shopping-behavior-analytics
   ```
2. **Install Python dependencies**
   ```bash
   pip install pandas sqlalchemy pymysql jupyter
   ```
3. **Run the ETL Notebook**
   - Update your MySQL credentials in `notebooks/customer_shopping_behavior_analysis.ipynb`.
   - Execute all cells to clean the data and populate the `customer` table in MySQL.
4. **Run SQL Queries & Open Dashboard**
   - Execute `sql/queries.sql` in MySQL Workbench.
   - Open `powerbi/customer_shopping_behavior.pbix` in Power BI Desktop to explore the interactive visuals.

---

## 👨‍💻 Author & Connect

<div align="center">

**Hamza Ben Allou**  
*Data Scientist | Data Analyst | BI Engineer*

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/hamza-ben-allou-48ab31236)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/hamzaX12)

</div>
