# Week 04 Results Summary

**Project:** CadetX Heavy Supplier, Inventory & Warehouse Analytics
**Team:** [Team name]
**Sales period analysed:** 2019-01-01 to 2024-12-31 (2,192 days)

Each section gives the result, what it means for the business, and the file that supports it.

## B1: Product performance

**Result:** 30 of 30 products had sales. Total revenue was 25,447,392,560 at a gross margin of 21.6%.
**Concentration:** 10 products (33.3% of the range) generate 80% of revenue.
**Top products:** [Top 3 by revenue, from `product_performance.csv`]
**Revenue vs. units:** [Note any product that ranks high on one measure only, from the Day 2 output.]
**Meaning:** Revenue is concentrated in a minority of products, so stock and replenishment effort should be weighted towards them.
**Source:** `output/product_performance.csv`

## B2 and B3: Fast movers, slow movers, and dead stock

**Result:**
- Fast movers: [N] products (top 20% by velocity)
- Slow movers: [N] products (bottom 20% by velocity)
- Non-moving products: 0 (every product sold in the period)
- Dead stock: 0 products, 0 value

**Meaning:** No product has stock sitting without sales over the last 90 days. Capital is not tied up in dead stock. The question is whether stock is too high relative to sales, which is covered under B5.
**Sensitivity:** Not yet tested at 60 or 180 days.
**Source:** `output/movement_classification.csv`

## B4: Inventory turnover

**Result:** Turnover is 0.07x, equivalent to 30,889 days of inventory on hand.
**Meaning:** On this snapshot, stock value is far above annual cost of sales. This is the result that needs checking before it is reported as a finding (see Caveat).
**Caveat:** Uses a single stock snapshot, not average inventory over the period. The result also depends on the units check on sales vs. current stock, which is still open. Week 5 will correct the basis.

## B5: Stock health

**Result:**
- Overstock: 30 products, 281,292,677,410 in stock (100% of stock value on this snapshot)
- Understock: 0 products
- Healthy: 0 products
- Out of stock: 0 products

**Largest overstock by value:**

| Product | Stock on hand | Days of cover | Stock value |
|---|---|---|---|
| Engine Block EB-600 | 632,583 | 30,663 | 60,411,676,500 |
| Transmission Assembly TA-800 | 661,663 | 32,205 | 45,323,915,500 |
| Boom Cylinder BC-400 | 630,617 | 29,814 | 22,449,965,200 |
| Track Chain TC-45 | 638,882 | 30,728 | 20,763,665,000 |
| Swing Motor SWM-350 | 622,249 | 29,670 | 19,414,168,800 |
| Turbocharger TB-900 | 661,248 | 30,863 | 19,110,067,200 |
| Hydraulic Cylinder HC-200 | 650,389 | 30,586 | 13,983,363,500 |
| Hydraulic Pump HP-300 | 643,984 | 31,100 | 12,203,496,800 |
| Fuel Pump FP-350 | 632,290 | 30,198 | 10,369,556,000 |
| Control Valve CV-75 | 647,348 | 30,969 | 8,286,054,400 |

**Meaning:** Every product is above the 90-day overstock threshold, so the overstock flag does not separate products. Reporting this as a finding depends on the units check.
**Source:** `output/stock_health.csv`, `output/top10_overstock.csv`

## Charts

| Chart | What it shows | File |
|---|---|---|
| Revenue Pareto | How concentrated revenue is across products | `output/chart1_pareto_revenue.png` |
| Movement class | Product count vs. stock value by movement class | `output/chart2_movement_class.png` |
| Days of cover | Distribution of stock cover across products | `output/chart3_days_of_cover.png` |

**Chart 1 reading:** 10 products (33.3%) make up 80% of revenue.

## Headline findings

1. Revenue is concentrated: 10 of 30 products generate 80% of revenue.
2. No dead stock: all 30 products sold in the period, so no capital is tied up in products with no sales.
3. Overstock is universal on this snapshot: all 30 products show 30,000+ days of cover, with 281.3 billion in stock. This needs the units check before it is reported as final.

## Recommended actions

1. Prioritise replenishment and stock availability for the top 10 products.
2. Hold the overstock conclusion until the units check confirms current stock and sales are on the same scale. If confirmed, review ordering for the top 10 overstock products by value.
3. Re-run turnover on average inventory from month-end balances in Week 5 to remove the snapshot distortion.

## Data issues found

- Day 1 profiling found no nulls or duplicate rows across the four core tables.
- Turnover and overstock results depend on whether `current_stock` and `quantity` are on the same unit basis. Check pending.
