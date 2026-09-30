# 🍽️ Swiggy Restaurant Sales Analysis

## 📌 Project Overview

End-to-end analysis of Swiggy restaurant order data using SQL Server for data cleaning, modeling, and querying. The raw flat file was validated, deduplicated, and normalized into a star schema, then analyzed to uncover trends in pricing, ratings, menu categories, and regional performance across Indian cities. The goal is to turn a raw, unstructured order dataset into a clean analytical model and produce insights that could support business decisions such as menu strategy, pricing, and location targeting.

## 🎯 Business Questions

Which cities and states generate the highest order activity. How do dish prices vary across categories and regions. Which restaurants and dishes hold the strongest ratings and order volumes. How do sales patterns shift across months, quarters, and days of the week. Which menu categories are the most popular overall.

## 🔄 Data Pipeline

The workflow moves through four clear stages.

**Raw** starts with `data/raw/swiggy_data_raw.csv`, the original unprocessed export containing 197,402 rows.

**Cleaning** removes 200 duplicate records and standardizes column headers, producing `data/processed/Swiggy_Data_Cleaned.csv` with 197,202 rows.

**Modeling** normalizes the cleaned flat file into a star schema with one fact table and five dimension tables, all stored in `data/processed/`.

**Analysis and reporting** uses SQL queries and visuals to answer the business questions and present findings.

## 🗂️ Repository Structure

| Folder | Purpose |
|--------|---------|
| `data/raw/` | Original unprocessed source file |
| `data/processed/` | Cleaned flat file and the star schema tables |
| `docs/` | Project documentation and SQL query reference |
| `notebooks/` | Jupyter notebooks for exploration and analysis |
| `queries/` | SQL scripts used to query the data model |
| `scripts/` | Cleaning and transformation code |
| `reports/` | Summary reports and written findings |
| `visuals/` | Charts, dashboards, and exported images |

## ⭐ Data Model

The project uses a star schema. `fact_order` sits at the center and connects to `dim_date`, `dim_location`, `dim_restaurant`, `dim_category`, and `dim_dish` through foreign keys.

```
                    dim_date
                       |
     dim_location ---- fact_order ---- dim_restaurant
                       |   |
                dim_category   dim_dish
```

## 📖 Data Dictionary

### `fact_order` (Fact)

| Column | Key | Description |
|--------|-----|-------------|
| `ORDER_ID` | PK | Unique order identifier |
| `DATE_ID` | FK → `dim_date` | Order date reference |
| `PRICE_INR` | Measure | Order price in INR |
| `RATING` | Measure | Dish rating from 0 to 5 |
| `RATING_COUNT` | Measure | Number of ratings |
| `LOCATION_ID` | FK → `dim_location` | Location reference |
| `RESTAURANT_ID` | FK → `dim_restaurant` | Restaurant reference |
| `CATEGORY_ID` | FK → `dim_category` | Category reference |
| `DISH_ID` | FK → `dim_dish` | Dish reference |

### `dim_date` (Dimension)

| Column | Description |
|--------|-------------|
| `DATE_ID` | Primary key |
| `FULL_DATE` | Actual calendar date |
| `YEAR` | Year |
| `MONTH_NAME` | Month name |
| `DAY` | Day of month |
| `QUARTER` | Quarter from 1 to 4 |
| `WEEK` | Week number |
| `DAY_OF_WEEK` | Day of week |

### `dim_location` (Dimension)

| Column | Description |
|--------|-------------|
| `LOCATION_ID` | Primary key |
| `STATE` | State |
| `CITY` | City |
| `LOCATION` | Locality or area |

### `dim_restaurant` (Dimension)

| Column | Description |
|--------|-------------|
| `RESTAURANT_ID` | Primary key |
| `RESTAURANT_NAME` | Restaurant name |

### `dim_category` (Dimension)

| Column | Description |
|--------|-------------|
| `CATEGORY_ID` | Primary key |
| `CATEGORY` | Menu category name |

### `dim_dish` (Dimension)

| Column | Description |
|--------|-------------|
| `DISH_ID` | Primary key |
| `DISH_NAME` | Dish name |

## 🛠️ Tools Used

SQL Server with T-SQL for data validation, cleaning, modeling, and analysis. Add your visualization tool here, for example Power BI, Tableau, or Excel, once your dashboard is complete.

---