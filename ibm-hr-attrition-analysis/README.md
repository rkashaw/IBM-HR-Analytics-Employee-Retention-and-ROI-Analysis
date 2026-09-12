# IBM HR Analytics: Employee Retention & ROI Analysis

A 3-month internship project analyzing the IBM HR Employee Attrition dataset to quantify the **financial cost of employee attrition** and surface retention insights through a Databricks pipeline and Power BI dashboard.

## Project Overview

Employee attrition isn't just an HR metric — it's a fiscal one. This project builds a small data pipeline that:

1. Ingests the raw IBM HR Attrition dataset
2. Engineers a **fiscal impact / attrition cost** metric (estimated at ~30% of an employee's annual salary per departure — a common industry replacement-cost benchmark)
3. Structures the data into a **Fact / Dimension model** (Gold layer) for analytics
4. Feeds a **Power BI dashboard** for stakeholder-facing reporting
5. Runs quartile analysis on income distribution to support compensation/retention insights

## Repo Structure

```
├── data/
│   └── WA_Fn-UseC_-HR-Employee-Attrition.csv   # Raw IBM HR Analytics dataset (1,470 employees)
├── notebooks/
│   └── attrition_cost_analysis.ipynb           # Databricks (PySpark) ETL + analysis notebook
├── powerbi/
│   └── hr_attrition_dashboard.pbix             # Power BI dashboard built on the Gold tables
└── README.md
```

## Pipeline Summary

**Bronze → Silver → Gold (Databricks / PySpark + Unity Catalog)**

- **Bronze:** Raw HR attrition data loaded into a Spark table
- **Silver:** Selected core fields (Employee ID, Age, Department, Job Role, Monthly Income, Attrition, Tenure) and engineered `attrition_cost` — for every employee who left, cost is calculated as `MonthlyIncome * 12 * 0.30`
- **Gold:**
  - `gold_fact_attrition` — fact table with employee ID, monthly income, and fiscal impact (USD)
  - `gold_dim_employee` — dimension table with department, job role, age, and tenure
- **Analysis:** Quartile breakdown of `MonthlyIncome` (Q1 ≈ 2,911 / Q3 ≈ 8,380, rounded to 4,000 / 8,000 for banding) to segment income tiers for reporting

## Dataset

[IBM HR Analytics Employee Attrition & Performance](https://www.ibm.com/communities/analytics/watson-analytics-blog/hr-employee-attrition/) — a fictional dataset created by IBM data scientists, containing 1,470 employee records across 35 attributes (demographics, compensation, satisfaction scores, tenure, etc.).

## Tools Used

- **Databricks** (PySpark, Unity Catalog, Delta Lake) — data engineering & transformation
- **Power BI** — dashboarding and visualization
- **Python** — analysis

## How to Run

1. Upload `data/WA_Fn-UseC_-HR-Employee-Attrition.csv` to your Databricks workspace as a table (e.g. `workspace.default.ibm_raw_data`)
2. Run `notebooks/attrition_cost_analysis.ipynb` on a Databricks cluster with Unity Catalog enabled
3. Open `powerbi/hr_attrition_dashboard.pbix` in Power BI Desktop and point it at the resulting Gold tables (or the CSV directly, for a standalone view)

## Notes

- The 30% attrition-cost multiplier is a standard industry rule-of-thumb for replacement cost (recruiting, onboarding, lost productivity), not a value derived from this dataset itself.
- This was built as part of a 3-month internship project for learning purposes — not a production pipeline.

## License

This project is shared for portfolio/educational purposes. The underlying dataset is publicly released by IBM for analytics practice.
