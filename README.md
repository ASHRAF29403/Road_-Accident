<div align="center">

# 🚦 Road Accident Analysis

### SQL • Excel • Power BI • Data Analytics & Business Intelligence

<p>
  <strong>End-to-End Road Accident Data Analysis (2021–2022)</strong>
</p>

<p>
  <a href="#-project-overview">Overview</a> •
  <a href="#-dataset-overview">Dataset</a> •
  <a href="#️-technologies--implementation">Technologies</a> •
  <a href="#-key-business-insights">Insights</a> •
  <a href="#-skills-demonstrated">Skills</a>
</p>

<br>

<img src="https://img.shields.io/badge/Microsoft%20SQL%20Server-Database-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white">
<img src="https://img.shields.io/badge/Microsoft%20Excel-Dashboard-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white">
<img src="https://img.shields.io/badge/Power%20BI-Business%20Intelligence-F2C811?style=for-the-badge&logo=powerbi&logoColor=black">
<img src="https://img.shields.io/badge/Data%20Analytics-Insights-3776AB?style=for-the-badge">

<br><br>

<img src="images/project-preview.png" alt="Road Accident Analysis" width="900">

<br>

<em>Road Accident Analysis — SQL, Excel & Power BI</em>

</div>

---

# 📚 Table of Contents

- [📌 Project Overview](#-project-overview)
- [📊 Dataset Overview](#-dataset-overview)
- [🛠️ Technologies & Implementation](#️-technologies--implementation)
  - [1️⃣ Microsoft SQL Server](#1️⃣-microsoft-sql-server-mssql)
  - [2️⃣ Microsoft Excel](#2️⃣-microsoft-excel)
  - [3️⃣ Power BI](#3️⃣-power-bi)
- [📈 Key Business Insights](#-key-business-insights)
- [🧠 Skills Demonstrated](#-skills-demonstrated)
- [📁 Project Structure](#-project-structure)
- [⚙️ How to Run](#️-how-to-run)
- [🏆 Project Outcome](#-project-outcome)
- [👨‍💻 Author](#-author)

---

# 📌 Project Overview

This repository contains a complete **end-to-end Road Accident Analysis Project** covering accident records from **2021 and 2022**.

The project demonstrates how a Data Analyst can transform raw accident data into actionable business insights through **data validation, cleaning, modeling, and interactive dashboard development**, using three of the most widely used analytics tools:

- 🗄️ **Microsoft SQL Server (MSSQL)**
- 📗 **Microsoft Excel**
- 📊 **Microsoft Power BI**

The objective was to build a reliable analytical framework that supports **accurate reporting, performance monitoring, trend analysis, and data-driven decision-making**.

---

# 📊 Dataset Overview

<div align="center">

| Metric | Value |
|---|---:|
| 📦 Accident Records | **≈ 307,000** |
| 📅 Time Period | **2021 – 2022** |
| 📐 Attributes | **21 columns** |
| 🌍 Domain | **Road Safety / Transportation** |

</div>

### Key Data Fields

```text
✓ Accident Index (Unique Identifier)
✓ Accident Date & Time
✓ Accident Severity        → Fatal / Serious / Slight
✓ Weather Conditions
✓ Lighting Conditions       → Daylight / Darkness
✓ Road Surface Conditions
✓ Road Type
✓ Number of Casualties
✓ Number of Vehicles Involved
✓ Vehicle Type
✓ Urban / Rural Classification
```

---

# 🛠️ Technologies & Implementation

<div align="center">

```text
                  ┌─────────────────────────┐
                  │      Raw Dataset        │
                  │     307K+ Records       │
                  │     21 Attributes       │
                  └────────────┬────────────┘
                               │
                               ▼
                  ┌─────────────────────────┐
                  │   SQL Server (MSSQL)    │
                  │                         │
                  │ Data Validation         │
                  │ Business Rules          │
                  │ KPI Calculations        │
                  └────────────┬────────────┘
                               │
                               ▼
                  ┌─────────────────────────┐
                  │  Microsoft Excel        │
                  │                         │
                  │ Data Cleaning           │
                  │ Pivot Tables / Charts   │
                  │ Interactive Dashboard   │
                  └────────────┬────────────┘
                               │
                               ▼
                  ┌─────────────────────────┐
                  │        Power BI         │
                  │                         │
                  │ Power Query             │
                  │ Star Schema Modeling    │
                  │ DAX Measures            │
                  │ Executive Dashboard     │
                  └─────────────────────────┘
```

</div>

---

## 1️⃣ Microsoft SQL Server (MSSQL)

SQL Server was used for **data validation, business rule verification, and analytical calculations** to ensure complete consistency between source data and reporting outputs.

### 🧹 Data Preparation

- Imported and processed a large CSV dataset (**~60 MB**)
- Standardized column names by replacing spaces with underscores
- Optimized data types for better storage and query performance
- Applied NULL handling strategies to prevent import failures

### 🧠 SQL Techniques Applied

```text
✓ KPI Calculations
✓ Aggregations (SUM, COUNT, AVG)
✓ Conditional Logic (CASE WHEN)
✓ Percentage Calculations (CAST, DECIMAL)
✓ Ranking and Top-N Analysis
✓ Data Validation Queries
✓ Advanced Filtering and Grouping
```

### 📌 Business Questions Answered

- Total Accidents and Casualties (Current vs Previous Year)
- Casualty Distribution by Vehicle Type
- Accident Severity Analysis
- Top 10 High-Risk Locations
- Urban vs Rural Accident Comparison
- Road Type Performance Analysis

### Example: Year-over-Year Comparison

```sql
SELECT
    accident_year,
    COUNT(*) AS total_accidents,
    SUM(number_of_casualties) AS total_casualties
FROM road_accidents
WHERE accident_year IN (2021, 2022)
GROUP BY
    accident_year
ORDER BY
    accident_year;
```

### Example: Severity Breakdown with Percentage

```sql
SELECT
    accident_severity,
    COUNT(*) AS total_accidents,
    CAST(
        COUNT(*) * 100.0 / SUM(COUNT(*)) OVER ()
        AS DECIMAL(5, 2)
    ) AS percentage_of_total
FROM road_accidents
GROUP BY
    accident_severity
ORDER BY
    total_accidents DESC;
```

### Example: Top 10 High-Risk Locations

```sql
SELECT TOP 10
    local_authority,
    COUNT(*) AS total_accidents,
    SUM(number_of_casualties) AS total_casualties
FROM road_accidents
GROUP BY
    local_authority
ORDER BY
    total_accidents DESC;
```

### Example: Urban vs Rural Comparison

```sql
SELECT
    urban_or_rural_area,
    COUNT(*) AS total_accidents,
    AVG(number_of_casualties) AS avg_casualties_per_accident
FROM road_accidents
GROUP BY
    urban_or_rural_area
ORDER BY
    total_accidents DESC;
```

---

## 2️⃣ Microsoft Excel

Excel was utilized to create a fully interactive dashboard while demonstrating advanced spreadsheet analytics techniques.

### 🧹 Data Cleaning

- Corrected data quality issues using **Find & Replace**
- Fixed spelling inconsistencies in accident severity classifications

### 🔄 Data Transformation

Created additional analytical fields using:

```text
TEXT(Date,"mmm")   →  Month
TEXT(Date,"yyyy")  →  Year
```

to generate **Year**, **Month**, and other time-based reporting dimensions.

### 📊 Dashboard Features

```text
✓ Pivot Tables
✓ Pivot Charts
✓ Calculated Items
✓ Interactive Slicers
✓ Timelines
✓ Professional Dark-Themed Design
✓ Navigation Buttons and Hyperlinks
```

### 🎯 Output

A fully dynamic dashboard allowing users to explore accident trends across multiple dimensions with a single click.

---

## 3️⃣ Power BI

Power BI was used to build a scalable semantic model and executive-level dashboard experience.

### 🔧 Power Query

```text
✓ Data Cleaning
✓ Data Transformation
✓ Data Profiling
✓ Data Validation
```

### 📐 Data Modeling

```text
✓ One-to-Many Relationships
✓ Star Schema Modeling
✓ Calendar Table Creation
```

### 🧮 DAX Measures

Developed advanced measures including:

- Current Year Casualties
- Previous Year Casualties
- Year-over-Year Growth (YoY)
- YTD Analysis
- Percentage Contribution Metrics

**Key functions used:**

```dax
TOTALYTD()
SAMEPERIODLASTYEAR()
CALCULATE()
DIVIDE()
```

**Example — YoY Growth Measure:**

```dax
YoY Growth % =
DIVIDE(
    [Current Year Casualties] - [Previous Year Casualties],
    [Previous Year Casualties]
)
```

**Example — YTD Casualties:**

```dax
Casualties YTD =
TOTALYTD (
    SUM ( road_accidents[number_of_casualties] ),
    calendar_table[Date]
)
```

### 📊 Dashboard Visuals

```text
✓ KPI Cards
✓ Area Charts
✓ Donut Charts
✓ Clustered Column Charts
✓ Interactive Geographic Maps
✓ Dynamic Filters and Drilldowns
```

### 🎨 UI/UX Design

Custom dashboard backgrounds were designed in **PowerPoint** and integrated into Power BI to create a polished, professional reporting experience.

---

# 📈 Key Business Insights

## 1️⃣ 📉 Overall Improvement in Road Safety

The analysis revealed an **overall reduction in both accidents and casualties** during 2022 compared to 2021.

| Metric | Change (2022 vs 2021) |
|---|---:|
| Accident-related metrics | **↓ ≈ 11% – 12%** |

This indicates measurable improvements in road safety performance.

## 2️⃣ 🛣️ High-Risk Road Types

**Single carriageways** accounted for more than:

# **70% – 75%**

of total recorded accidents.

> 💡 **Recommendation:** Infrastructure investment should prioritize converting high-risk single carriageways into safer dual-carriageway roads where feasible.

## 3️⃣ 🌆 Accident Concentration Patterns

Most accidents occurred:

- 🏙️ **In Urban Areas**
- ☀️ **During Daylight Conditions**

This suggests that **traffic density** plays a more significant role in accident frequency than visibility constraints alone.

## 4️⃣ 🚗 Highest-Risk Vehicle Category

**Cars** were responsible for the largest proportion of accident involvement compared with all other vehicle categories.

This points toward the importance of **targeted driver awareness campaigns** and **stricter traffic enforcement measures**.

---

# 🧠 Skills Demonstrated

```text
✓ SQL (MSSQL)
✓ Data Cleaning
✓ Data Validation
✓ Exploratory Data Analysis (EDA)
✓ Data Modeling
✓ Power Query
✓ DAX
✓ Excel Dashboards
✓ Tableau Visualization
✓ Power BI Development
✓ Business Intelligence
✓ KPI Development
✓ Dashboard Design (UI/UX)
✓ Data Storytelling
```

---

# 📁 Project Structure

```text
road-accident-analysis/
│
├── images/
│   ├── project-preview.png
│   ├── excel-dashboard.png
│   └── powerbi-dashboard.png
│
├── sql/
│   ├── 01_data_preparation.sql
│   ├── 02_data_validation.sql
│   ├── 03_kpi_calculations.sql
│   └── 04_business_analysis.sql
│
├── excel/
│   └── road_accident_dashboard.xlsx
│
├── powerbi/
│   └── road_accident_analysis.pbix
│
└── README.md
```

> 📝 عدّل الأسماء والمسارات دي بحيث تطابق بالظبط أسماء الملفات الموجودة فعليًا في الريبو بتاعك.

---

# ⚙️ How to Run

1. **Clone the repository**
```bash
   git clone https://github.com/ASHRAF29403/road-accident-analysis.git
```
2. **SQL Server**: Open SSMS, connect to your instance, and run the scripts in `sql/` in order (`01` → `04`).
3. **Excel**: Open `excel/road_accident_dashboard.xlsx` to explore the interactive Pivot-based dashboard.
4. **Power BI**: Open `powerbi/road_accident_analysis.pbix` in Power BI Desktop to explore the semantic model, DAX measures, and executive dashboard.

---

# 🏆 Project Outcome

This project demonstrates a complete analytics workflow, starting from raw accident records and ending with validated insights and interactive dashboards across multiple BI platforms.

It highlights the ability to combine **SQL, Excel, and Power BI** to build production-quality analytical solutions that support business stakeholders with reliable, data-driven decision-making.

---

# 👨‍💻 Author

**Ashraf Nabil Mohamed**
Data Analyst Junior & Machine Learning | Transitioning to Data Engineering

- 🎓 B.Sc. Computer Science (AI & Data Science), Zagazig University
- 💻 GitHub: [github.com/ASHRAF29403](https://github.com/ASHRAF29403)

</div>
