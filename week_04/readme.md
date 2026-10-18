# Week 04: Product and Inventory Performance

**Project:** CadetX Heavy Supplier, Inventory & Warehouse Analytics
**Team:** [Name 1 (Data Analyst)], [Name 2 (Data Analyst)], [Name 3 (Data Scientist)]
**Scrum Master this week:** [Name]
**Sprint goal:** Establish a baseline of product movement and inventory health.

## Scope

Week 4 covers Phase 2 tasks from the CadetX catalogue:

- B1: Product performance analysis
- B2: Fast-moving product identification
- B3: Slow-moving and dead stock identification
- B4: Inventory turnover analysis (snapshot basis)
- B5: Stock health assessment

## Data

Source: CadetX Heavy Supplier, Inventory & Warehouse Analytics dataset (CSV files).

Tables used:
- `products.csv`: 30 products, with names and unit costs
- `inventory_master.csv`: 180 rows of stock by product and branch
- `sales_orders_header.csv`: order dates
- `sales_orders_lines.csv`: 130,402 sales lines
- `stock_ledger.csv`: 237,230 movements, reviewed on Day 1 and used in later weeks

Sales period: 2019-01-01 to 2024-12-31 (2,192 days)

Day 1 profiling found no nulls and no duplicate rows in any of the four tables.

## Repository structure

```
week-04/
├── week04_analysis.py     # Day 1: load, profile, check joins
├── week04_day2.py         # Day 2: product performance (B1)
├── week04_day3.py         # Day 3: fast/slow movers and dead stock (B2, B3)
├── week04_day4.py         # Day 4: turnover and stock health (B4, B5)
├── week04_day5.py         # Day 5: charts, KPI summary
├── output/
│   ├── product_performance.csv
│   ├── movement_classification.csv
│   ├── stock_health.csv
│   ├── chart1_pareto_revenue.png
│   ├── chart2_movement_class.png
│   ├── chart3_days_of_cover.png
│   ├── week04_kpis.csv
│   └── top10_overstock.csv
└── README.md
```

## How to run

The workflow was run in Google Colab. Each day's code is a notebook cell, and the CSVs are in `/content/`. The Day 2 to Day 5 scripts are saved as files in `week-04/` for repeat runs on a local machine, where the paths would be `data/` and `week-04/output/`.

Order: Day 1 profiling, then Day 2 (product performance), Day 3 (movement and dead stock), Day 4 (turnover and stock health), Day 5 (charts and KPIs).

Day 4 uses `period_days = 2192`, taken from the Day 3 output.

## Method

**Day 1: Data checks**
- Profiled shape, columns, data types, nulls, and duplicate rows for each table.
- Checked that join keys exist in every table.
- Flagged negative quantities and products in sales missing from the product master.

**Day 2: Product performance (B1)**
- Excluded returns (quantity ≤ 0) from sales.
- Revenue = quantity × unit price. COGS = quantity × unit cost.
- Gross margin = revenue − COGS. Ranked products by revenue and by units.

**Day 3: Movement and dead stock (B2, B3)**
- Velocity = units sold ÷ days in the sales period (2,192 days).
- Fast = top 20% by velocity. Slow = bottom 20%. Medium = the rest. Non-moving = no sales.
- Dead stock = stock on hand > 0 and no sale in the last 90 days.

**Day 4: Turnover and stock health (B4, B5)**
- Turnover = total COGS ÷ stock value at cost (current snapshot).
- Days of inventory = period days ÷ turnover.
- Days of cover = stock on hand ÷ average daily units sold.
- Overstock > 90 days of cover. Understock < 7 days. Out of stock = zero on hand. No sales = stock but no sales in the period.

**Day 5: Charts and KPIs**
- Revenue Pareto curve, movement class chart, and days-of-cover histogram.
- KPI summary and top 10 overstock list, saved as CSV.

## Key results

| Metric | Value |
|---|---|
| Total COGS (sales period) | 19,961,848,170 |
| Stock value at cost (snapshot) | 281,292,677,410 |
| Inventory turnover | 0.07x |
| Days of inventory | 30,889 |
| Products classed as overstock | 30 of 30 |
| Overstock value | 281,292,677,410 |
| Products with sales | [from Day 5 KPI file] |
| Total revenue | [from Day 5 KPI file] |
| Gross margin % | [from Day 5 KPI file] |
| Dead stock value | [from Day 5 KPI file] |
| Dead stock products | [from Day 5 KPI file] |

**Status:** The Day 4 results above are from the notebook output and are pending a units check (see Limitations).

## Headline findings

1. [Finding with a number, once the units check is complete.]
2. [Finding with a number, from the Day 5 KPI file.]
3. [Finding with a number, from the Day 5 top 10 overstock list.]

## Recommended actions

1. [Action tied to finding 1.]
2. [Action tied to finding 2.]
3. [Action tied to finding 3.]

## Assumptions

- Returns (quantity ≤ 0) are excluded from sales. They will be handled in a later week.
- Velocity classes: top 20% fast, bottom 20% slow, rest medium.
- Dead stock uses a 90-day window. Results at 60 and 180 days are [to be tested / reported].
- Overstock is above 90 days of cover. Understock is below 7 days.
- Turnover uses the current stock snapshot, not average inventory over the period.

## Limitations

- **Overstock scale:** All 30 products are classed as overstock, with 30,000+ days of cover. This needs checking against total units sold before it is reported as a finding. A units or scale mismatch between the sales and inventory tables would produce the same result.
- **Turnover basis:** The snapshot can over- or understate turnover depending on how stock moved during the period. Week 5 will use month-end balances from `stock_ledger`.
- **Period length:** Turnover depends on `period_days`. Confirm it matches Day 3's output (2,192).

## Next week (Week 5)

- Average inventory from month-end balances in `stock_ledger`
- Inventory aging (B6)
- Turnover by product category and branch
