# <div align="center">

# 

# \# 🛍️ Customer Shopping Behavior Analytics

# 

# \*\*An End-to-End Retail Data Analytics Pipeline: From Raw Data to Executive Insights\*\*

# 

# \[!\[Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge\&logo=python\&logoColor=white)](https://www.python.org/)

# \[!\[Pandas](https://img.shields.io/badge/Pandas-Data%20ETL-150458?style=for-the-badge\&logo=pandas\&logoColor=white)](https://pandas.pydata.org/)

# \[!\[MySQL](https://img.shields.io/badge/MySQL-SQL%20Analytics-4479A1?style=for-the-badge\&logo=mysql\&logoColor=white)](https://www.mysql.com/)

# \[!\[Power BI](https://img.shields.io/badge/Power%20BI-Interactive%20Dashboard-F2C811?style=for-the-badge\&logo=powerbi\&logoColor=black)](https://powerbi.microsoft.com/)

# \[!\[Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge\&logo=jupyter\&logoColor=white)](https://jupyter.org/)

# 

# \*Uncovering revenue drivers, subscription dynamics, discount behavior, and customer loyalty segments across 3,900 retail transactions.\*

# 

# \[Explore Dashboard](#-key-insights--recommendations) • \[View SQL Queries](#-sql-analytical-framework) • \[Project Architecture](#-project-architecture) • \[Connect With Me](#-author--connect)

# 

# </div>

# 

# \---

# 

# \## 📑 Table of Contents

# 

# \- \[Project Overview](#-project-overview)

# \- \[Project Architecture](#-project-architecture)

# \- \[Repository Structure](#-repository-structure)

# \- \[Data Dictionary](#-data-dictionary)

# \- \[ETL \& Feature Engineering (Python)](#-etl--feature-engineering-python)

# \- \[SQL Analytical Framework (MySQL)](#-sql-analytical-framework-mysql)

# \- \[Key Insights \& Recommendations](#-key-insights--recommendations)

# \- \[How to Run This Project](#-how-to-run-this-project)

# \- \[Author \& Connect](#-author--connect)

# 

# \---

# 

# \## 🎯 Project Overview

# 

# Modern retail teams need clear visibility into what drives customer spending, how promotions impact order value, and which demographics convert into loyal subscribers. This project demonstrates a complete, real-world data analytics lifecycle:

# 

# 1\. \*\*Business Requirements:\*\* Defined 10 core retail questions spanning revenue concentration, subscription value, shipping preferences, discount impact, and customer loyalty.

# 2\. \*\*Data Cleaning \& Feature Engineering (Python):\*\* Audited 3,900 transactions, imputed missing review ratings using category medians, removed redundant attributes, and engineered demographic and purchase-frequency features.

# 3\. \*\*Database Integration \& Querying (MySQL):\*\* Automated data loading via SQLAlchemy and executed 10 structured SQL queries using CTEs, subqueries, and window functions.

# 4\. \*\*Business Intelligence \& Storytelling (Power BI):\*\* Built an interactive executive dashboard with dynamic slicers and compiled findings into a stakeholder presentation.

# 

# \---

# 

# \## 🏗️ Project Architecture

# 

# ```mermaid

# flowchart LR

# &#x20;   A\[("📄 Raw Data<br/>customer\_shopping\_behavior.csv<br/>(3,900 Rows × 18 Cols)")] --> B\["🐍 Python ETL<br/>Pandas \& Jupyter<br/>• Median Imputation<br/>• Feature Engineering<br/>• Schema Normalization"]

# &#x20;   B --> C\[("🗄️ MySQL Database<br/>SQLAlchemy + PyMySQL<br/>Table: customer")]

# &#x20;   C --> D\["🔍 SQL Analytics<br/>queries.sql<br/>• 10 Business Queries<br/>• CTEs \& Window Functions"]

# &#x20;   C --> E\["📊 Power BI Dashboard<br/>customer\_shopping\_behavior.pbix<br/>• KPIs \& Interactive Slicers"]

# &#x20;   D --> F\["📑 Executive Strategy<br/>Presentation Deck<br/>Actionable Recommendations"]

# &#x20;   E --> F

# ```

# 

# \---

# 

# \## 📂 Repository Structure

# 

# | Folder / File | Type | Description |

# | :--- | :--- | :--- |

# | `data/customer\_shopping\_behavior.csv` | Raw Data | Original dataset containing 3,900 customer transactions and 18 attributes. |

# | `data/customer\_shopping\_behavior\_cleaned.csv` | Processed Data | Cleaned, standardized dataset with engineered features ready for BI/SQL. |

# | `notebooks/customer\_shopping\_behavior\_analysis.ipynb` | Jupyter Notebook | End-to-end Python script for EDA, imputation, feature engineering, and MySQL upload. |

# | `sql/queries.sql` | SQL Script | 10 structured MySQL queries answering key business and segmentation questions. |

# | `powerbi/customer\_shopping\_behavior.pbix` | Power BI File | Interactive BI dashboard with KPIs, category breakdowns, and dynamic filters. |

# | `powerbi/customer\_shopping\_behavior.pdf` | Dashboard Export | Static PDF snapshot of the Power BI executive dashboard. |

# | `presentation/Customer\_Shopping\_Behavior\_Analytics.pdf` | Slide Deck | Executive presentation covering the full analytics lifecycle and strategy. |

# | `README.md` | Documentation | Comprehensive project documentation and setup guide. |

# 

# \---

# 

# \## 📖 Data Dictionary

# 

# The dataset contains \*\*3,900 unique customer records\*\*. Below is the schema after Python preprocessing and feature engineering:

# 

# | Column Name | Data Type | Source | Description |

# | :--- | :--- | :--- | :--- |

# | `customer\_id` | `INT` | Raw | Unique identifier for each customer transaction. |

# | `age` | `INT` | Raw | Customer age in years. |

# | `gender` | `VARCHAR` | Raw | Customer gender (`Male`, `Female`). |

# | `item\_purchased` | `VARCHAR` | Raw | Specific product bought (e.g., Blouse, Sweater, Dress). |

# | `category` | `VARCHAR` | Raw | Product category (`Clothing`, `Accessories`, `Footwear`, `Outerwear`). |

# | `purchase\_amount` | `INT` | Renamed | Transaction value in USD (renamed from `Purchase Amount (USD)`). |

# | `location` | `VARCHAR` | Raw | US state where the purchase occurred. |

# | `size` | `VARCHAR` | Raw | Apparel size (`S`, `M`, `L`, `XL`). |

# | `color` | `VARCHAR` | Raw | Product color variant. |

# | `season` | `VARCHAR` | Raw | Season of purchase (`Winter`, `Spring`, `Summer`, `Fall`). |

# | `review\_rating` | `FLOAT` | Cleaned | Customer rating (1.0–5.0); 37 nulls imputed using category median. |

# | `subscription\_status` | `VARCHAR` | Raw | Loyalty subscription indicator (`Yes`, `No`). |

# | `shipping\_type` | `VARCHAR` | Raw | Fulfillment method (`Express`, `Standard`, `2-Day Shipping`, `Store Pickup`, etc.). |

# | `discount\_applied` | `VARCHAR` | Raw | Whether a discount was applied (`Yes`, `No`). \*(`promo\_code\_used` dropped due to 100% redundancy).\* |

# | `previous\_purchases` | `INT` | Raw | Total count of prior historical purchases by the customer. |

# | `payment\_method` | `VARCHAR` | Raw | Payment channel used (`Venmo`, `Cash`, `Debit Card`, `Credit Card`, `PayPal`, etc.). |

# | `frequency\_of\_purchases` | `VARCHAR` | Raw | Categorical shopping cadence (`Weekly`, `Fortnightly`, `Monthly`, `Annually`, etc.). |

# | `age\_groups` | `CATEGORY` | \*\*Engineered\*\* | Quartile-based age segments (`Teenager`, `Adult`, `Middle\_age`, `Old`). |

# | `purchest\_frequency\_days` | `INT` | \*\*Engineered\*\* | Numeric mapping of purchase frequency in days (`7` to `365`). |

# 

# \---

# 

# \## 🐍 ETL \& Feature Engineering (Python)

# 

# Key preprocessing steps executed in `customer\_shopping\_behavior\_analysis.ipynb`:

# 

# ```python

# import pandas as pd

# from sqlalchemy import create\_engine

# 

# \# 1. Load dataset \& impute missing Review Ratings with Category median

# df = pd.read\_csv("../data/customer\_shopping\_behavior.csv")

# df\["Review Rating"] = df.groupby("Category")\["Review Rating"].transform(

# &#x20;   lambda x: x.fillna(x.median())

# )

# 

# \# 2. Standardize column names to snake\_case

# df.columns = df.columns.str.lower().str.replace(" ", "\_")

# df = df.rename(columns={"purchase\_amount\_(usd)": "purchase\_amount"})

# 

# \# 3. Feature Engineering: Age Quartiles \& Numeric Purchase Frequency

# df\["age\_groups"] = pd.qcut(

# &#x20;   df\["age"], q=4, labels=\["Teenager", "Adult", "Middle\_age", "Old"]

# )

# 

# frequency\_mapping = {

# &#x20;   "Weekly": 7, "Bi-Weekly": 14, "Fortnightly": 14,

# &#x20;   "Monthly": 30, "Quarterly": 90, "Every 3 Months": 90, "Annually": 365

# }

# df\["purchest\_frequency\_days"] = df\["frequency\_of\_purchases"].map(frequency\_mapping)

# 

# \# 4. Drop redundant column (100% identical to discount\_applied)

# if (df\["discount\_applied"] == df\["promo\_code\_used"]).all():

# &#x20;   df.drop("promo\_code\_used", axis=1, inplace=True)

# 

# \# 5. Export cleaned dataset directly into MySQL

# engine = create\_engine("mysql+pymysql://root:password@localhost:3306/customer\_behivior")

# df.to\_sql("customer", engine, if\_exists="replace", index=False)

# ```

# 

# \---

# 

# \## 🔍 SQL Analytical Framework (MySQL)

# 

# Ten targeted business queries were developed in `sql/queries.sql` to extract actionable metrics. Below are two highlights showcasing \*\*CTEs\*\* and \*\*Window Functions\*\*:

# 

# \### Customer Loyalty Segmentation (Q7)

# ```sql

# WITH customer\_tiers AS (

# &#x20;   SELECT

# &#x20;       previous\_purchases,

# &#x20;       CASE

# &#x20;           WHEN previous\_purchases = 1 THEN 'New'

# &#x20;           WHEN previous\_purchases BETWEEN 2 AND 10 THEN 'Returning'

# &#x20;           ELSE 'Loyal'

# &#x20;       END AS segments

# &#x20;   FROM customer

# )

# SELECT

# &#x20;   segments,

# &#x20;   COUNT(\*) AS customer\_count

# FROM customer\_tiers

# GROUP BY segments;

# ```

# 

# \### Top 3 Most Purchased Products per Category (Q8)

# ```sql

# WITH ranked\_products AS (

# &#x20;   SELECT

# &#x20;       category,

# &#x20;       item\_purchased,

# &#x20;       COUNT(item\_purchased) AS total\_count,

# &#x20;       ROW\_NUMBER() OVER (

# &#x20;           PARTITION BY category

# &#x20;           ORDER BY COUNT(item\_purchased) DESC

# &#x20;       ) AS rank\_num

# &#x20;   FROM customer

# &#x20;   GROUP BY category, item\_purchased

# )

# SELECT category, item\_purchased, total\_count, rank\_num

# FROM ranked\_products

# WHERE rank\_num <= 3;

# ```

# 

# \---

# 

# \## 📊 Key Insights \& Recommendations

# 

# \### Baseline KPIs

# \* \*\*Total Customers:\*\* `3,900`

# \* \*\*Average Purchase Amount:\*\* `$59.76`

# \* \*\*Average Review Rating:\*\* `3.75 / 5.00`

# \* \*\*Subscription Rate:\*\* `26.88%` Subscribed vs. `73.12%` Non-Subscribed

# 

# \### Strategic Findings \& Actions

# 1\. \*\*Close the 73.12% Subscription Gap:\*\* Nearly three-quarters of shoppers are non-subscribers. Launch targeted loyalty enrollment campaigns aimed at repeat buyers (`previous\_purchases > 5`) who already trust the brand.

# 2\. \*\*Prioritize Core Revenue Categories:\*\* \*\*Clothing (\~$104K)\*\* and \*\*Accessories (\~$74K)\*\* generate \*\*\~77% of total revenue\*\*, significantly outperforming Footwear (\~$36K) and Outerwear (\~$18K). Focus seasonal inventory and cross-sell bundles around these core lines.

# 3\. \*\*Target High-Value Age Cohorts:\*\* The \*\*Teenager (\~$62K)\*\* and \*\*Middle-Age (\~$59K)\*\* quartiles lead overall revenue contribution. Tailor digital marketing and promo strategies specifically to these top-performing segments.

# 4\. \*\*Optimize Discount Margins:\*\* Use the SQL discount-sensitivity queries (Q2 \& Q6) to identify high-spending customers who still purchase above the `$59.76` average and restrict blanket discounts on naturally high-demand items.

# 

# \---

# 

# \## 🚀 How to Run This Project

# 

# 1\. \*\*Clone the repository:\*\*

# &#x20;  ```bash

# &#x20;  git clone https://github.com/hamzaX12/customer-shopping-behavior-analytics.git

# &#x20;  cd customer-shopping-behavior-analytics

# &#x20;  ```

# 

# 2\. \*\*Install Python dependencies:\*\*

# &#x20;  ```bash

# &#x20;  pip install pandas sqlalchemy pymysql jupyter

# &#x20;  ```

# 

# 3\. \*\*Run the ETL Pipeline:\*\*

# &#x20;  \* Create a local MySQL database named `customer\_behivior`.

# &#x20;  \* Update your MySQL credentials in `notebooks/customer\_shopping\_behavior\_analysis.ipynb` and run all cells to clean the data and populate the `customer` table.

# 

# 4\. \*\*Execute SQL Analysis \& Explore Power BI:\*\*

# &#x20;  \* Run `sql/queries.sql` in MySQL Workbench or your preferred SQL client.

# &#x20;  \* Open `powerbi/customer\_shopping\_behavior.pbix` in Power BI Desktop to interact with the dashboard.

# 

# \---

# 

# \## 👤 Author \& Connect

# 

# \*\*Hamza Ben Allou\*\*

# 

# \[!\[LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge\&logo=linkedin\&logoColor=white)](https://www.linkedin.com/in/hamza-ben-allou-48ab31236)

# \[!\[GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=for-the-badge\&logo=github\&logoColor=white)](https://github.com/hamzaX12)

# 

# \*If you found this project helpful, feel free to star the repository or reach out on LinkedIn!\*

