# 🍴 Swiggy Restaurant Data Analysis (India, 2025)

Analyzing nearly 200,000 Swiggy food delivery orders across India using SQL, to
understand where demand comes from, what people order, and how they rate it.

---

## 📌 Overview

This project takes a raw dataset of Swiggy orders and turns it into a clear story a
business can act on. Using SQL, I broke down the orders by time, location, food type,
price, and rating, then pulled the results together into a short set of findings and
recommendations.

The headline story is simple. Demand is steady and strong all year, but it is heavily
concentrated. One city and one state pull far ahead of everyone else, a small group
of big brands drive most of the orders, and customers are happy, with ratings sitting
high across the board.

---

## 🎯 Key Results

| KPI | Value |
|:----|:------|
| Total Orders | 197.4K |
| Total Revenue | 53.0M INR |
| Average Dish Price | 268.50 INR |
| Average Rating | 4.34 / 5 |
| States Covered | 28 |
| Time Period | Jan to Aug 2025 |

**A few things that stood out:**

1. Bengaluru led all cities at 20.1K orders, almost double the next city.
2. Karnataka was the top state for revenue at 5.46M INR.
3. McDonald's and KFC were the busiest restaurants, close to 13K orders each.
4. Most orders fell in the 100 to 299 INR range, more than half of all orders.
5. Ratings leaned strongly positive, with 4.4 the most common score by far.

---

## 🛠️ Tools & Skills

* **SQL** for querying, aggregation, grouping, ranking, and sorting
* **Data validation** for null, blank, and duplicate checks before analysis
* **Data storytelling** for turning raw query output into plain takeaways

---

## 📂 Project Structure

```
Swiggy-Restaurant-Analysis/
│
├── README.md                     Project overview (this file)
├── .gitignore
│
├── data/
│   ├── raw/
│   │   └── swiggy_data_raw.csv           Original unprocessed dataset
│   └── processed/
│       ├── README.md
│       ├── Swiggy_Data_Cleaned.csv       Cleaned full dataset
│       ├── dim_category.csv              Category dimension
│       ├── dim_date.csv                  Date dimension
│       ├── dim_dish.csv                  Dish dimension
│       ├── dim_location.csv              Location dimension
│       ├── dim_restaurant.csv            Restaurant dimension
│       └── fact_order.csv                Order fact table
│
├── docs/
│   ├── README.md
│   └── Swiggy_Restaurant Doc.md          Dataset documentation
│
├── queries/                              All SQL queries used in the analysis
│
├── visuals/                              Charts and KPI cards
│   ├── KPIs/
│   ├── Data Validation/
│   ├── Deep-Dive Analysis/
│   ├── Location Based Analysis/
│   └── Food Performance Analysis/
│
└── reports/
    ├── README.md
    └── Swiggy Restaurant Summary Report.md   Full written report with tables and insights
```

---

## 📖 What's Inside the Analysis

The full write up covers four areas:

1. **Time Trends** — how orders moved across the year, months, and days of the week
2. **Location** — the top cities by orders and the top states by revenue
3. **Food Performance** — the busiest restaurants, top dishes, and popular price bands
4. **Ratings** — how customers scored their orders overall

Each section pairs a short table of the numbers with a plain explanation of what it
means for the business, plus links to the matching charts in the visuals folder.

👉 **Read the full write up here: [Summary Report](reports/Swiggy%20Restaurant%20Summary%20Report.md)**

---

## 💡 Main Takeaways

1. Protect Bengaluru and Karnataka, since they carry an outsized share of the business.
2. Grow the second tier cities, which sit tightly bunched near 10K orders each.
3. Time promotions around weekends, the strongest days for orders.
4. Focus deals on the mid price band, where most spending already happens.
5. Keep the top brands close, since a few chains drive most of the volume.

---

## 👤 Author

**[Bhatti Prabhpreet Singh]**
Data Analyst | SQL • Data Storytelling • Business Insights

📫 [LinkedIn](https://www.linkedin.com/in/bhatti-prabhpreet-singh/)
