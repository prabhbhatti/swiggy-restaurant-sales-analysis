Looking at your screenshot, the problem is clear: it's **wall after wall of paragraph text** with no visual variety. Recruiters skim, so we need scannable lists, badges, tables, and whitespace. Here's a punchier version that reads naturally and avoids dashes.

---

```markdown
# 🍽️ Swiggy Restaurant Sales Analysis

![SQL Server](https://img.shields.io/badge/SQL%20Server-T--SQL-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)
![Python](https://img.shields.io/badge/Python-Pandas-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-2ea44f?style=for-the-badge)

> Turning **197,402 rows** of raw Swiggy order data into a clean star schema and business ready insights, all in SQL Server.

📄 **Want the full SQL?** Every query lives in [`docs/Swiggy_Restaurant Doc.md`](Swiggy_Restaurant%20Doc.md).

---

## 📌 Project Overview

This project takes a messy, unstructured Swiggy order export and transforms it into a clean analytical model. The raw file was validated, deduplicated, and normalized into a star schema, then queried to reveal how pricing, ratings, menu categories, and regional demand behave across Indian cities.

The end goal is simple: **support real business decisions** around menu strategy, pricing, and location targeting.

---

## 🎯 Business Questions

This analysis set out to answer five core questions:

1. 🏙️ Which **cities and states** generate the most order activity?
2. 💰 How do **dish prices** vary across categories and regions?
3. ⭐ Which **restaurants and dishes** hold the strongest ratings and volumes?
4. 📅 How do sales shift across **months, quarters, and days of the week**?
5. 🍜 Which **menu categories** are the most popular overall?

---

## 🔄 Data Pipeline

The data flows through four clean stages:

```
📁 RAW  ➜  🧹 CLEANING  ➜  ⭐ MODELING  ➜  📊 ANALYSIS
```

| Stage | What Happens | Output |
|:------|:-------------|:-------|
| **📁 Raw** | Original unprocessed export | `swiggy_data_raw.csv` &nbsp;(197,402 rows) |
| **🧹 Cleaning** | Removes 200 duplicates, standardizes headers | `Swiggy_Data_Cleaned.csv` &nbsp;(197,202 rows) |
| **⭐ Modeling** | Normalizes into a star schema | 1 fact + 5 dimension tables |
| **📊 Analysis** | SQL queries and visuals answer the questions | Charts and findings |

---

## 📊 Key Findings

> The headline results. Every number below is backed by a query in the [full SQL doc](Swiggy_Restaurant%20Doc.md).

| Metric | Result |
|:-------|:-------|
| 💰 **Total Revenue** | ⟨XX.XX INR Million⟩ |
| 📦 **Total Orders** | 197,202 |
| 🏙️ **Top City** | ⟨Mumbai⟩ |
| 🍜 **Most Popular Category** | ⟨Fast Food⟩ |
| 📅 **Busiest Day** | ⟨Saturday⟩ |
| ⭐ **Average Rating** | ⟨4.X / 5⟩ |

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
📦 swiggy-restaurant-analysis
├── 📁 data/
│   ├── raw/                    # Original source file
│   └── processed/              # Cleaned file + star schema tables
├── 📁 docs/                    # Documentation & SQL reference
├── 📁 notebooks/               # Exploration & analysis
├── 📁 queries/                 # SQL scripts
├── 📁 scripts/                 # Cleaning & transformation code
├── 📁 reports/                 # Written findings
└── 📁 visuals/                 # Charts, grouped by theme
    ├── Data Validation/
    ├── KPIs/
    ├── Deep-Dive Analysis/
    ├── Food Performance Analysis/
    └── Location Based Analysis/
```

---

## ⭐ Data Model

A classic **star schema**. The `fact_order` table sits at the center and links out to five dimensions.

```
                    dim_date
                       │
   dim_location ─── fact_order ─── dim_restaurant
                     │   │
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
| `DATE_ID` | 🔗 FK → `dim_date` | Order date reference |
| `PRICE_INR` | 📊 Measure | Order price in INR |
| `RATING` | 📊 Measure | Dish rating from 0 to 5 |
| `RATING_COUNT` | 📊 Measure | Number of ratings |
| `LOCATION_ID` | 🔗 FK → `dim_location` | Location reference |
| `RESTAURANT_ID` | 🔗 FK → `dim_restaurant` | Restaurant reference |
| `CATEGORY_ID` | 🔗 FK → `dim_category` | Category reference |
| `DISH_ID` | 🔗 FK → `dim_dish` | Dish reference |

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
| 🗄️ **SQL Server (T‑SQL)** | Validation, cleaning, star schema modeling, analysis |
| 🐍 **Python (Pandas)** | Exploration and chart generation |

---

<div align="center">

*From raw CSV to a modeled star schema and business ready insights.*

</div>
```

---

### 🎨 What makes this version better for recruiters

1. **Badges up top** give an instant read on your tech stack before they read a word.
2. **A bold one-line hook** (the blockquote) tells them the value in one sentence.
3. **Business Questions are now a numbered list** with icons instead of a text blob, so they scan in seconds.
4. **The pipeline is a visual flow plus a table**, which reads far faster than four paragraphs.
5. **Key Findings is a clean metric table plus an image grid**, the first thing most recruiters look for.
6. **Collapsible data dictionary** (`<details>`) keeps the page short and tidy while the detail stays one click away.
7. Lots of **horizontal rules and whitespace** break up the density you saw in the screenshot.
8. Prose rewritten to **sound natural with no dashes** used as connectors.

---

### ⚠️ Two quick checks

- The image grid uses `<table>` with HTML `<img>` tags so I could set a clean width. This renders fine on GitHub. The `../visuals/...` paths still assume the README sits inside `docs/`. If it lives at the repo root, remove every `../`.
- I left two spots where GitHub may keep a soft hyphen (`T‑SQL`). That's a non‑breaking styling choice, not a typed dash. Swap to plain `T-SQL` if you prefer.

Want me to also generate a matching **banner image** description, or adjust the image grid to show different charts?