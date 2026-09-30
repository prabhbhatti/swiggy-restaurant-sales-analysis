# 🍽️ Swiggy Restaurant Sales Analysis — Summary Report

**Name:** ⟨Your Name⟩
**Tools:** SQL Server (data cleaning, star schema modeling, and analysis), Python with Pandas (exploration and charts)
**Dataset:** ad hoc Swiggy order export. Order level records across Indian cities covering price, ratings, restaurants, dishes, menu categories, and location.

---

## 1. Executive Summary

This project looks at Swiggy order data to understand how pricing, ratings, menu categories, and regional demand behave across Indian cities, so we can make smarter decisions about menu strategy, pricing, and where to focus. I started with a messy export of 197,402 rows, cleaned it down to 197,202 clean records, and modeled it into a star schema so it could be queried quickly and reliably.

The main takeaway is that demand is concentrated. A small group of cities and menu categories drive most of the activity, and there are clear patterns in when people order and what they are willing to pay. That gives us obvious places to focus budget and attention.

**Headline results:**

| KPI | Result |
|-----|--------|
| Total Orders | 197,202 |
| Total Revenue | ⟨XX.XX INR Million⟩ |
| Top City | Mumbai |
| Most Popular Category | Fast Food |
| Busiest Day | Saturday |
| Average Rating | ⟨4.X / 5⟩ |
| Duplicates Removed | 200 |

---

## 2. Objectives

1. Which cities and states generate the most order activity?
2. How do dish prices vary across categories and regions?
3. Which restaurants and dishes hold the strongest ratings and volumes?
4. How do sales shift across months, quarters, and days of the week?
5. Which menu categories are the most popular overall?

---

## 3. Methodology

I built a star schema in SQL Server that connects a central `fact_order` table to five dimensions: `dim_date`, `dim_location`, `dim_restaurant`, `dim_category`, and `dim_dish`. Before modeling, I validated the raw file, standardized the headers, and removed 200 duplicate rows, which brought the clean dataset to 197,202 records.

I then wrote SQL queries for every KPI and for the deeper breakdowns by city, category, restaurant, and time. Python with Pandas was used for exploration and to generate the charts. Each visual maps back to one of the five business questions, so the analysis stays focused and easy to follow.

---

## 4. Key Findings & Insights

### 4.1 Location — Cities and States

| Rank | City | Orders | Revenue Share |
|------|------|--------|---------------|
| 1 | Mumbai | ⟨ ⟩ | ⟨ ⟩ |
| 2 | ⟨City⟩ | ⟨ ⟩ | ⟨ ⟩ |
| 3 | ⟨City⟩ | ⟨ ⟩ | ⟨ ⟩ |

**What this means:** Demand is concentrated in a handful of major cities, with Mumbai leading order activity. The top cities pull in a large share of total revenue, which tells us where the core customer base already lives. That makes them the safest place to defend market share, while the mid tier cities are the natural targets for growth.

### 4.2 Pricing — Dish Prices by Category and Region

| Category | Average Price (INR) | Notes |
|----------|---------------------|-------|
| ⟨Category⟩ | ⟨ ⟩ | Highest average price |
| ⟨Category⟩ | ⟨ ⟩ | Mid range |
| ⟨Category⟩ | ⟨ ⟩ | Most affordable |

**What this means:** Prices vary a lot by category, and they also shift from region to region for the same type of dish. The higher priced categories bring in more revenue per order, while the affordable categories drive volume. Knowing this split helps decide where to run offers and where premium pricing already works.

### 4.3 Food Performance — Restaurants and Dishes

| Type | Top Performer | Metric |
|------|---------------|--------|
| Restaurant by Orders | ⟨Restaurant⟩ | ⟨ ⟩ orders |
| Restaurant by Rating | ⟨Restaurant⟩ | ⟨ ⟩ / 5 |
| Dish by Volume | ⟨Dish⟩ | ⟨ ⟩ orders |

**What this means:** A small set of restaurants and dishes account for a large share of orders and hold the strongest ratings. These are the reliable performers worth featuring and promoting. The average rating across the platform sits around ⟨4.X out of 5⟩, which shows overall satisfaction is healthy, so the focus can stay on volume rather than fixing quality problems.

### 4.4 Time Trends — Months, Quarters, and Days

| Time View | Peak | Notes |
|-----------|------|-------|
| Busiest Day | Saturday | Weekend demand is highest |
| Busiest Month | ⟨Month⟩ | ⟨ ⟩ |
| Strongest Quarter | ⟨Q⟩ | ⟨ ⟩ |

**What this means:** Orders clearly rise toward the weekend, with Saturday as the busiest day. There are also seasonal swings across months and quarters that repeat in a predictable way. This makes it easier to plan promotions and staffing, since we know in advance when demand will spike.

### 4.5 Menu Categories — Popularity

| Rank | Category | Orders | Share |
|------|----------|--------|-------|
| 1 | Fast Food | ⟨ ⟩ | ⟨ ⟩ |
| 2 | ⟨Category⟩ | ⟨ ⟩ | ⟨ ⟩ |
| 3 | ⟨Category⟩ | ⟨ ⟩ | ⟨ ⟩ |

**What this means:** Fast Food is the most popular category overall, so it is the clear anchor of the menu. A few categories carry most of the demand while the long tail brings in far less. That points to keeping the popular categories well stocked and promoted, while reviewing whether the weaker categories are worth the shelf space.

---

## 5. Recommendations

1. **Double down on the top cities.** Mumbai and the other leading cities already drive most of the revenue, so they should keep the core budget while mid tier cities become the growth targets.
2. **Lead with Fast Food and the top categories.** They pull the most orders, so they deserve the best placement and the most promotion.
3. **Use pricing by category smartly.** Run offers on the affordable, high volume categories and hold firm pricing where premium dishes already sell well.
4. **Feature the proven restaurants and dishes.** The top performers have both the volume and the ratings, so promoting them is a low risk way to lift orders.
5. **Plan around the weekend and seasonal peaks.** Saturday and the busy months are predictable, so schedule promotions and support to match.
6. **Review the weak categories.** The long tail brings in little, so decide whether to refresh them or focus the effort elsewhere.

---

## 6. Conclusion

Overall, the cleaned dataset of 197,202 orders shows that demand is concentrated in a few cities and a few menu categories, led by Mumbai and Fast Food, with the strongest activity landing on Saturdays. Pricing, ratings, and volumes all point to a clear group of winners that are worth backing.

The clearest ways to grow are to focus spend on the top cities, promote the most popular categories and proven dishes, price by category with intent, and plan around the weekend and seasonal peaks. The star schema and SQL queries behind this report make it easy to refresh these numbers and keep tracking all the key metrics in one place.