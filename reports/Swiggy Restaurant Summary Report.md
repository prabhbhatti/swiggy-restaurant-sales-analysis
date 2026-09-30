# 📊 Swiggy Restaurant Data Analysis — Summary Report

**Tools:** SQL (aggregation, grouping, ranking), cloud SQL worksheet for querying
**Dataset:** 197,401 Swiggy orders across 28 states, January to August 2025

---

## 1. Executive Summary

This project looks at how food delivery orders behaved on Swiggy across India in
2025, so we can see where demand comes from, what people order, and what they think
of it. I used SQL to pull apart nearly 200,000 orders by time, location, food type,
and rating, then turned the results into simple takeaways.

The main story is clear. Demand is steady and strong all year, but it is heavily
concentrated. One city and one state pull far ahead of the rest, and a handful of
big brands drive most of the orders. Customers are also happy, since ratings sit
high across the board.

**Headline results:**

| KPI | Value |
|-----|-------|
| Total Orders | 197.4K |
| Total Revenue | 53.0M INR |
| Average Dish Price | 268.50 INR |
| Average Rating | 4.34 / 5 |
| States Covered | 28 |
| Time Period | Jan to Aug 2025 |

📊 *KPI charts: [Total Orders](../visuals/KPIs/Total%20Orders.png) ·
[Total Revenue](../visuals/KPIs/Total%20Revenue.png) ·
[Average Dish Price](../visuals/KPIs/Average%20Dish%20Price.png) ·
[Average Rating](../visuals/KPIs/Average%20Rating.png)*

---

## 2. Objectives

1. How does order demand move across the year, month, and week?
2. Which cities and states drive the most orders and revenue?
3. Which restaurants, categories, and dishes perform best?
4. How do customers rate their orders overall?
5. What price range do most orders fall into?

---

## 3. Methodology

I worked from a single large order table covering 197,401 records. Before analysis,
I ran data validation checks for nulls, blanks, and duplicate records to make sure
the results were clean. Using SQL, I then wrote aggregation queries to group orders
by time period, city, state, restaurant, category, dish, price band, and rating. I
used ranking and sorting to pull out the top performers in each area, then calculated
the headline KPIs like total revenue and average rating.

📊 *Cleaning checks (charts): [Null Check](../visuals/Data%20Validation/Null%20Check.png) ·
[Blank/Empty String Check](../visuals/Data%20Validation/Blank%20or%20Empty%20String%20Check.png) ·
[Duplicate Record Check](../visuals/Data%20Validation/Duplication%20Record%20Check.png) ·
[Delete Duplication](../visuals/Data%20Validation/Delete%20Duplication.png)*

---

## 4. Key Findings & Insights

### 4.1 Time Trends

**Orders by month**

| Month | Total Orders |
|-------|-------------:|
| January | 25,393 |
| August | 25,227 |
| May | 25,188 |
| July | 24,936 |
| April | 24,584 |
| March | 24,400 |
| June | 24,382 |
| February | 23,291 |

**Orders by day of the week (top days)**

| Day | Total Orders |
|-----|-------------:|
| Saturday | 28,933 |
| Sunday | 28,469 |
| Thursday | 28,450 |
| Wednesday | 28,284 |

Orders stayed remarkably steady all year, sitting between 23K and 25K every month,
with January the busiest at 25.4K. Weekends were the strongest days, led by Saturday.

**What this means:** Demand is stable and predictable, which is good for planning. The
only real lift comes on weekends, so that is the natural window for promotions and
extra delivery capacity.

📊 *Charts: [Monthly Order Trends](../visuals/Deep-Dive%20Analysis/Monthly%20Order%20Trends.png) ·
[Orders by Day of The Week](../visuals/Deep-Dive%20Analysis/Orders%20by%20Day%20of%20The%20Week.png) ·
[Quarterly Trends](../visuals/Deep-Dive%20Analysis/Quarterly%20Trends.png) ·
[Yearly Trends](../visuals/Deep-Dive%20Analysis/Yearly%20Trends.png)*

### 4.2 Location

Bengaluru was the top city by a wide margin at 20.1K orders, almost double the next
city. Karnataka was also the top state for revenue at 5.46M INR.

**What this means:** The business is very top heavy on one market. Bengaluru and
Karnataka carry an outsized share, so they are the safest place to protect and the
biggest risk if demand there slips. The cities ranked two through ten are tightly
bunched near 10K each, which shows a healthy second tier worth growing.

📊 *Charts: [Top 10 Cities by Order Volume](../visuals/Location%20Based%20Analysis/Top%2010%20Cities%20by%20Order%20Volume.png) ·
[Revenue Contributed by States](../visuals/Location%20Based%20Analysis/Revenue%20Contributed%20by%20States.png)*

### 4.3 Food Performance

McDonald's and KFC were the two busiest restaurants, neck and neck around 13K orders
each. Veg Fried Rice was the single most ordered dish, and most orders landed in the
100 to 299 INR price band.

**What this means:** A small group of big quick service brands drives the bulk of
orders, so these partners matter most. On price, customers clearly favour the mid
range, which lines up with the 268.50 INR average dish price, so that band is the
sweet spot for deals and combos.

📊 *Charts: [Top 10 Restaurants](../visuals/Food%20Performance%20Analysis/Top%2010%20Restaurants%20by%20Order%20Volume.png) ·
[Most Popular Dishes](../visuals/Food%20Performance%20Analysis/Most%20Popular%20Dishes.png) ·
[Top 5 Categories](../visuals/Food%20Performance%20Analysis/Top%205%20Categories%20by%20Order%20Volume.png) ·
[Cuisine Performance](../visuals/Food%20Performance%20Analysis/Cuisine%20Performance.png) ·
[Total Order by Price Range](../visuals/Food%20Performance%20Analysis/Total%20Order%20by%20Price%20Range.png)*

### 4.4 Ratings

**Rating distribution**

| Rating | Order Count |
|--------|------------:|
| 4.40 | 85,642 |
| 4.30 | 13,698 |
| 4.60 | 10,840 |
| 4.50 | 9,946 |
| 5.00 | 9,401 |
| 4.70 | 9,089 |
| 4.80 | 8,809 |
| 4.20 | 8,214 |
| 4.10 | 7,619 |
| 4.90 | 5,713 |
| 4.00 | 5,346 |
| 3.90 | 4,021 |
| 3.80 | 3,966 |

Ratings lean strongly positive. A 4.4 score alone appeared on 85.6K orders, and the
large majority of orders sat at 4.0 or higher.

**What this means:** Customer satisfaction is high and consistent, so quality is not
the problem to solve here. The opportunity is about reach and volume rather than
fixing a bad experience.

📊 *Chart: [Rating Distribution (1-5)](../visuals/Food%20Performance%20Analysis/Rating%20Distribution%20%281-5%29.png)*

---

## 5. Recommendations

1. **Protect Bengaluru and Karnataka.** They drive the most orders and revenue, so
they deserve the most attention and the strongest partner support.
2. **Grow the second tier cities.** The cities ranked two through ten are close
together near 10K orders, so a small push could lift the whole group.
3. **Lean into weekends.** Saturday and Sunday are the busiest days, so that is
where promotions and delivery capacity will pay off most.
4. **Focus deals on the mid price band.** Most orders sit in the 100 to 299 INR
range, so combos and offers priced there will match what people already buy.
5. **Keep the top brands close.** A few large chains drive most of the volume, so
strong relationships with them protect the core of the business.

---

## 6. Conclusion

Across 197,401 orders in 2025, Swiggy demand was steady through the year with a lift
on weekends. Bengaluru and Karnataka led the country in both orders and revenue, a
small set of big brands drove most of the volume, most spending landed in the mid
price range, and customer ratings were strongly positive.

The clearest ways to grow are to protect the leading market, nurture the tightly
packed second tier of cities, and time promotions around weekends and the mid price
band.