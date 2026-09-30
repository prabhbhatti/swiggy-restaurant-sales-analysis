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

---

## 2. Objectives

1. How does order demand move across the year, month, and week?
2. Which cities and states drive the most orders and revenue?
3. Which restaurants, categories, and dishes perform best?
4. How do customers rate their orders overall?
5. What price range do most orders fall into?

---

## 3. Methodology

I worked from a single large order table covering 197,401 records. Using SQL, I
wrote aggregation queries to group orders by time period, city, state, restaurant,
category, dish, price band, and rating. I used ranking and sorting to pull out the
top performers in each area, then calculated the headline KPIs like total revenue
and average rating. The results were exported into charts and two dashboards so the
patterns are easy to read at a glance.

---

## 4. Key Findings & Insights

### 4.1 Time Trends
> 📊 *See the Time Trends dashboard in `/visuals`*

Orders stayed remarkably steady all year, sitting between 23K and 25K every month,
with January the busiest at 25.4K. Weekends were the strongest days, led by Saturday.

**What this means:** Demand is stable and predictable, which is good for planning. The
only real lift comes on weekends, so that is the natural window for promotions and
extra delivery capacity. The dip in Quarter 3 is not a real drop, it just reflects
the data ending in August.

### 4.2 Location
> 📊 *See the Location dashboard in `/visuals`*

Bengaluru was the top city by a wide margin at 20.1K orders, almost double the next
city. Karnataka was also the top state for revenue at 5.46M INR.

**What this means:** The business is very top heavy on one market. Bengaluru and
Karnataka carry an outsized share, so they are the safest place to protect and the
biggest risk if demand there slips. The cities ranked two through ten are tightly
bunched near 10K each, which shows a healthy second tier worth growing.

### 4.3 Food Performance
> 📊 *See the Food Performance dashboard in `/visuals`*

McDonald's and KFC were the two busiest restaurants, neck and neck around 13K orders
each. Veg Fried Rice was the single most ordered dish, and most orders landed in the
100 to 299 INR price band.

**What this means:** A small group of big quick service brands drives the bulk of
orders, so these partners matter most. On price, customers clearly favour the mid
range, which lines up with the 268.50 INR average dish price, so that band is the
sweet spot for deals and combos.

### 4.4 Ratings
> 📊 *See the Ratings breakdown in `/visuals`*

Ratings lean strongly positive. A 4.4 score alone appeared on 85.6K orders, and the
large majority of orders sat at 4.0 or higher.

**What this means:** Customer satisfaction is high and consistent, so quality is not
the problem to solve here. The opportunity is about reach and volume rather than
fixing a bad experience.

---

## 5. Recommendations

1. **Protect Bengaluru and Karnataka.** They drive the most orders and revenue, so
they deserve the most attention and the strongest partner support.
2. **Grow the second tier cities.** Mumbai, Hyderabad, Jaipur, and the rest are
close together near 10K orders, so a small push could lift the whole group.
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
band. The dashboards make it easy to keep an eye on all of these trends in one place.