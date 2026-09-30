# 📝 SQL Queries

This section contains the full SQL workflow, written in T-SQL for SQL Server. It covers data validation, star schema creation, data loading, KPIs, and deep-dive analysis.

## 📑 Table of Contents

- [A. Data Validation](#a-data-validation)
  - [1. Null Check](#1-null-check)
  - [2. Blank or Empty String Check](#2-blank-or-empty-string-check)
  - [3. Duplicate Records Check](#3-duplicate-records-check)
  - [4. Delete Duplicate Records](#4-delete-duplicate-records)
- [B. Star Schema Creation](#b-star-schema-creation)
  - [1. Dimension Tables](#1-dimension-tables)
  - [2. Fact Table](#2-fact-table)
- [C. Loading Data](#c-loading-data)
  - [1. Populate Dimension Tables](#1-populate-dimension-tables)
  - [2. Populate Fact Table](#2-populate-fact-table)
- [D. KPIs](#d-kpis)
  - [1. Total Orders](#1-total-orders)
  - [2. Total Revenue (INR Million)](#2-total-revenue-inr-million)
  - [3. Average Dish Price (INR)](#3-average-dish-price-inr)
  - [4. Average Rating](#4-average-rating)
- [E. Time-Based Trends](#e-time-based-trends)
  - [1. Monthly Order Trends](#1-monthly-order-trends)
  - [2. Quarterly Trends](#2-quarterly-trends)
  - [3. Yearly Trends](#3-yearly-trends)
  - [4. Orders by Day of the Week](#4-orders-by-day-of-the-week)
- [F. Location Analysis](#f-location-analysis)
  - [1. Top 10 Cities by Order Volume](#1-top-10-cities-by-order-volume)
  - [2. Revenue Contribution by State](#2-revenue-contribution-by-state)
- [G. Food Performance Analysis](#g-food-performance-analysis)
  - [1. Top 10 Restaurants by Order Volume](#1-top-10-restaurants-by-order-volume)
  - [2. Top 5 Categories by Order Volume](#2-top-5-categories-by-order-volume)
  - [3. Most Popular Dishes](#3-most-popular-dishes)
  - [4. Cuisine Performance (Orders and Average Rating)](#4-cuisine-performance-orders-and-average-rating)
- [H. Price and Rating Distribution](#h-price-and-rating-distribution)
  - [1. Total Orders by Price Range](#1-total-orders-by-price-range)
  - [2. Rating Distribution](#2-rating-distribution)

---

## A. Data Validation

### 1. Null Check

```sql
SELECT 
    SUM(CASE WHEN State IS NULL THEN 1 ELSE 0 END) AS Null_State_Count,
    SUM(CASE WHEN City IS NULL THEN 1 ELSE 0 END) AS Null_City_Count,
    SUM(CASE WHEN Restaurant_Name IS NULL THEN 1 ELSE 0 END) AS Null_Restaurant_Name_Count,
    SUM(CASE WHEN Location IS NULL THEN 1 ELSE 0 END) AS Null_Location_Count,
    SUM(CASE WHEN Category IS NULL THEN 1 ELSE 0 END) AS Null_Category_Count,
    SUM(CASE WHEN Dish_Name IS NULL THEN 1 ELSE 0 END) AS Null_Dish_Name_Count,
    SUM(CASE WHEN Price_INR IS NULL THEN 1 ELSE 0 END) AS Null_Price_INR_Count,
    SUM(CASE WHEN Rating IS NULL THEN 1 ELSE 0 END) AS Null_Rating_Count,
    SUM(CASE WHEN Rating_Count IS NULL THEN 1 ELSE 0 END) AS Null_Rating_Count_Count
FROM swiggy_data;
```

### 2. Blank or Empty String Check

```sql
SELECT * FROM swiggy_data
WHERE State = '' OR City = '' OR Restaurant_Name = '' OR Location = '' OR Category = '' OR Dish_Name = '';
```

### 3. Duplicate Records Check

```sql
SELECT State, City, Order_Date, Restaurant_Name, Location, Category, Dish_Name, Price_INR, Rating, Rating_Count, 
       COUNT(*) AS Duplicate_Count
FROM swiggy_data
GROUP BY State, City, Order_Date, Restaurant_Name, Location, Category, Dish_Name, Price_INR, Rating, Rating_Count
HAVING COUNT(*) > 1;
```

### 4. Delete Duplicate Records

```sql
WITH CTE AS (
    SELECT *,
           ROW_NUMBER() OVER (PARTITION BY State, City, Order_Date, Restaurant_Name, 
           Location, Category, Dish_Name, Price_INR, Rating, Rating_Count 
           ORDER BY (SELECT NULL)) AS RowNum
    FROM swiggy_data
)
DELETE FROM CTE WHERE RowNum > 1;
```

---

## B. Star Schema Creation

### 1. Dimension Tables

```sql
-- Date Table
CREATE TABLE dim_date(
    DATE_ID INT IDENTITY(1,1) PRIMARY KEY,
    FULL_DATE DATE,
    YEAR INT,
    MONTH_NAME VARCHAR(20),
    DAY INT,
    QUARTER INT,
    WEEK INT,
    DAY_OF_WEEK INT
);

-- Location Table
CREATE TABLE dim_location(
    LOCATION_ID INT IDENTITY(1,1) PRIMARY KEY,
    STATE VARCHAR(100),
    CITY VARCHAR(100),
    LOCATION VARCHAR(200)
);

-- Restaurant Table
CREATE TABLE dim_restaurant(
    RESTAURANT_ID INT IDENTITY(1,1) PRIMARY KEY,
    RESTAURANT_NAME VARCHAR(200)
);

-- Category Table
CREATE TABLE dim_category(
    CATEGORY_ID INT IDENTITY(1,1) PRIMARY KEY,
    CATEGORY VARCHAR(100)
);

-- Dish Table
CREATE TABLE dim_dish(
    DISH_ID INT IDENTITY(1,1) PRIMARY KEY,
    DISH_NAME VARCHAR(200)
);
```

### 2. Fact Table

```sql
CREATE TABLE fact_order(
    ORDER_ID INT IDENTITY(1,1) PRIMARY KEY,
    DATE_ID INT,
    PRICE_INR DECIMAL(10,2),
    RATING DECIMAL(4,2),
    RATING_COUNT INT,
    LOCATION_ID INT,
    RESTAURANT_ID INT,
    CATEGORY_ID INT,
    DISH_ID INT,
    FOREIGN KEY (DATE_ID) REFERENCES dim_date(DATE_ID),
    FOREIGN KEY (LOCATION_ID) REFERENCES dim_location(LOCATION_ID),
    FOREIGN KEY (RESTAURANT_ID) REFERENCES dim_restaurant(RESTAURANT_ID),
    FOREIGN KEY (CATEGORY_ID) REFERENCES dim_category(CATEGORY_ID),
    FOREIGN KEY (DISH_ID) REFERENCES dim_dish(DISH_ID)
);
```

---

## C. Loading Data

### 1. Populate Dimension Tables

```sql
-- Date
INSERT INTO dim_date (FULL_DATE, YEAR, MONTH_NAME, DAY, QUARTER, WEEK, DAY_OF_WEEK)
SELECT DISTINCT
    Order_Date,
    YEAR(Order_Date),
    DATENAME(MONTH, Order_Date),
    DATEPART(DAY, Order_Date),
    DATEPART(QUARTER, Order_Date),
    DAY(Order_Date),
    DATEPART(WEEKDAY, Order_Date)
FROM swiggy_data
WHERE Order_Date IS NOT NULL;

-- Location
INSERT INTO dim_location (STATE, CITY, LOCATION)
SELECT DISTINCT State, City, Location FROM swiggy_data;

-- Restaurant
INSERT INTO dim_restaurant (RESTAURANT_NAME)
SELECT DISTINCT Restaurant_Name FROM swiggy_data;

-- Category
INSERT INTO dim_category (CATEGORY)
SELECT DISTINCT Category FROM swiggy_data;

-- Dish
INSERT INTO dim_dish (DISH_NAME)
SELECT DISTINCT Dish_Name FROM swiggy_data;
```

### 2. Populate Fact Table

```sql
INSERT INTO fact_order (DATE_ID, PRICE_INR, RATING, RATING_COUNT, 
       LOCATION_ID, RESTAURANT_ID, CATEGORY_ID, DISH_ID)
SELECT dd.DATE_ID,
       sd.Price_INR,
       sd.Rating,
       sd.Rating_Count,
       dl.LOCATION_ID,
       dr.RESTAURANT_ID,
       dc.CATEGORY_ID,
       dishd.DISH_ID
FROM swiggy_data sd
JOIN dim_date dd ON sd.Order_Date = dd.FULL_DATE
JOIN dim_location dl ON sd.State = dl.STATE AND sd.City = dl.CITY AND sd.Location = dl.LOCATION
JOIN dim_restaurant dr ON sd.Restaurant_Name = dr.RESTAURANT_NAME
JOIN dim_category dc ON sd.Category = dc.CATEGORY
JOIN dim_dish dishd ON sd.Dish_Name = dishd.DISH_NAME;
```

---

## D. KPIs

### 1. Total Orders

```sql
SELECT COUNT(*) AS Total_Orders FROM fact_order;
```

### 2. Total Revenue (INR Million)

```sql
SELECT FORMAT(SUM(PRICE_INR) / 1000000.0, 'N2') + ' INR Million'
       AS Total_Revenue_INR_Million 
FROM fact_order;
```

### 3. Average Dish Price (INR)

```sql
SELECT FORMAT(AVG(PRICE_INR), 'N2') + ' INR' AS Average_Dish_Price_INR
FROM fact_order;
```

### 4. Average Rating

```sql
SELECT AVG(RATING) AS Average_Rating
FROM fact_order;
```

---

## E. Time-Based Trends

### 1. Monthly Order Trends

```sql
SELECT d.YEAR, d.MONTH_NAME, COUNT(*) AS Total_Orders
FROM fact_order f
JOIN dim_date d ON f.DATE_ID = d.DATE_ID
GROUP BY d.YEAR, d.MONTH_NAME
ORDER BY COUNT(*) DESC;
```

### 2. Quarterly Trends

```sql
SELECT d.YEAR, d.QUARTER, COUNT(*) AS Total_Orders
FROM fact_order f
JOIN dim_date d ON f.DATE_ID = d.DATE_ID
GROUP BY d.YEAR, d.QUARTER
ORDER BY COUNT(*) DESC;
```

### 3. Yearly Trends

```sql
SELECT d.YEAR, COUNT(*) AS Total_Orders
FROM fact_order f
JOIN dim_date d ON f.DATE_ID = d.DATE_ID
GROUP BY d.YEAR
ORDER BY COUNT(*) DESC;
```

### 4. Orders by Day of the Week

```sql
SELECT DATENAME(WEEKDAY, d.FULL_DATE) AS Day_of_Week, COUNT(*) AS Total_Orders
FROM fact_order f
JOIN dim_date d ON f.DATE_ID = d.DATE_ID
GROUP BY DATENAME(WEEKDAY, d.FULL_DATE), DATEPART(WEEKDAY, d.FULL_DATE)
ORDER BY DATEPART(WEEKDAY, d.FULL_DATE);
```

---

## F. Location Analysis

### 1. Top 10 Cities by Order Volume

```sql
SELECT TOP 10 l.CITY, COUNT(*) AS Total_Orders
FROM fact_order f
JOIN dim_location l ON f.LOCATION_ID = l.LOCATION_ID
GROUP BY l.CITY
ORDER BY COUNT(*) DESC;
```

### 2. Revenue Contribution by State

```sql
SELECT l.STATE, SUM(f.PRICE_INR) AS Total_Revenue
FROM fact_order f
JOIN dim_location l ON f.LOCATION_ID = l.LOCATION_ID
GROUP BY l.STATE
ORDER BY SUM(f.PRICE_INR) DESC;
```

---

## G. Food Performance Analysis

### 1. Top 10 Restaurants by Order Volume

```sql
SELECT TOP 10 r.RESTAURANT_NAME, COUNT(*) AS Total_Orders
FROM fact_order f
JOIN dim_restaurant r ON f.RESTAURANT_ID = r.RESTAURANT_ID
GROUP BY r.RESTAURANT_NAME
ORDER BY COUNT(*) DESC;
```

### 2. Top 5 Categories by Order Volume

```sql
SELECT TOP 5 c.CATEGORY, COUNT(*) AS Total_Orders
FROM fact_order f
JOIN dim_category c ON f.CATEGORY_ID = c.CATEGORY_ID
GROUP BY c.CATEGORY
ORDER BY COUNT(*) DESC;
```

### 3. Most Popular Dishes

```sql
SELECT dis.DISH_NAME, COUNT(*) AS Total_Orders
FROM fact_order f
JOIN dim_dish dis ON f.DISH_ID = dis.DISH_ID
GROUP BY dis.DISH_NAME
ORDER BY COUNT(*) DESC;
```

### 4. Cuisine Performance (Orders and Average Rating)

```sql
SELECT c.CATEGORY, COUNT(*) AS Total_Orders, AVG(f.RATING) AS Average_Rating
FROM fact_order f
JOIN dim_category c ON f.CATEGORY_ID = c.CATEGORY_ID
GROUP BY c.CATEGORY
ORDER BY Total_Orders DESC;
```

---

## H. Price and Rating Distribution

### 1. Total Orders by Price Range

```sql
SELECT
    CASE
        WHEN PRICE_INR < 100 THEN '<100'
        WHEN PRICE_INR BETWEEN 100 AND 200 THEN '100-199'
        WHEN PRICE_INR BETWEEN 200 AND 300 THEN '200-299'
        WHEN PRICE_INR BETWEEN 300 AND 400 THEN '300-399'
        WHEN PRICE_INR BETWEEN 400 AND 500 THEN '400-499'
        ELSE '500+'
    END AS Price_Range,
    COUNT(*) AS Total_Orders
FROM fact_order
GROUP BY
    CASE
        WHEN PRICE_INR < 100 THEN '<100'
        WHEN PRICE_INR BETWEEN 100 AND 200 THEN '100-199'   
        WHEN PRICE_INR BETWEEN 200 AND 300 THEN '200-299'
        WHEN PRICE_INR BETWEEN 300 AND 400 THEN '300-399'
        WHEN PRICE_INR BETWEEN 400 AND 500 THEN '400-499'
        ELSE '500+'
    END
ORDER BY Total_Orders DESC;
```

### 2. Rating Distribution

```sql
SELECT RATING, COUNT(*) AS Rating_Count
FROM fact_order
GROUP BY RATING
ORDER BY COUNT(*) DESC;