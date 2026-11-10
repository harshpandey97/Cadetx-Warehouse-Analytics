# Week 07 Sprint Notes

**Project:** CadetX Heavy Supplier, Inventory & Warehouse Analytics
**Scrum Master:** [Name]
**Team:** [Name 1 (Data Analyst)], [Name 2 (Data Analyst)], [Name 3 (Data Scientist)]
**Sprint goal:** Measure supplier contribution, reliability, and cost, and summarise customer purchase behaviour, using validated data only.

## Planning

- Sprint planning meeting held on [date].
- Tasks: D1, D2, D3, E1, charts and KPI summary.

## Tasks completed

| Task | Description | Status |
|---|---|---|
| D1 | Supplier contribution | Done (Day 2). Confirmed. |
| D2 | Supplier reliability | Done (Day 3). Confirmed, with date caveat. |
| D3 | Supplier cost per unit | Done (Day 4). Confirmed. |
| E1 | Customer purchase behaviour | Done (Day 4, restated on delivered orders). Confirmed. |
| Charts and KPI summary | Supplier share, cost per unit, customer value | Pending: Day 5 run to confirm. |

## Work done this week

- **Day 1:** Checked all seven required files and their columns. Found that the 2,370 POs without a received date are **Cancelled**, not pending.
- **Day 2:** Supplier value shares (12.1% to 12.9%). Header totals match their lines on all received POs.
- **Day 3:** On-time rate (84.2% to 85.3%). Received dates equal expected dates for 80.4% of POs, so the date data needs a caveat. Reliability score in `suppliers.csv` does not match order performance.
- **Day 4:** Cost per unit (3.4% spread). Customer behaviour restated on delivered orders after an earlier pass included cancelled orders.

## Key numbers

- Received POs: 21,630 (cancelled excluded: 2,370)
- Purchase value: 312 billion
- Delivered sales orders: 18,033 (cancelled excluded: 1,967)
- Orders per customer: 36.1
- Top 50 customers' value share: 14.3%

## Assumptions

- Only Received POs and Delivered sales orders are used.
- Average cost per unit is the simple mean of the eight suppliers.

## Blockers and data issues

- **Received dates match expected dates for 80.4% of POs.** Lead-time and on-time results describe the data, not confirmed supplier behaviour. Raise with CadetX.
- **Fill rate and defect rate cannot be measured.** No received-quantity or defect data in the files. Request from CadetX.
- **Reliability score** in `suppliers.csv` does not follow order performance.
- **Earlier pending label:** README text from Weeks 1 and 2 called the 2,370 blank-date POs "pending". They are cancelled. Correct in those READMEs.

## Peer contributions

- [Name]: [what they did]
- [Name]: [what they did]
- [Name]: [what they did]

## Next week (Week 8)

- Demand forecasting (F tasks) and supplier risk checks (D4, D5).

## Submission

- Repo link pasted into the CadetX portal: [date and status]
- Files committed: `week-07/` (output, README, results) and this file.
