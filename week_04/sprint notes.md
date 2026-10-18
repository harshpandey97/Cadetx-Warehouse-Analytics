# Week 04 Sprint Notes

**Project:** CadetX Heavy Supplier, Inventory & Warehouse Analytics
**Scrum Master:** [Name]
**Team:** [Name 1 (Data Analyst)], [Name 2 (Data Analyst)], [Name 3 (Data Scientist)]
**Sprint goal:** Establish a baseline of product movement and inventory health.

## Planning

- Sprint planning meeting held on [date].
- Team selected Phase 2 tasks B1 to B5 from the catalogue.
- Work split: analysts took product performance, charts and KPIs; the data scientist took movement classification and the days-of-cover calculation.

## Tasks completed

| Task | Description | Status |
|---|---|---|
| B1 | Product performance | Done (Day 2) |
| B2 | Fast-moving products | Done (Day 3) |
| B3 | Slow-moving and dead stock | Done (Day 3) |
| B4 | Inventory turnover (snapshot basis) | Done, pending units check (Day 4) |
| B5 | Stock health | Done, pending units check (Day 4) |
| Charts and KPI summary | Pareto, movement class, days of cover | Done (Day 5) |

## Work done this week

- **Day 1:** Profiled all four core tables. Product master: 30 products. Inventory master: 180 rows. Sales lines: 130,402 rows. Stock ledger: 237,230 movements. No nulls or duplicates found.
- **Day 2:** Product performance from sales lines, excluding returns. Revenue, COGS, gross margin, and rankings by revenue and units.
- **Day 3:** Velocity over the sales period (2019-01-01 to 2024-12-31, 2,192 days). Fast, medium, slow, and non-moving classes. Dead stock flagged.
- **Day 4:** Turnover, days of inventory, and days of cover. Stock health classes assigned.
- **Day 5:** Three charts and KPI summary saved to `output/`.

## Key numbers

Day 4 output (from the notebook):
- Total COGS: 19,961,848,170
- Stock value at cost (snapshot): 281,292,677,410
- Inventory turnover: 0.07x
- Days of inventory: 30,889
- Products classed as overstock: 30 of 30

Day 5 KPI summary: [paste contents of `output/week04_kpis.csv`]

## Assumptions

- Returns (quantity ≤ 0) excluded from sales.
- Velocity classes: top 20% fast, bottom 20% slow, rest medium.
- Dead stock: stock on hand > 0 and no sale in the last 90 days.
- Overstock > 90 days of cover. Understock < 7 days.
- Turnover uses the current stock snapshot, not average inventory.

## Blockers and data issues

- **Overstock scale:** Every product shows 30,000+ days of cover. The units check (total units sold vs. current stock) has been run/[pending]. The overstock result is not reported as final until this is confirmed.
- **Script execution:** Day 3 and Day 4 scripts did not run as files in Colab. The code was run as notebook cells. The scripts are saved in `week-04/` for local reruns.
- [Add any other issues found, e.g. products in sales missing from products.csv.]

## Peer contributions

- [Name]: [what they did, e.g. Day 2 product performance, charts]
- [Name]: [what they did]
- [Name]: [what they did, e.g. movement classification, days-of-cover]

## Next week (Week 5)

- Replace snapshot inventory with average inventory from month-end balances in `stock_ledger`.
- Inventory aging (B6).
- Turnover by product category and branch.
- Confirm the overstock finding before building Week 5 analysis on it.

## Submission

- Repo link pasted into the CadetX portal: [date and status]
- Files committed: scripts, `output/`, `README.md`, `results.md`, this file.
