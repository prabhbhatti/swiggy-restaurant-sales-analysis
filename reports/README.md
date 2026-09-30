# 🍽️ Swiggy Restaurant Sales Analysis

> **📖 [Read the Full Report Here](Swiggy%20Restaurant%20Summary%20Report.md)** ← Start here!

A deep dive into **Swiggy order data across Indian cities** using SQL Server and Python,
turning 197,402 raw rows into a clean star schema and business ready insights.

## Quick Results
| Metric | Result |
|--------|--------|
| Total Orders | 197,202 |
| Total Revenue | ⟨XX.XX INR Million⟩ |
| Top City | Mumbai |
| Most Popular Category | Fast Food |
| Busiest Day | Saturday |
| Average Rating | ⟨4.X / 5⟩ |

## 🔄 Data Pipeline
Every record flows through four clean stages:
`📁 Raw` · `🧹 Cleaning` · `⭐ Modeling` · `📊 Analysis`

The raw export was validated, deduplicated, and normalized into a star schema with
**1 fact table and 5 dimension tables**, then queried to answer five business questions.

## 📸 Dashboard Preview
| Total Revenue | Top 10 Restaurants |
|----------|-----------|
| ![Total Revenue](visuals/KPIs/Total%20Revenue.png) | ![Top 10 Restaurants](visuals/Food%20Performance%20Analysis/Top%2010%20Restaurants%20by%20Order%20Volume.png) |

## 📁 Repository Structure
- `data/` — raw and processed datasets (star schema tables)
- `queries/` — SQL scripts for all KPIs
- `scripts/` — cleaning and transformation code
- `notebooks/` — exploration and analysis
- `reports/` — full analysis report
- `visuals/` — charts and dashboards, grouped by theme