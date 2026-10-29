# Week 05: Refined Turnover, Inventory Aging, and Branch Analysis

**Project:** CadetX Heavy Supplier, Inventory & Warehouse Analytics
**Team:** [Name 1 (Data Analyst)], [Name 2 (Data Analyst)], [Name 3 (Data Scientist)]
**Scrum Master this week:** [Name]
**Sprint goal:** Replace the Week 4 snapshot turnover with an average-inventory basis, measure stock age, and locate where stock is building up.

## Scope

- B4 (refined): Inventory turnover on month-end average inventory
- B6: Inventory aging (approximate, see Limitations)
- Turnover by branch and by category, as additional cuts of B4

## Data

- `stock_ledger.csv`: 237,230 movements, 2019-01-01 to 2025-01-28
- `inventory_master.csv`: 180 product-branch rows
- `products.csv`: 30 products, unit costs and categories
- `sales_orders_header.csv` and `sales_orders_lines.csv`: COGS and branch of sale
- Week 4 output: `product_performance.csv` (COGS by product)

Analysis period for turnover: 2019-01-01 to 2024-12-31 (2,192 days). The ledger runs past this to 28 January 2025; aging uses that date as the as-of date.

## Repository structure

```
week-05/
├── README.md
├── results.md
├── output/
│   ├── week5_turnover_by_product.csv          (superseded, see Limitations)
│   ├── week5_turnover_by_product_corrected.csv
│   ├── week5_turnover_by_category_corrected.csv
│   ├── week5_turnover_by_branch.csv
│   ├── week5_aging_buckets.csv
│   ├── week5_aging_by_product.csv
│   ├── week5_kpis.csv
│   └── week5_chart1_turnover_by_branch.png
│   └── week5_chart2_aging.png
│   └── week5_chart3_turnover_by_category.png
```

## How to run

Run in Google Colab, in this order, with CSVs in `/content/`:

1. Day 1: reconcile ledger balances with `inventory_master.current_stock`
2. Day 2: month-end average inventory and turnover (product and total)
3. Day 3: FIFO inventory aging, with sign and ordering diagnostics
4. Day 4: turnover by category and by branch
5. Day 5: charts and KPI summary

Day 2 must be run before Day 4, since Day 4 reads the Day 2 outputs.

## Method

**Average inventory (B4 refined)**
- Month-end balance for each product and branch, taken from the last ledger movement in each month.
- Months with no movement carry the previous balance forward. Product and branch pairs start at 0 before their first movement.
- Value = balance × unit cost. Average inventory = mean over the 72 months, January 2019 to December 2024.
- Turnover = total COGS ÷ average inventory value. Days of inventory = 2,192 ÷ turnover.

**Inventory aging (B6)**
- FIFO: each receipt is a lot. Outbound movements consume the oldest lots first.
- Age = days from lot receipt date to the as-of date (28 January 2025).
- Buckets: 0 to 30, 31 to 90, 91 to 180, 181 to 365, over 365 days.

**Diagnostics**
- Balance change between consecutive ledger rows was compared with the recorded quantity for each movement type.

## Key results

| Metric | Value |
|---|---|
| Total COGS (2019 to 2024) | 19,961,848,170 |
| Average inventory value (month-end) | 140,733,247,081 |
| Turnover (average basis) | 0.14x |
| Days of inventory | 15,454 |
| Week 4 snapshot turnover (for comparison) | 0.07x |

**Reconciliation (Day 1):** total `current_stock` 19,303,266 vs. total ledger balance 19,304,792, a difference of 1,526 units (0.008%). 166 of 180 product-branch rows match exactly. The other 14 are within about 500 units.

**Branch turnover:**

| Branch | COGS | Average inventory | Turnover | Days of inventory |
|---|---|---|---|---|
| HYD001 | 2,706,527,690 | 23,839,330,000 (approx.) | 0.11x | 19,307 |
| PUN001 | 2,934,731,060 | 24,049,560,000 (approx.) | 0.12x | 17,963 |
| DEL001 | 3,034,255,720 | 23,726,610,000 (approx.) | 0.13x | 17,141 |
| AHM001 | 3,458,891,070 | 23,111,120,000 (approx.) | 0.15x | 14,646 |
| KOL001 | 3,755,788,160 | 22,170,740,000 (approx.) | 0.17x | 12,940 |
| CHN001 | 4,071,654,470 | 23,835,880,000 (approx.) | 0.17x | 12,832 |

**Category turnover:** all 15 categories fall between 0.13x and 0.15x. Transmission is lowest at 0.13x; Hydraulic and Sensors are highest at 0.15x.

**Stock age (approximate):**

| Age bucket | Units | Share of value |
|---|---|---|
| 0 to 30 days | 221,480 | 1.1% |
| 31 to 90 days | 641,705 | 3.3% |
| 91 to 180 days | 936,052 | 4.6% |
| 181 to 365 days | 1,870,067 | 9.8% |
| Over 365 days | 15,635,488 | 81.1% |

Oldest-on-average products (average lot age): Bucket Tooth BT-10 (949 days), Alternator ALT-500 (938), Swing Motor SWM-350 (938), Transmission Assembly TA-800 (937), Engine Oil Filter OF-90 (934).

## Headline findings

1. Stock is spread evenly across branches (about 22 to 24 billion each on average), but sales differ: COGS ranges from 2.7 billion (HYD001) to 4.1 billion (CHN001). Branches with the lowest sales carry the most stock relative to demand.
2. Average-basis turnover is 0.14x, twice the Week 4 snapshot figure of 0.07x. Stock built up over the period, so the snapshot overstated the end-of-period position.
3. About 81% of stock value on hand is over a year old (approximate, see Limitations).

## Recommended actions

1. Review replenishment at the two lowest-turnover branches, HYD001 and PUN001, before any further receipts.
2. Set a clearance or return review for stock older than 365 days, starting with the oldest-on-average products.
3. Confirm the aging result by correcting the ledger ordering issue (see Limitations) before using it for stock write-down decisions.

## Assumptions

- Turnover uses month-end balances; movements within a month are not reflected in the average.
- Stock is valued at current unit cost, not historical cost.
- Product-branch pairs with no movement in a month carry the last known balance.
- Aging uses FIFO, with the ledger's movement order as recorded.
- COGS uses the current unit cost, consistent with Week 4.

## Limitations

- **Ledger reconciliation:** about 20% of IN and OUT rows do not match their recorded quantities against the balance change. About 55,000 rows are affected, spread evenly across 2019 to 2024. About 11,300 of them are on days where the product and branch had only one movement, so ordering cannot explain them. The ledger has genuine inconsistencies in these rows.
- **Aging is approximate:** the mismatches can shift which lot is consumed, so bucket shares are estimates. The direction (most stock is old) is robust; the exact percentages are not.
- **Opening balances:** the first-row check in the diagnostic treated opening balances as zero. The correct opening balance is `inventory_master.opening_stock`. This affects up to 180 rows and is minor.
- **Ledger period:** the ledger runs to 28 January 2025, beyond the 2024-12-31 sales period. The turnover grid stops at December 2024, so this does not affect turnover.
- **Superseded files:** `week5_turnover_by_product.csv` and the first category table used a per-product average that captured roughly one branch's stock instead of all six. They are wrong and must not be reported. Use the `_corrected` files.
- **ADJUSTMENT movements:** ADJUSTMENT quantities are always positive, so their direction cannot be read from the quantity. They are excluded from the sign check and treated as recorded in the balance.

## Next week (Week 6)

- Warehouse space utilisation (C1) and throughput (C2), which are the remaining Phase 2 tasks.
- Overstock and understock detection (B8) on the corrected average-basis figures.
- Confirm the ledger ordering issue with the data owner, if one is available.
