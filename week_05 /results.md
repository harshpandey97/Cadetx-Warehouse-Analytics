# Week 05 Results Summary

**Project:** CadetX Heavy Supplier, Inventory & Warehouse Analytics
**Team:** [Team name]
**Analysis period:** 2019-01-01 to 2024-12-31 (2,192 days). Aging as of 2025-01-28.

## B4 (refined): Inventory turnover

**Result:** Turnover is 0.14x on a month-end average basis, equivalent to 15,454 days of inventory. Average inventory value is 140,733,247,081 against COGS of 19,961,848,170.
**Meaning:** Week 4 used a single snapshot and showed 0.07x. The average basis is the more reliable figure, and it shows stock was building up across the period rather than only at the end.
**Source:** `output/week5_turnover_by_product_corrected.csv`

## Turnover by branch

**Result:**

| Branch | Turnover | Days of inventory |
|---|---|---|
| HYD001 | 0.11x | 19,307 |
| PUN001 | 0.12x | 17,963 |
| DEL001 | 0.13x | 17,141 |
| AHM001 | 0.15x | 14,646 |
| KOL001 | 0.17x | 12,940 |
| CHN001 | 0.17x | 12,832 |

**Meaning:** Average stock is similar across branches, but sales are not. HYD001 has the lowest turnover and the highest days of inventory.
**Source:** `output/week5_turnover_by_branch.csv`

## Turnover by category

**Result:** All 15 categories fall between 0.13x and 0.15x. Transmission is lowest (0.13x). Hydraulic and Sensors are highest (0.15x).
**Meaning:** Category turnover is close to the overall average. The branch differences are the stronger signal.
**Source:** `output/week5_turnover_by_category_corrected.csv`

## B6: Inventory aging (approximate)

**Result:**

| Age | Units | Share of value |
|---|---|---|
| 0 to 30 days | 221,480 | 1.1% |
| 31 to 90 days | 641,705 | 3.3% |
| 91 to 180 days | 936,052 | 4.6% |
| 181 to 365 days | 1,870,067 | 9.8% |
| Over 365 days | 15,635,488 | 81.1% |

**Meaning:** Most stock on hand is over a year old. The direction is reliable; the exact percentages are estimates because about 20% of ledger rows do not reconcile.
**Source:** `output/week5_aging_buckets.csv`, `output/week5_aging_by_product.csv`

## Charts

| Chart | What it shows | File |
|---|---|---|
| Turnover by branch | Branch turnover against overall average | `output/week5_chart1_turnover_by_branch.png` |
| Aging | Share of stock value by age bucket | `output/week5_chart2_aging.png` |
| Turnover by category | Category turnover against overall average | `output/week5_chart3_turnover_by_category.png` |

## Headline findings

1. Branch turnover ranges from 0.11x (HYD001) to 0.17x (KOL001 and CHN001), while average stock is about 22 to 24 billion at every branch.
2. Average-basis turnover (0.14x) is twice the Week 4 snapshot figure (0.07x).
3. About 81% of stock value is over a year old (approximate).

## Recommended actions

1. Review replenishment at HYD001 and PUN001 before further receipts.
2. Set a clearance or return review for stock over 365 days, starting with the oldest-on-average products (BT-10, ALT-500, SWM-350, TA-800, OF-90).
3. Correct the ledger ordering issue before using aging for write-down decisions.

## Data issues

- About 55,000 IN and OUT ledger rows do not reconcile with their recorded quantities. About 11,300 of these are on days with a single movement for that product and branch.
- The ledger runs to 28 January 2025, past the 2024-12-31 sales period.
- The first-row check treated opening balances as zero. The correct opening balance is `inventory_master.opening_stock`.
- The first Day 2 product file and first category table are wrong (per-product averages captured about one branch's stock). Do not report them.
