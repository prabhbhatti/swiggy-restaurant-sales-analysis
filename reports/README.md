# Swiggy Restaurant Data Analysis (SQL Project)

## Overview
This project explores real world food delivery data from Swiggy covering
197,401 orders placed across India during 2025 (January to August). Using
SQL, I answered business questions about sales, customer behaviour, location
trends, and food performance. The goal was to turn a large raw dataset into
clear insights that a business team could actually use.

## Dataset Snapshot
| Metric | Value |
|--------|-------|
| Total Orders | 197,401 |
| Total Revenue | 53.00 Million INR |
| Average Dish Price | 268.50 INR |
| Average Rating | 4.34 out of 5 |
| Time Period | January to August 2025 |
| States Covered | 28 |

## What I Analysed
The project is split into four themes so the findings stay easy to follow.

### 1. Time Trends
How orders move across the year, the quarter, the month, and the day of week.

### 2. Location Analysis
Which cities order the most and which states bring in the most revenue.

### 3. Food Performance
The most popular categories, restaurants, and dishes, plus how ratings and
prices are spread out.

### 4. Business KPIs
The headline numbers that summarise the whole dataset.

## Key Findings

### Time Trends
Orders stayed steady month to month, sitting between 23,000 and 25,000.
January was the busiest month with 25,393 orders. Weekends were the strongest
days, with Saturday leading at 28,933 orders. Quarter 3 looks smaller only
because the data stops in August, so it holds just two months.

### Location
Bengaluru was the top city by a wide margin with 20,072 orders, almost double
the next city. Karnataka was also the top state for revenue at 5.46 Million
INR, which makes sense because Bengaluru drives so much of it.

### Food Performance
McDonald's and KFC were the two busiest restaurants, very close together at
around 13,000 orders each. Veg Fried Rice was the single most ordered dish.
Most orders fell in the 100 to 299 INR price band, which matches the average
dish price of 268.50 INR.

### Ratings
Ratings lean strongly positive. A 4.4 rating alone appeared on 85,642 orders,
and the vast majority of orders sat at 4.0 or higher.

## Tools Used
* SQL for all queries and aggregation

## Files in This Repository
| File | Description |
|------|-------------|
| README.md | Project overview and key findings |
| Metadata Summary Report.md | Full data tables and detailed breakdowns |

## About This Project
This was built as a portfolio project to show practical SQL skills: writing
aggregation queries, grouping and ranking data, and explaining the results in
plain business language.