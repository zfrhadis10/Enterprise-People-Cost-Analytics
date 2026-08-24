# 💼 Enterprise People Cost & Workforce Expenditure Analytics (2023–2024)
### End-to-End HR Cost Control & Budget Variance Analysis

![Power BI](https://img.shields.io/badge/Power_BI-Dashboard-F2C811?style=flat-square&logo=powerbi&logoColor=black)
![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat-square&logo=python&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-Financial_Metrics-217346?style=flat-square&logo=microsoftexcel&logoColor=white)
![Data Analytics](https://img.shields.io/badge/Data_Analytics-Insights-4B8BBE?style=flat-square)
![People Analytics](https://img.shields.io/badge/People_Analytics-HR-6A4C93?style=flat-square)
![HR Analytics](https://img.shields.io/badge/HR_Analytics-Workforce-00A896?style=flat-square)
![Data Cleaning](https://img.shields.io/badge/Data_Cleaning-Pandas_%2F_NumPy-F77F00?style=flat-square)
![Dashboard](https://img.shields.io/badge/Dashboard-Executive-118AB2?style=flat-square)

**Repository Description:** People Cost & Workforce Expenditure Analytics built with Python & Power BI. Features DAX financial variance measures and executive budget optimization insights across 1,700+ payroll records.

---

## 🚀 Project Overview

This project delivers an enterprise-grade analytics platform designed to monitor, analyze, and optimize **People Cost (Workforce Expenditure)** for a large-scale enterprise operating in Indonesia.

Processing over **1,728 aggregated payroll and headcount transaction records** across **8 operational divisions** and **9 cost components** over a 24-month period (2023–2024), this solution translates complex HR financial data into an interactive executive decision-making system.

### Key Analytical Deliverables:
* **Data Audit & Cleansing:** Automated Python ETL scripts (Pandas & NumPy).
* **Financial DAX Measures:** Time Intelligence, dynamic KPI measures, and variance calculations.
* **Interactive Power BI Dashboard:** Built with a minimal corporate **Navy theme Palette** (`#163F81`).
* **Strategic Cost Control Insights:** Data-backed recommendations for executive management.

---

## 📊 Interactive Dashboard Preview

<p align="center">
  <img src="https://github.com/zfrhadis10/Enterprise-People-Cost-Analytics/blob/main/images/dashboard%20preview_1.png" alt="Dashboard Preview 1" width="45%">
  <img src="https://github.com/zfrhadis10/Enterprise-People-Cost-Analytics/blob/main/images/dashboard%20preview_2.png" alt="Dashboard Preview 2" width="45%">
</p>

<p align="center">
  <b>Executive Dashboard: Workforce Expenditure, Budget Variance & Cost Optimization Analysis</b>
</p>
---

## 🔢 Executive Summary & Key Quantitative Metrics

| Metric Category | Realized Metric (2023–2024) | Benchmark / Target | Variance / Gap |
| :--- | :--- | :--- | :--- |
| **Total Realized Expenditure** | **IDR 1,157.1 Billion** | IDR 1,117.6 Billion (Budget) | **+IDR 39.5 Billion (+3.5%)** |
| **Average Monthly Expenditure**| **IDR 48.2 Billion / Month** | IDR 46.5 Billion / Month | **+IDR 1.64 Billion / Month** |
| **Average Headcount** | **39,814 Employees** | 40,000 Employees | -186 Employees (-0.46%) |
| **Cost Per Head (CPH)** | **IDR 1.21 Million / Head / Mo** | IDR 1.16 Million / Head / Mo | **+4.31% Cost Elevation** |
| **Highest Seasonal Spike** | **IDR 62.0 Billion (Sep/Bonus)** | IDR 49.0 Billion (Budget) | **+26.5% Budget Variance** |
| **Secondary Seasonal Spike** | **IDR 58.0 Billion (Mar/THR)** | IDR 46.0 Billion (Budget) | **+26.0% Budget Variance** |

---

## 🎯 Business Problem & Core Challenges

* **Fragmented Cost Center Visibility:** Salaries, variable allowances, overtime, BPJS contributions, THR, and annual performance bonuses were recorded across disparate operational ledgers.
* **Seasonal Budget Overruns:** Lack of predictive visibility into peak months (THR in Q1/Q2 and Year-End Bonuses in Q3/Q4) led to severe monthly liquidity pressures.
* **Divisional Efficiency Disparities:** Inability to evaluate **Cost Per Head (CPH)** efficiency across high-headcount divisions (Manufacturing) vs. high-salary divisions (IT & Sales).

---

## 🏗️ Data Architecture & Workflow

```text
Raw Datasets (CSV / Excel)
│
├── fmcg_workforce_cost_dataset.csv  (1,728 rows | Jan 2023 - Dec 2024)
│
▼
Python Ingestion & Cleansing Layer (Pandas)
├── Structural Integrity & Missing Value Audit
├── Standardizing Category Names & Outlier Treatment
└── Data Validation & Type Casting
│
▼
Power BI Data Model
├── Table : fmcg_workforce_cost_dataset
└── Custom DAX Measures (Total Actual, Total Budget, Variance %, Cost per Headcount)
│
▼
Analytics & Visualization Layer
├── KPI Cards, Line Chart, Pie Chart, Treemap, Pivot Table
└── Executive Dashboard (Navy Corporate Aesthetic)
```

---

## 🛠️ Complete Technical Implementation

### 1. Data Processing & Cleaning (Python Script)

```python
import pandas as pd
import numpy as np

# Ingest Raw Dataset
df = pd.read_csv('dataset/fmcg_workforce_cost_dataset.csv')

# Data Cleansing & Validation
df['Division'] = df['Division'].str.strip().str.title()
df['Category'] = df['Category'].str.strip().str.title()
df['Date'] = pd.to_datetime(df['Date'])

# Handling Anomalies & Zero-Values
df['Actual_IDR'] = np.where(df['Actual_IDR'] < 0, 0, df['Actual_IDR'])
df['Budget_IDR'] = np.where(df['Budget_IDR'] < 0, 0, df['Budget_IDR'])

# Export Cleaned Fact Table
df.to_csv('dataset/cleaned_workforce_cost.csv', index=False)
```

### 2. Core DAX Measures

```dax
Total Actual = SUM(fmcg_workforce_cost_dataset[Actual_IDR])

Total Budget = SUM(fmcg_workforce_cost_dataset[Budget_IDR])

Total Variance IDR = [Total Actual] - [Total Budget]

Variance % = 
DIVIDE(
    [Total Variance IDR],
    [Total Budget],
    0
)
```

**Time Intelligence (Year-Over-Year Growth):**

```dax
Actual YoY Growth (%) = 
VAR CurrentPeriod = [Total Actual]
VAR PreviousPeriod = CALCULATE([Total Actual], SAMEPERIODLASTYEAR(fmcg_workforce_cost_dataset[Date]))
RETURN
DIVIDE(CurrentPeriod - PreviousPeriod, PreviousPeriod, 0)
```

**Cost Per Headcount:**

```dax
Cost per Headcount = 
DIVIDE(
    [Total Actual],
    AVERAGE(fmcg_workforce_cost_dataset[Headcount]),
    0
)
```

---

## 📈 Divisional Breakdown & Cost Distribution

| Division | Realized Spend (IDR B) | % Share of Total | Headcount | Cost Per Head (IDR M/Mo) | Variance Status |
| --- | --- | --- | --- | --- | --- |
| **Manufacturing & Plant** | **578.5** | 50.0% | 22,100 | 1.09 | 🟡 Over Budget (+2.8%) |
| **Sales & Distribution** | **208.3** | 18.0% | 8,200 | 1.06 | 🟢 On Budget (+0.5%) |
| **Supply Chain & Logistics** | **127.3** | 11.0% | 4,500 | 1.18 | 🟢 On Budget (-0.8%) |
| **Information Technology** | **81.0** | 7.0% | 1,800 | 1.88 | 🔴 Over Budget (+8.4%) |
| **Marketing & Brand** | **69.4** | 6.0% | 1,200 | 2.41 | 🔴 Over Budget (+6.2%) |
| **Finance & Accounting** | **34.7** | 3.0% | 800 | 1.81 | 🟢 On Budget (-1.2%) |
| **Human Resources** | **34.7** | 3.0% | 750 | 1.93 | 🟢 On Budget (-0.4%) |
| **Research & Development** | **23.1** | 2.0% | 464 | 2.07 | 🟡 Over Budget (+3.1%) |

---

## 🔍 Analytical Findings & Strategic Insights

* **Seasonal Budget Volatility:**
  * **THR Allowance Peak (March 2024):** Actual spend reached **IDR 58.0B** vs budget of **IDR 46.0B** (+26.0% variance).
  * **Year-End Bonus Peak (September 2024):** Actual spend reached **IDR 62.0B** vs budget of **IDR 49.0B** (+26.5% variance).
  * *Root Cause:* Flat linear budgeting (IDR 45B–52B/month) failed to account for legally required holiday allowances and performance bonuses.

* **Overtime Variance in Operations:**
  * Manufacturing overtime surged by **+18.4% YoY**, representing **IDR 14.2 Billion** in excess unbudgeted costs, driven by Q3 production scale-ups.

* **High CPH Escalation in Specialized Talent:**
  * IT and Marketing exhibit the highest Cost Per Head metrics (**IDR 1.88M** and **IDR 2.41M/month** respectively), largely driven by retention bonuses and external consultant allowances.

---

## 💡 Strategic Business Recommendations

* **Implement Amortized Accrual Budgeting:** Replace static flat monthly budgets with an **annualized accrual model**, allocating ~8.33% of anticipated THR and bonus pools each month to remove artificial monthly budget deficits.
* **Overtime Caps & Automated Threshold Alerts:** Establish dynamic shift-level overtime triggers in Manufacturing when operational output exceeds 85% capacity, capping unauthorized overtime spend.
* **Band-Based CPH Governance for Tech & Marketing:** Introduce standardized compensation bands for specialized roles to curb unforecasted salary and variable allowance inflation.

---

## 📂 Repository Structure

```text
enterprise-people-cost-analytics/
│
├── Workforce_Cost_Analytics.pbix        # Interactive Power BI Report
├── FMCG_Workforce_Cost_Notebook.ipynb   # Data Cleaning & Validation Notebook
├── fmcg_workforce_cost_dataset.csv      # Synthetic Enterprise Dataset
├── images/
│   └── dashboard preview_1.png          # High-Res Dashboard Preview
    └── dashboard preview_2.png
└── README.md                            # Project Documentation
```

---

## 👤 Author

**Zafirah Aida Adista**

*Data Analytics & BI Professional*

📧 [zafirah.adistaa@gmail.com](mailto:zafirah.adistaa@gmail.com)
