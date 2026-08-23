# 💼 Enterprise People Cost & Workforce Expenditure Analytics (2023–2024)
### End-to-End HR Cost Control, Data Pipeline & Budget Variance Monitoring System

**Repository Name:** `enterprise-people-cost-analytics`
**Repository Description:** End-to-end People Cost & Workforce Expenditure Analytics platform built with Python & Power BI. Features DAX financial variance modeling, Star Schema data architecture, and executive budget optimization insights across 1,700+ payroll records.
**Topics / Tags:** `power-bi` | `python` | `dax` | `data-analytics` | `people-analytics` | `hr-analytics` | `star-schema` | `etl-pipeline` | `dashboard`

---

## 🚀 Project Overview

This project delivers an enterprise-grade analytics platform designed to monitor, analyze, and optimize **People Cost (Workforce Expenditure)** for a large-scale enterprise operating in Indonesia.

Processing over **1,728 aggregated payroll and headcount transaction records** across **8 operational divisions** and **9 cost components** over a 24-month period (2023–2024), this solution translates complex HR financial data into an interactive executive decision-making system.

### Key Analytical Deliverables:
* **Data Audit & Cleansing:** Automated Python ETL scripts (Pandas & NumPy).
* **Relational Data Modeling:** Optimized Star Schema architecture.
* **Advanced Financial DAX:** Time Intelligence, dynamic KPI measures, and variance modeling.
* **Interactive Power BI Dashboard:** Built with a minimal corporate **Navy theme Palette** (`#163F81`).
* **Strategic Cost Control Insights:** Data-backed recommendations for executive management.

---

## 📊 Interactive Dashboard Preview

![2024 Monthly Workforce Expenditure Trend](dashboard_preview.png)

<p align="center">
  <b>Executive Overview: Budget Allocation vs. Realized Workforce Expenditure (2024 Trend)</b>
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

## 🏗️ Data Architecture & Pipeline

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
Power BI Dimensional Engine (Star Schema)
├── Fact Table : Fact_WorkforceCost
├── Dim Tables : Dim_Division, Dim_Category, Dim_Date
└── Relationships: 1-to-Many (1:*), Single Direction Filter
│
▼
Analytics & Visualization Layer
├── Financial DAX Calculation Engine
├── Field Parameters for Dynamic Metric Toggling
└── Executive Dashboard (Navy Corporate Aesthetic)
```

---

## 🛠️ Complete Technical Implementation

### 1. Data Processing & ETL Pipeline (Python Script)

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

### 2. Star Schema Data Modeling Topology

* **`Fact_WorkforceCost`**: `Transaction_ID` (PK), `Date` (FK), `Division_ID` (FK), `Category_ID` (FK), `Actual_IDR`, `Budget_IDR`, `Headcount`
* **`Dim_Division`**: `Division_ID` (PK), `Division_Name`, `Division_Head`, `Operational_Unit`
* **`Dim_Category`**: `Category_ID` (PK), `Category_Name`, `Expense_Type` (Fixed/Variable)
* **`Dim_Date`**: `Date` (PK), `Year`, `Month_Name`, `Month_Number`, `Quarter`, `Is_Peak_Month`

---

## ⚙️ Core DAX Formulations

### 1. Actual vs. Budget Monetary Variance

```dax
Actual Expenditure (IDR) = SUM(Fact_WorkforceCost[Actual_IDR])

Budget Allocation (IDR) = SUM(Fact_WorkforceCost[Budget_IDR])

Variance (IDR) = [Actual Expenditure (IDR)] - [Budget Allocation (IDR)]

Variance (%) = 
DIVIDE(
    [Variance (IDR)],
    [Budget Allocation (IDR)],
    0
)
```

### 2. Time Intelligence (Year-Over-Year Expenditure Growth)

```dax
Actual YoY Growth (%) = 
VAR CurrentPeriod = [Actual Expenditure (IDR)]
VAR PreviousPeriod = CALCULATE([Actual Expenditure (IDR)], SAMEPERIODLASTYEAR('Dim_Date'[Date]))
RETURN
DIVIDE(CurrentPeriod - PreviousPeriod, PreviousPeriod, 0)
```

### 3. Normalized Cost Per Head (CPH)

```dax
Cost Per Head (CPH) = 
DIVIDE(
    [Actual Expenditure (IDR)],
    AVERAGE(Fact_WorkforceCost[Headcount]),
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
├── dataset/
│   └── fmcg_workforce_cost_dataset.csv  # Synthetic Enterprise Dataset
├── images/
│   └── dashboard_preview.png            # High-Res Dashboard Preview
└── README.md                            # Project Documentation
```

---

## 👤 Author

**Zafirah Aida Adista**

*Data Analytics & BI Professional*

📧 [zafirah.adistaa@gmail.com](mailto:zafirah.adistaa@gmail.com)
