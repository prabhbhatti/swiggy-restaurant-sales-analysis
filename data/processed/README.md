Here's a complete `README.md` for your `processed/` folder:
# Processed Data

This folder contains the cleaned dataset and a **star schema** model derived from
the raw Swiggy data. The raw flat file was cleaned, deduplicated, and normalized
into one fact table and five dimension tables for analysis and reporting.

---

## 📁 Files

| File | Type | Description |
|------|------|-------------|
| `Swiggy_Data_Cleaned.csv` | Cleaned flat file | Deduplicated version of the raw dataset |
| `fact_order.csv` | Fact table | One row per order, with measures and foreign keys |
| `dim_date.csv` | Dimension | Order date attributes |
| `dim_location.csv` | Dimension | State / city / locality |
| `dim_restaurant.csv` | Dimension | Restaurant names |
| `dim_category.csv` | Dimension | Menu category names |
| `dim_dish.csv` | Dimension | Dish names |

---

## 🧹 Cleaning Summary

| Dataset | Rows |
|---------|-----:|
| `swiggy_data_raw.csv` (source) | 197,402 |
| `Swiggy_Data_Cleaned.csv` | 197,202 |
| **Rows removed** | **200 (duplicate records)** |

**Changes applied during cleaning:**
- Removed **200 duplicate rows**.
- Standardized column headers (e.g., `Price_INR` → `Price (INR)`, `Rating_Count` → `Rating Count`).
- Normalized the flat file into a star schema (see below).

> ⚠️ **Data quality note:** Some source values in `dim_dish` and `dim_category`
> reflect raw Swiggy menu-listing noise (e.g., leading `*`, quotes, or bracketed
> promo text). One known **character-encoding artifact** exists in `dim_category`
> (e.g., `1 + 1 BOGO @ 179 each [Coupons...Applicable]`), where special characters
> were not read as UTF-8. These are candidates for further cleaning.

---

## ⭐ Star Schema

```
                    dim_date
                       │
     dim_location ──── fact_order ──── dim_restaurant
                       │   │
                dim_category   dim_dish
```

`fact_order` is the central fact table. Each order links to five dimensions via
foreign keys.

---

## 📖 Data Dictionary

### `fact_order.csv`
One row per order.

| Column | Key | Description |
|--------|-----|-------------|
| `ORDER_ID` | PK | Unique order identifier |
| `DATE_ID` | FK → `dim_date` | Order date reference |
| `PRICE_INR` | Measure | Order price in INR |
| `RATING` | Measure | Dish rating (0–5) |
| `RATING_COUNT` | Measure | Number of ratings |
| `LOCATION_ID` | FK → `dim_location` | Location reference |
| `RESTAURANT_ID` | FK → `dim_restaurant` | Restaurant reference |
| `CATEGORY_ID` | FK → `dim_category` | Category reference |
| `DISH_ID` | FK → `dim_dish` | Dish reference |

### `dim_date.csv`
| Column | Description |
|--------|-------------|
| `date_id` | Primary key |
| `FULL_DATE` | Actual calendar date |
| `YEAR` | Year |
| `MONTH_NAME` | Month name (e.g., January) |
| `DAY` | Day of month |
| `QUARTER` | Quarter (1–4) |
| `WEEK` | Week number |
| `DAY_OF_WEEK` | Day of week (1–7) |

### `dim_location.csv`
| Column | Description |
|--------|-------------|
| `LOCATION_ID` | Primary key |
| `STATE` | State |
| `CITY` | City |
| `LOCATION` | Locality / area |

### `dim_restaurant.csv`
| Column | Description |
|--------|-------------|
| `RESTAURANT_ID` | Primary key |
| `RESTAURANT_NAME` | Restaurant name |

### `dim_category.csv`
| Column | Description |
|--------|-------------|
| `CATEGORY_ID` | Primary key |
| `CATEGORY` | Menu category name |

### `dim_dish.csv`
| Column | Description |
|--------|-------------|
| `DISH_ID` | Primary key |
| `DISH_NAME` | Dish name |

### `Swiggy_Data_Cleaned.csv`
Cleaned, denormalized flat file (source for the star schema).

| Column | Description |
|--------|-------------|
| `State` | State |
| `City` | City |
| `Order Date` | Date of order |
| `Restaurant Name` | Restaurant name |
| `Location` | Locality / area |
| `Category` | Menu category |
| `Dish Name` | Dish name |
| `Price (INR)` | Price in INR |
| `Rating` | Dish rating (0–5) |
| `Rating Count` | Number of ratings |

---

## 📝 Notes

- **Naming convention:** schema tables use `UPPER_SNAKE_CASE`; the cleaned flat
  file uses `Title Case (with spaces)`. This is intentional.
- All records are from **2025**.

A couple of quick things before you commit this:

1. I left the encoding note based on what I saw — feel free to remove it if you've already fixed those values.
2. If you know the exact **row counts** for each dimension/fact table (e.g., how many unique dishes, restaurants, etc.), those are great to add — want me to include a "Table Sizes" section if you send the counts?