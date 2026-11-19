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
    D --> E["SQL
