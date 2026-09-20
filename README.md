<div align="center">

# 🚦 Road Accident Analysis

### SQL Server • Excel • Power BI • Data Analytics

<p>
  <strong>End-to-End Road Accident Analytics Project</strong>
</p>

<p>
  <a href="#-project-overview">Overview</a> •
  <a href="#-dataset">Dataset</a> •
  <a href="#-workflow">Workflow</a> •
  <a href="#-sql-server-analysis">SQL</a> •
  <a href="#-power-bi-dashboard">Power BI</a> •
  <a href="#-key-insights">Insights</a>
</p>

<br>

<img src="https://img.shields.io/badge/SQL%20Server-Analysis-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white">
<img src="https://img.shields.io/badge/Excel-Dashboard-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white">
<img src="https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black">
<img src="https://img.shields.io/badge/Data%20Analytics-Project-3776AB?style=for-the-badge">

<br><br>

<img src="images/dashboard-preview.png" alt="Road Accident Analysis Dashboard" width="900">

<br>

<em>Interactive Road Accident Analysis Dashboard</em>

</div>

---

# 📌 Project Overview

This repository contains a complete **End-to-End Road Accident Analysis Project** covering accident records from **2021 and 2022**.

The project demonstrates how raw accident data can be transformed into reliable analytical insights through:

- Data Validation
- Data Cleaning
- Data Transformation
- SQL Analysis
- Exploratory Data Analysis
- Data Modeling
- KPI Development
- Interactive Dashboard Development

The project combines three major analytics tools:

- 🗄️ **Microsoft SQL Server**
- 📊 **Microsoft Excel**
- 📈 **Microsoft Power BI**

The main objective is to create a reliable analytical framework for monitoring road accident trends, understanding accident patterns, comparing yearly performance, and supporting data-driven decision-making.

---

# 🎯 Business Objectives

The analysis focuses on answering key business questions such as:

| Business Question | Analysis |
|---|---|
| 🚦 How many accidents occurred? | Accident KPI Analysis |
| 👥 How many casualties were recorded? | Casualty Analysis |
| 📅 How did 2022 compare with 2021? | Year-over-Year Analysis |
| 🛣️ Which road types have the highest accident concentration? | Road Type Analysis |
| 🚗 Which vehicle categories are most involved? | Vehicle Analysis |
| 🌆 Are accidents more common in urban or rural areas? | Location Analysis |
| 🌤️ How do lighting and weather conditions affect accidents? | Environmental Analysis |
| 📍 Which locations have the highest accident concentration? | Geographic Analysis |
| ⚠️ Which accident severity categories dominate? | Severity Analysis |

---

# 📊 Dataset

The project analyzes approximately:

<div align="center">

| Metric | Value |
|---|---:|
| 🚗 Accident Records | **≈ 307,000** |
| 📅 Years Covered | **2021 – 2022** |
| 📋 Attributes | **21** |
| 💾 Source File | **CSV (~60 MB)** |

</div>

### Key Data Fields

The dataset contains information related to:

**Accident Information**

- Accident Index
- Accident Date
- Accident Time
- Accident Severity
- Number of Casualties
- Number of Vehicles

**Road Information**

- Road Type
- Junction Details
- Junction Control
- Carriageway
- Road Surface Conditions
- Urban / Rural Area

**Environmental Conditions**

- Weather Conditions
- Light Conditions
- Road Surface Conditions
- Carriageway Hazards

**Vehicle Information**

- Vehicle Type
- Vehicle Characteristics
- Number of Vehicles Involved

---

# 🛠️ Technology Stack

<div align="center">

| Technology | Main Purpose |
|---|---|
| 🗄️ **SQL Server** | Data Validation & Analytical Queries |
| 📊 **Microsoft Excel** | Data Analysis & Interactive Dashboard |
| 📈 **Power BI** | Data Modeling & Business Intelligence |
| 🔄 **Power Query** | Data Cleaning & Transformation |
| 📐 **DAX** | KPI & Time Intelligence |
| 🎨 **PowerPoint** | Dashboard UI/UX Design |

</div>

---

# 🔄 Project Workflow

<div align="center">

```text
                  ┌──────────────────────┐
                  │     Raw CSV Data     │
                  │    ~307K Records     │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │    Data Validation   │
                  │      SQL Server      │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │   Data Cleaning &    │
                  │   Transformation     │
                  │    Excel / Power     │
                  │       Query          │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Exploratory Analysis │
                  │     SQL / Excel     │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │    Data Modeling     │
                  │      Power BI        │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │   DAX & KPI Layer    │
                  │  Time Intelligence   │
                  └──────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Interactive          │
                  │ Accident Dashboard   │
                  └──────────────────────┘
