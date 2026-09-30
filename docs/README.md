# 🍽️ Swiggy Restaurant Sales Analysis

## 📌 Project Overview

This project takes a messy, unstructured Swiggy order export and turns it into a clean analytical model. The raw file was validated, deduplicated, and normalized into a star schema, then queried to reveal how pricing, ratings, menu categories, and regional demand behave across Indian cities.

The end goal is simple. It gives clear support for real business decisions around menu strategy, pricing, and location targeting.

---

## 🎯 Business Questions

This analysis set out to answer five core questions.

1. 🏙️ Which **cities and states** generate the most order activity?
2. 💰 How do **dish prices** vary across categories and regions?
3. ⭐ Which **restaurants and dishes** hold the strongest ratings and volumes?
4. 📅 How do sales shift across **months, quarters, and days of the week**?
5. 🍜 Which **menu categories** are the most popular overall?

---

## 🔄 Data Pipeline

The data flows through four clean stages.

```
📁 RAW  ➜  🧹 CLEANING  ➜  ⭐ MODELING  ➜  📊 ANALYSIS
```

| Stage | What Happens | Output |
|:------|:-------------|:-------|
| **📁 Raw** | Original unprocessed export | `swiggy_data_raw.csv` (197,402 rows) |
| **🧹 Cleaning** | Removes 200 duplicates and standardizes headers | `Swiggy_Data_Cleaned.csv` (197,202 rows) |
| **⭐ Modeling** | Normalizes the flat file into a star schema | 1 fact table and 5 dimension tables |
| **📊 Analysis** | SQL queries and visuals answer the questions | Charts and findings |

---

## 📊 Key Findings

> The headline results. Every number below is backed by a query in the [full SQL doc](Swiggy_Restaurant%20Doc.md).

| Metric | Result |
|:-------|:-------|
| 💰 **Total Revenue** | XX.XX INR Million |
| 📦 **Total Orders** | 197,202 |
| 🏙️ **Top City** | Mumbai |
| 🍜 **Most Popular Category** | Fast Food |
| 📅 **Busiest Day** | Saturday |
| ⭐ **Average Rating** | 4.X out of 5 |

### 📈 Snapshot

<table>
  <tr>
    <td align="center"><b>Total Revenue</b><br><img src="../visuals/KPIs/Total%20Revenue.png" width="380"/></td>
    <td align="center"><b>Total Orders</b><br><img src="../visuals/KPIs/Total%20Orders.png" width="380"/></td>
  </tr>
  <tr>
    <td align="center"><b>Top 10 Restaurants</b><br><img src="../visuals/Food%20Performance%20Analysis/Top%2010%20Restaurants%20by%20Order%20Volume.png" width="380"/></td>
    <td align="center"><b>Revenue by State</b><br><img src="../visuals/Location%20Based%20Analysis/Revenue%20Contributed%20by%20States.png" width="380"/></td>
  </tr>
</table>

**Monthly Order Trends**

![Monthly Order Trends](../visuals/Deep-Dive%20Analysis/Monthly%20Order%20Trends.png)

---

## 🗂️ Repository Structure

```
swiggy-restaurant-analysis
├── data/
│   ├── raw/            # Original source file
│   └── processed/      # Cleaned file and star schema tables
├── docs/               # Documentation and SQL reference
├── notebooks/          # Exploration and analysis
├── queries/            # SQL scripts
├── scripts/            # Cleaning and transformation code
├── reports/            # Written findings
└── visuals/            # Charts, grouped by theme
    ├── Data Validation/
    ├── KPIs/
    ├── Deep-Dive Analysis/
    ├── Food Performance Analysis/
    └── Location Based Analysis/
```

---

## ⭐ Data Model

A classic star schema. The `fact_order` table sits at the center and links out to five dimensions.

```
                    dim_date
                       |
   dim_location --- fact_order --- dim_restaurant
                   |         |
            dim_category   dim_dish
```

---

## 📖 Data Dictionary

<details>
<summary><b>🟦 fact_order (Fact Table)</b></summary>

<br>

| Column | Key | Description |
|:-------|:----|:------------|
| `ORDER_ID` | 🔑 PK | Unique order identifier |
| `DATE_ID` | 🔗 FK to `dim_date` | Order date reference |
| `PRICE_INR` | 📊 Measure | Order price in INR |
| `RATING` | 📊 Measure | Dish rating from 0 to 5 |
| `RATING_COUNT` | 📊 Measure | Number of ratings |
| `LOCATION_ID` | 🔗 FK to `dim_location` | Location reference |
| `RESTAURANT_ID` | 🔗 FK to `dim_restaurant` | Restaurant reference |
| `CATEGORY_ID` | 🔗 FK to `dim_category` | Category reference |
| `DISH_ID` | 🔗 FK to `dim_dish` | Dish reference |

</details>

<details>
<summary><b>📅 dim_date</b></summary>

<br>

| Column | Description |
|:-------|:------------|
| `DATE_ID` | Primary key |
| `FULL_DATE` | Actual calendar date |
| `YEAR` | Year |
| `MONTH_NAME` | Month name |
| `DAY` | Day of month |
| `QUARTER` | Quarter from 1 to 4 |
| `WEEK` | Week number |
| `DAY_OF_WEEK` | Day of week |

</details>

<details>
<summary><b>📍 dim_location</b></summary>

<br>

| Column | Description |
|:-------|:------------|
| `LOCATION_ID` | Primary key |
| `STATE` | State |
| `CITY` | City |
| `LOCATION` | Locality or area |

</details>

<details>
<summary><b>🏪 dim_restaurant</b></summary>

<br>

| Column | Description |
|:-------|:------------|
| `RESTAURANT_ID` | Primary key |
| `RESTAURANT_NAME` | Restaurant name |

</details>

<details>
<summary><b>🍱 dim_category</b></summary>

<br>

| Column | Description |
|:-------|:------------|
| `CATEGORY_ID` | Primary key |
| `CATEGORY` | Menu category name |

</details>

<details>
<summary><b>🍕 dim_dish</b></summary>

<br>

| Column | Description |
|:-------|:------------|
| `DISH_ID` | Primary key |
| `DISH_NAME` | Dish name |

</details>

---

## 🛠️ Tools Used

| Tool | Role |
|:-----|:-----|
| 🗄️ **SQL Server (T-SQL)** | Validation, cleaning, star schema modeling, and analysis |
---

<div align="center">

*From a raw CSV to a modeled star schema and business ready insights.*

</div>
