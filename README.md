# 🚀 dbt + Databricks Medallion Architecture (ELT Pipeline)

![dbt](https://img.shields.io/badge/dbt-FF694B?style=for-the-badge&logo=dbt&logoColor=white)
![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![ELT](https://img.shields.io/badge/Architecture-Medallion-blue?style=for-the-badge)

---

## 📖 Project Overview

This project implements a production-style **ELT pipeline** using **dbt Core** integrated with **Databricks (Unity Catalog)**, following the **Medallion Architecture (Bronze → Silver → Gold)**.

It demonstrates:

- Modular layered transformations
- SCD Type 2 implementation
- Automated data validation
- Schema management using macros
- Version-controlled reference data (dbt seeds)
- Warehouse-native transformations (ELT)
- End-to-end analytics-ready data modeling

---

# 🏗️ Architecture

## 📸 Unity Catalog Setup

<img src="./assets/unity-catalog-setup.png" width="1000"/>

---

## 🥉 Bronze Layer — Raw Ingestion

<img src="./assets/bronze-layer-model.png" width="1000"/>

- Direct references to Unity Catalog source tables  
- Minimal transformation  
- Column standardization  
- Materialized as **views**

**Goal:** Preserve trusted raw data.

---

## 🥈 Silver Layer — Cleaned & Historical (SCD Type 2)

<img src="./assets/silver-layer-transformations.png" width="1000"/>

- Standardized and joined datasets  
- Fact + dimension modeling  
- Deduplication logic  
- Implemented **Slowly Changing Dimension Type 2**  
- Tracks:
  - `effective_start_date`
  - `effective_end_date`
  - `is_current`
- Materialized as **views/tables**

**Goal:** Maintain clean, history-aware analytical datasets.

---

## 🧪 dbt Test Execution

<img src="./assets/dbt-test-results.png" width="1000"/>

- Implemented built-in tests: `not_null`, `unique`, `accepted_values`
- Created custom generic test: `generic_non_negative`
- Automated validation during `dbt test`

---

## ⚙️ dbt Run Output

<img src="./assets/dbt-run-output.png" width="1000"/>

- Successfully executed layered models
- Verified dependency graph via `ref()`
- Full pipeline execution with `dbt run`

---

## 🥇 Gold Layer — Analytics & KPI Models

*(Add gold layer screenshot here if available)*

- Aggregated reporting tables
- Business KPIs
- Optimized for BI tools
- Materialized as **tables**

**Goal:** Deliver analytics-ready datasets for reporting.

---

## 📂 Project Structure

| Folder/File        | Purpose |
|--------------------|----------|
| `models/bronze`    | Raw ingestion models |
| `models/silver`    | Cleaned & joined transformations |
| `models/gold`      | Business-ready analytics models |
| `models/source`    | Source table definitions |
| `tests/generic`    | Custom reusable data tests |
| `macros/`          | Reusable SQL macros |
| `seeds/`           | Static reference CSV data |
| `snapshots/`       | SCD Type-2 snapshot logic |
| `dbt_project.yml`  | dbt configuration file |
| `profiles.yml`     | Databricks connection config |

---

## 🎯 Key Highlights

- End-to-end ELT pipeline in Databricks  
- Production-style dbt project organization  
- SCD Type-2 historical modeling  
- Automated data validation framework  
- Modular SQL engineering with reusable macros  
- Analytics-ready Gold layer  
