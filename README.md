# 🏠 Boston Housing Market — End-to-End Data Analytics Project

![Project Banner](https://img.shields.io/badge/Status-Completed-brightgreen) ![Tools](https://img.shields.io/badge/Tools-Excel%20%7C%20MySQL%20%7C%20PowerBI-blue) ![Dataset](https://img.shields.io/badge/Dataset-506%20Records-orange) ![Domain](https://img.shields.io/badge/Domain-Real%20Estate-purple)

---

## 📌 Project Overview

This is a **complete end-to-end data analytics project** built on the classic Boston Housing Dataset. The goal was to simulate a real-world business scenario where a **real estate investment firm** needs to identify the best neighborhoods in Boston to invest in for **maximum ROI**.

The project covers the **full analytics pipeline** — from raw data to business insights — using four industry-standard tools:

| Phase | Tool | Deliverable |
|-------|------|-------------|
| 📊 Data Cleaning & Exploration | Microsoft Excel | Cleaned dataset + Pivot Charts |
| 🗄️ Deep Analysis | MySQL (via MySQL Workbench) | 7 Business SQL Queries |
| 📝 Business Storytelling | Microsoft Word | Professional Case Study Document |
| 📈 Dashboard & Visualization | Microsoft Power BI | 4-Page Interactive Dashboard |

---

## 📂 Repository Structure

```
Boston-Housing-Market-Analysis/
│
├── 📄 README.md                          # Project documentation
├── 📊 Boston-house-price-data.csv        # Raw dataset (506 records)
├── 📗 Boston_Housing_Analysis.xlsx       # Excel analysis with pivot tables
├── 📘 Boston_Housing_Case_Study.docx     # Business case study document
└── 📉 Boston_Housing_Dashboard.pbix      # Power BI interactive dashboard
```

---

## 📋 Dataset Description

The **Boston Housing Dataset** contains **506 observations** across **14 variables** describing residential neighborhoods in Greater Boston.

| Column | Description | Type |
|--------|-------------|------|
| CRIM | Per capita crime rate by town | Numeric |
| ZN | Proportion of residential land zoned | Numeric |
| INDUS | Proportion of non-retail business acres | Numeric |
| CHAS | Charles River adjacency (1 = yes, 0 = no) | Binary |
| NOX | Nitric oxide concentration (pollution proxy) | Numeric |
| RM | Average number of rooms per dwelling | Numeric |
| AGE | Proportion of old owner-occupied units | Numeric |
| DIS | Distances to employment centres | Numeric |
| RAD | Highway accessibility index | Numeric |
| TAX | Property tax rate per $10,000 | Numeric |
| PTRATIO | Pupil-teacher ratio by town | Numeric |
| B | Black population index | Numeric |
| LSTAT | % lower status population | Numeric |
| **MEDV** | **Median house value in $000s — Target Variable** | Numeric |

---

## 🔍 Phase 1 — Excel: Data Cleaning & Exploration

### What Was Done:
- Imported raw CSV and formatted as structured Excel Table
- Checked for **blanks, duplicates, and outliers**
- Identified **MEDV capped at $50K** — flagged as outlier
- Created **3 calculated columns:**
  - `Price_Category` → Low / Mid / High
  - `Crime_Risk` → Low / Medium / High
  - `Room_Tier` → Small / Medium / Large
- Built **3 Pivot Tables + Charts:**
  - Avg House Price by Crime Risk
  - Avg House Price by Room Tier
  - Price Category Distribution

### Key Excel Findings:
> ✅ Low crime areas average **$25,200** vs High crime areas at **$12,100**
> ✅ Large room properties average **$30,400** — highest of all tiers
> ✅ **56%** of properties fall in the Mid price category

---

## 🗄️ Phase 2 — MySQL: Business Queries

### Database Setup:
- Created `boston_housing` database in MySQL
- Imported 506 records via **Table Data Import Wizard** in MySQL Workbench

### SQL Queries Written:

```sql
-- 1. Basic data validation
SELECT COUNT(*) AS Total_Records FROM `boston-house-price-data`;

-- 2. Overall price statistics
SELECT ROUND(AVG(MEDV),2) AS Avg_Price,
       ROUND(MIN(MEDV),2) AS Min_Price,
       ROUND(MAX(MEDV),2) AS Max_Price
FROM `boston-house-price-data`;

-- 3. Avg price by crime risk band
SELECT CASE
           WHEN CRIM <= 1 THEN 'Low Crime'
           WHEN CRIM <= 10 THEN 'Medium Crime'
           ELSE 'High Crime'
       END AS Crime_Band,
       ROUND(AVG(MEDV),2) AS Avg_Price,
       COUNT(*) AS Total_Areas
FROM `boston-house-price-data`
GROUP BY Crime_Band
ORDER BY Avg_Price DESC;

-- 4. Avg price by room tier
-- 5. School quality impact on price
-- 6. Top 10 best investment areas (Investment Score)
-- 7. Pollution impact on price
```

### SQL Findings:

| Factor | Low Band Avg Price | High Band Avg Price |
|--------|-------------------|---------------------|
| Crime | $25,200 | $12,100 |
| Room Size | $30,400 (Large) | $13,900 (Small) |
| School Quality | $27,800 (Good) | $17,200 (Poor) |
| Pollution | $25,600 (Low) | $14,800 (High) |

---

## 📝 Phase 3 — Business Case Study

A fully formatted **Word document** presenting the analysis as a professional business report for a real estate investment firm.

### Document Structure:
1. **Cover Page** — Branded title page
2. **Executive Summary** — Problem statement and key findings
3. **Data Overview** — Variable descriptions and key statistics
4. **Key Findings** — 4 findings with data tables
5. **Investment Recommendations** — Tier 1, 2, 3 strategy
6. **Risk Factors & Conclusion** — Limitations and next steps

### Investment Score Formula:
```
Investment Score = MEDV / LSTAT
```
> Higher score = Strong house value relative to lower-status population % = Better investment

---

## 📈 Phase 4 — Power BI Dashboard

A **4-page interactive dashboard** with slicers, KPI cards, charts and tables.

### Dashboard Pages:

#### Page 1 — Executive Overview
- KPI Cards: Avg House Price | Total Areas | Avg Crime Rate
- Donut Chart: Price Category Distribution
- Bar Chart: Avg Price by Crime Risk

#### Page 2 — Neighborhood Deep Dive
- 3 Dropdown Slicers: Crime Risk | Room Tier | Price Category
- Table: Area details with Investment Score
- Line Chart: School Quality vs House Price
- Column Chart: Avg Price by Room Size

#### Page 3 — Investment Opportunities
- KPI Card: Avg Investment Score
- Scatter Chart: Crime Rate vs House Price
- Table: Top Investment Areas ranked by Investment Score
- Slicer: Crime Risk filter

#### Page 4 — School & Pollution Impact
- KPI Cards: Avg Pupil Teacher Ratio | Avg Pollution Level
- Bar Chart: School Quality vs House Price
- Column Chart: Pollution Level vs House Price
- Slicer: Crime Risk filter

---

## 💡 Key Business Insights

1. **Crime is the #1 price driver** — Low crime areas command 2x the price of high crime zones
2. **Room size matters** — Large room properties fetch 119% more than small room ones
3. **School quality adds premium** — Good school areas are priced 61% higher than poor school areas
4. **Pollution depresses value** — Low pollution areas are priced 73% higher than high pollution zones
5. **Investment sweet spot** — Properties with CRIM < 1, RM > 6.5, PTRATIO < 15 offer the best ROI

---

## 🛠️ Tools & Technologies

| Tool | Version | Purpose |
|------|---------|---------|
| Microsoft Excel | 2021/365 | Data cleaning, pivot tables, charts |
| MySQL | 9.1 | Database creation, SQL analysis |
| MySQL Workbench | 8.0 CE | SQL query interface |
| Microsoft Power BI | Desktop | Interactive dashboard |
| Microsoft Word | 2021/365 | Business case study document |

---

## 🚀 How to Use This Project

1. **Clone the repository:**
```bash
git clone https://github.com/YOUR_USERNAME/Boston-Housing-Market-Analysis.git
```

2. **Excel file** → Open directly in Microsoft Excel 2016+

3. **SQL** → Import CSV into MySQL using Table Data Import Wizard in MySQL Workbench

4. **Power BI** → Open `.pbix` file in Power BI Desktop (free download from Microsoft)

5. **Case Study** → Open `.docx` in Microsoft Word

---

## 📊 Results Summary

| Metric | Value |
|--------|-------|
| Total Records Analyzed | 506 |
| Average House Price | $22,532 |
| Best Investment Score | 34.0+ |
| Top Price Driver | Crime Rate |
| Recommended Investment Tier | Low Crime + Large Rooms + Good Schools |

---

## 👤 Author

**Kaushiki Sharma** — Data Analyst

[![GitHub](https://img.shields.io/badge/GitHub-Follow-black)](https://github.com/kaushi01)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](https://linkedin.com/in/kaushiki-sharma-/)

---

## 📃 License

This project is open source and available under the [MIT License](LICENSE).

---

⭐ **If you found this project helpful, please give it a star!** ⭐
