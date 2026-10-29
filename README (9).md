# Week 06: Warehouse Throughput, Space Utilisation, and Overstock Flags

**Project:** CadetX Heavy Supplier, Inventory & Warehouse Analytics
**Team:** [Name 1 (Data Analyst)], [Name 2 (Data Analyst)], [Name 3 (Data Scientist)]
**Scrum Master this week:** [Name]
**Sprint goal:** Measure branch throughput and space use, and flag overstock and understock, separating confirmed results from those waiting on the stock unit.

## Scope

- C2: Warehouse throughput by branch (confirmed)
- C1: Warehouse space utilisation (partly provisional)
- B8: Overstock and understock detection (provisional)

## Data

- `branches.csv`: branch name, region, warehouse type, and capacity (text such as "45230 sqft", converted to a number)
- `inventory_master.csv`: current, opening, and maximum stock by product and branch
- `stock_ledger.csv`: IN, OUT, and ADJUSTMENT movements, 2019-01-01 to 2025-01-28
- `sales_orders_header.csv`: order dates and branch

Sales period: 2019-01-01 to 2024-12-31 (72 months). Ledger movements after this date are excluded.

## Repository structure

```
week-06/
├── README.md
├── results.md
└── output/
    ├── week6_throughput_by_branch.csv
    ├── week6_monthly_movements_by_branch.csv
    ├── week6_space_utilisation.csv
    ├── week6_overstock_understock_flags.csv
    ├── week6_kpis.csv
    ├── week6_chart1_throughput.png
    ├── week6_chart2_space_vs_stock.png
    └── week6_chart3_days_of_cover_PROVISIONAL.png
```

## How to run

Run in Google Colab, in this order, with CSVs in `/content/`:

1. Day 1: check branch, capacity, and inventory columns
2. Day 2: space utilisation per branch (C1)
3. Day 3: throughput per branch and month (C2)
4. Day 4: overstock and understock flags (B8)
5. Day 5: charts and KPI summary

Day 4 reads the Day 3 monthly file, so run Day 3 first. Day 4 also reads the Week 5 corrected product file.

## Method

**Capacity:** `warehouse_capacity` text converted to a number (square feet). All six branches convert cleanly.

**Space utilisation (C1)**
- Stock-to-maximum utilisation: current stock ÷ `max_stock`. Provisional.
- Space share vs stock share: each branch's share of total floor space compared with its share of total stock units. This needs no unit and is reported as a relative figure.
- Units per 1,000 sqft: provisional.

**Throughput (C2)**
- Monthly OUT units per branch, averaged over 72 months.
- Out-to-in ratio: total OUT ÷ total IN.
- Peak month: highest single-month OUT for the branch.

**Overstock and understock (B8)**
- Average monthly OUT per product and branch over 72 months.
- Days of cover = current stock ÷ (average monthly OUT ÷ 30.4).
- Overstock: current stock above `max_stock`. Understock: below `safety_stock`. Below reorder: below `reorder_level`.
- Status is provisional because current stock depends on the unconfirmed unit.

## Key results

| Result | Value | Status |
|---|---|---|
| Units sold per month, all branches | 15,578 | Confirmed |
| Highest-throughput branch | CHN001 (3,211 a month) | Confirmed |
| Lowest-throughput branch | HYD001 (2,130 a month) | Confirmed |
| Out-to-in ratio, all branches | 5.5% | Confirmed |
| Floor space share range | 13.2% to 20.0% | Confirmed |
| Stock share range | 16.2% to 17.0% | Confirmed |
| Overstock pairs (of 180) | 180 | Provisional |
| Understock pairs (of 180) | 0 | Provisional |
| Median days of cover | 38,170 | Provisional |

Full tables are in `results.md`.

## Headline findings

1. Throughput is confirmed and differs by branch, from 2,130 units a month at HYD001 to 3,211 at CHN001.
2. Stock is spread almost evenly across branches, while floor space is not. KOL001 holds more stock than its space share.
3. Every product-branch pair is flagged overstock. This reflects the stock unit question, not a finding yet.

## Recommended actions

1. Use confirmed throughput to set branch replenishment priorities, starting with CHN001.
2. Confirm the stock unit and IN-quantity unit with CadetX, then re-run B8 and the per-sqft measures.
3. Review KOL001 stock against floor space once the unit is confirmed.

## Assumptions

- Sales period is 2019-01-01 to 2024-12-31 (72 months).
- Average monthly OUT is a simple mean over 72 months, including months with no sales.
- Days per month for days of cover is 30.4.
- Space share uses `warehouse_capacity` in square feet as the measure of floor space.

## Limitations

- **Stock unit:** `current_stock` is about 333 times `max_stock`, and about 95% of received units are still on hand. Until the unit is confirmed, all stock-based figures (utilisation, overstock, understock, days of cover) are provisional.
- **Per-sqft measures:** units per square foot depend on the stock unit and are not comparable across branches yet.
- **Ledger period:** movements after 2024-12-31 are excluded, so totals may differ slightly from full-ledger totals.

## Next week (Week 7)

- Supplier and customer analytics (D and E tasks), using purchase order and sales order data.
- Re-run C1 and B8 once CadetX confirms the stock unit.
