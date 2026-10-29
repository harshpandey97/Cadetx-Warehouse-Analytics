# Week 06 Results Summary

**Project:** CadetX Heavy Supplier, Inventory & Warehouse Analytics
**Team:** [Team name]
**Sales period analysed:** 2019-01-01 to 2024-12-31 (72 months)

Each result is marked **confirmed** (depends only on sales and ledger quantities that reconcile) or **provisional** (depends on the stock unit, which CadetX has not yet confirmed).

## C2: Throughput by branch (confirmed)

**Result:** The six branches sell 15,578 units a month on average, a total of 1,121,633 units over the period.

| Branch | Avg units sold per month | Peak month | Out-to-in ratio |
|---|---|---|---|
| CHN001 | 3,211 | 5,138 | 6.7% |
| KOL001 | 2,909 | 4,148 | 6.4% |
| AHM001 | 2,697 | 3,795 | 5.9% |
| DEL001 | 2,346 | 3,518 | 4.9% |
| PUN001 | 2,285 | 3,310 | 4.9% |
| HYD001 | 2,130 | 3,007 | 4.6% |

**Meaning:** Chennai (CHN001) moves the most stock and Hyderabad (HYD001) the least. Monthly peaks run at about 1.4 to 1.6 times the average at every branch, so demand is fairly steady.
**Note:** Overall out-to-in ratio is 5.5%. Branch ratios are within normal variation of that figure.
**Source:** `output/week6_throughput_by_branch.csv`, `output/week6_monthly_movements_by_branch.csv`

## C1: Space utilisation (provisional)

**Result:**

| Branch | Share of floor space | Share of stock units | Gap (points) |
|---|---|---|---|
| KOL001 | 13.2% | 16.2% | +3.0 |
| AHM001 | 15.1% | 16.3% | +1.2 |
| HYD001 | 16.0% | 16.8% | +0.8 |
| PUN001 | 17.1% | 16.9% | -0.2 |
| CHN001 | 18.5% | 16.8% | -1.7 |
| DEL001 | 20.0% | 17.0% | -3.0 |

Current stock is 333 times the designed maximum (`max_stock`) across all branches, so stock-to-maximum utilisation is not reported as a finding.

**Meaning (confirmed, unit-free):** Stock is spread almost evenly across branches, but floor space is not. KOL001 holds more stock than its space share, while DEL001 has the most space and the lowest stock share relative to it.
**Provisional:** Units per 1,000 sqft (CHN001 77, KOL001 97) depends on the stock unit.
**Source:** `output/week6_space_utilisation.csv`

## B8: Overstock and understock (provisional)

**Result:**
- Overstock: 180 of 180 product-branch pairs
- Understock: 0
- Below reorder level: 0
- Median days of cover: 38,170

**Meaning:** The flags are correct under the current data, but they cannot be used as findings. Every pair appears overstocked and none appear short, which points to a units or scale problem in the stock data rather than a business result. This matches the overstock flag reported in Week 4 and the aging result in Week 5.
**Source:** `output/week6_overstock_understock_flags.csv`

## Charts

| Chart | Status | File |
|---|---|---|
| Throughput by branch | Confirmed | `output/week6_chart1_throughput.png` |
| Space share vs stock share | Relative | `output/week6_chart2_space_vs_stock.png` |
| Days of cover | Provisional | `output/week6_chart3_days_of_cover_PROVISIONAL.png` |

## KPI summary

| KPI | Value | Status |
|---|---|---|
| Units sold per month, all branches (avg) | 15,578 | Confirmed |
| Highest-throughput branch | CHN001 | Confirmed |
| Lowest-throughput branch | HYD001 | Confirmed |
| Out-to-in ratio, all branches | 5.5% | Confirmed |
| Overstock pairs (of 180) | 180 | Provisional |
| Understock pairs (of 180) | 0 | Provisional |
| Median days of cover | 38,170 | Provisional |

## Headline findings

1. Throughput is confirmed and differs by branch: Chennai sells 51% more units a month than Hyderabad.
2. Stock is spread evenly across branches, while floor space is not. Kolkata holds the largest stock share relative to its space.
3. Every product-branch pair is flagged overstock, which is a data question to resolve with CadetX, not a finding yet.

## Recommended actions

1. Use throughput (confirmed) to set branch replenishment priorities, starting with Chennai.
2. Ask CadetX to confirm the stock unit and whether IN quantities are recorded in units, cases, or pallets. Re-run B8 and the per-sqft measures after the answer.
3. Review Kolkata's stock against its floor space once the unit is confirmed.

## Data issues

- `current_stock` is about 333 times `max_stock` across all branches; the unit is unconfirmed.
- Total IN (20.2 million units) is about 18 times total OUT (1.1 million), and about 95% of received units are still on hand.
- `sales_orders_header.csv` and `stock_ledger.csv` were not found in `/content/` after a session restart and had to be re-uploaded.
