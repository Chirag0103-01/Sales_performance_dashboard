# Sales_performance_dashboard

An interactive sales analytics project tracking revenue, profit margin, growth,
and top-performing products/regions for a retail business — built for Power BI
with the underlying analysis also reproduced in pure SQL.

## Dataset

- **Name:** Sample Superstore Dataset
- **Source:** [Kaggle – Superstore Dataset](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)
  (also published as "Sample Superstore" — a long-standing, widely used retail
  analytics dataset, originally popularized via Tableau Public)
- **Size:** ~9,800 order-level retail transactions (2019–2022), covering Sales,
  Profit, Discount, Quantity, Region, Segment, Category, and Product details.

> **Setup:** Download the CSV from Kaggle and save as `data/superstore.csv`
> before running the script.

## Tools Used

Python, Pandas (cleaning & KPI calculation) · SQL (see `sql_queries.sql` —
joins-equivalent aggregations, window functions: `RANK()`, `LAG()`, running
totals) · Excel (pivot-table cross-check) · Power BI (final interactive
dashboard)

## What the Script Does

1. **Data cleaning** — handles encoding issues common in this dataset, parses
   order dates, removes duplicate rows.
2. **KPI calculation** — total sales, total profit, profit margin %, total
   orders.
3. **EDA & charts** —
   - Monthly sales trend
   - Year-over-year sales growth
   - Sales by category and region
   - Top 10 products by sales
   - Profit margin by customer segment
   - Discount vs profit relationship
4. **Automated clean export** — writes a dashboard-ready CSV to `outputs/`,
   simulating the "automated reporting" refresh step you'd schedule in a real
   pipeline.
5. **Auto-generated insights summary.**

## How to Run

```bash
pip install pandas numpy matplotlib seaborn
python sales_analysis.py
```

### SQL Version

`sql_queries.sql` reproduces the core analysis in SQL, including:
- Aggregations by region/segment/product
- A `RANK()` window function to find top customers by spend
- A `LAG()` window function to calculate month-over-month growth by region
- A running-total (cumulative sales) window function

Run it against any SQL engine after loading the CSV into a table called
`orders` (example using SQLite shown in the file's header comment).

## Key Insights

*(Auto-generated from the dataset on each run — actual numbers depend on your
data. Typical structure of findings:)*

- Overall profit margin sits in a healthy-but-improvable range, with clear
  differences in profitability by region and segment.
- One region consistently outperforms the others in total sales — a candidate
  for case-study analysis on what's working, to replicate in lower-performing
  regions.
- The Corporate/Consumer segment (whichever scores highest in your run) shows
  the best profit margin, suggesting where marketing spend may be most
  efficient.
- Discounting shows a measurable negative relationship with profit — useful
  evidence for setting discount policy thresholds rather than discounting
  reactively.

## Power BI Dashboard

Suggested dashboard layout:
- KPI cards: Total Sales, Total Profit, Profit Margin %, Total Orders
- Line chart: monthly sales trend with year filter
- Bar charts: sales by region, sales by category
- Top-10 table: products by sales (drill-through enabled)
- Slicers: Region, Segment, Category, Date Range

## Project Structure

```
03-sales-performance-dashboard/
├── data/                 # place superstore.csv here (not committed)
├── notebooks/            # optional Jupyter exploration
├── outputs/              # generated charts + clean export
├── sales_analysis.py     # main analysis script
├── sql_queries.sql       # SQL version of the analysis
└── README.md
```

## Author

Chirag — [LinkedIn](www.linkedin.com/in/chirag-kumar-0458a4251) · [GitHub](https://github.com/Chirag0103-01)
