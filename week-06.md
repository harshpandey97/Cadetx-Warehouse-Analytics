# Week 06 Sprint Notes

**Project:** CadetX Heavy Supplier, Inventory & Warehouse Analytics
**Scrum Master:** [Name]
**Team:** [Name 1 (Data Analyst)], [Name 2 (Data Analyst)], [Name 3 (Data Scientist)]
**Sprint goal:** Measure branch throughput and space use, and flag overstock and understock, separating confirmed results from those waiting on the stock unit.

## Planning

- Sprint planning meeting held on [date].
- Tasks: C2 (throughput), C1 (space utilisation), B8 (overstock and understock), charts and KPI summary.

## Tasks completed

| Task | Description | Status |
|---|---|---|
| C2 | Warehouse throughput by branch | Done (Day 3). Confirmed. |
| C1 | Warehouse space utilisation | Done (Day 2). Space share confirmed; utilisation against max provisional. |
| B8 | Overstock and understock flags | Done (Day 4). Provisional. |
| Charts and KPI summary | Throughput, space vs stock, days of cover | Done (Day 5). Days-of-cover chart provisional. |

## Work done this week

- **Day 1:** Checked branch, capacity, and inventory columns. Capacity text ("45230 sqft") converts cleanly to a number for all six branches. `sales_orders_header.csv` and `stock_ledger.csv` were not found after a session restart and were re-uploaded.
- **Day 2:** Space utilisation. Stock against `max_stock` is about 333 times the designed maximum, so it is reported as provisional. Space share and stock share are reported as relative figures.
- **Day 3:** Throughput over 72 months (2019 to 2024). Total OUT 1,121,633; total IN 20,218,956.
- **Day 4:** Overstock and understock flags. All 180 product-branch pairs flagged overstock; none understock. Median days of cover 38,170 (provisional).
- **Day 5:** Charts and KPI file saved. KPIs tagged confirmed or provisional.

## Key numbers

**Confirmed**
- Units sold per month, all branches: 15,578 (average)
- Highest-throughput branch: CHN001 (3,211 a month)
- Lowest-throughput branch: HYD001 (2,130 a month)
- Out-to-in ratio: 5.5%
- Floor space share range: 13.2% to 20.0%
- Stock share range: 16.2% to 17.0%

**Provisional**
- Overstock pairs: 180 of 180
- Understock pairs: 0
- Median days of cover: 38,170

## Assumptions

- Sales period: 2019-01-01 to 2024-12-31 (72 months). Ledger movements after this date are excluded.
- Average monthly OUT is a simple mean over 72 months, including months with no sales.
- Days per month for days of cover: 30.4.
- Floor space measured by `warehouse_capacity` in square feet.

## Blockers and data issues

- **Stock unit (open, blocking):** `current_stock` is about 333 times `max_stock`, and about 95% of received units are still on hand. CadetX has not yet confirmed whether stock and IN quantities are in units, cases, or pallets. All stock-based figures stay provisional until this is answered.
- **Session restart:** Colab cleared `/content/`, so the sales and ledger files had to be uploaded again. Keep the CSVs in the repo's `data/` folder or re-upload them at the start of each session.
- **Per-sqft measures:** not comparable across branches until the unit is confirmed.

## Peer contributions

- [Name]: [what they did]
- [Name]: [what they did]
- [Name]: [what they did]

## Next week (Week 7)

- Supplier and customer analytics (D and E tasks), using purchase order and sales order data.
- Re-run C1 and B8 once CadetX confirms the stock unit.

## Submission

- Repo link pasted into the CadetX portal: [date and status]
- Files committed: `week-06/` (scripts, output, README, results) and this file.
