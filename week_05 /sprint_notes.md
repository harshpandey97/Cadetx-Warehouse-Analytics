# Week 05 Sprint Notes

**Project:** CadetX Heavy Supplier, Inventory & Warehouse Analytics
**Scrum Master:** [Name]
**Team:** [Name 1 (Data Analyst)], [Name 2 (Data Analyst)], [Name 3 (Data Scientist)]
**Sprint goal:** Replace the Week 4 snapshot turnover with an average-inventory basis, measure stock age, and locate where stock is building up.

## Planning

- Sprint planning meeting held on [date].
- Tasks: B4 (refined), B6, turnover by branch and category.

## Tasks completed

| Task | Description | Status |
|---|---|---|
| B4 refined | Turnover on month-end average inventory | Done (Day 2). Overall 0.14x. |
| B6 | Inventory aging (FIFO) | Done, approximate (Day 3) |
| Branch and category turnover | Additional cuts of B4 | Done (Day 4) |
| Charts and KPI summary | Branch, aging, category | Charts and KPI file pending: confirm Day 5 output |

## Work done this week

- **Day 1:** Reconciled ledger balances with `inventory_master`. 166 of 180 rows match exactly. Total difference 1,526 units (0.008%).
- **Day 2:** Month-end average inventory and turnover. Average inventory 140.7 billion; turnover 0.14x. The first per-product file was wrong and was corrected.
- **Day 3:** FIFO aging with diagnostics. About 20% of IN/OUT rows do not reconcile, so aging is reported as approximate.
- **Day 4:** Turnover by category and branch. Category results confirmed against branch and overall totals.
- **Day 5:** Charts and KPI file. [Pending run.]

## Key numbers

- Total COGS: 19,961,848,170
- Average inventory value: 140,733,247,081
- Turnover: 0.14x (Week 4 snapshot was 0.07x)
- Branch range: 0.11x (HYD001) to 0.17x (KOL001, CHN001)
- Stock over 365 days: about 81% of value (approximate)

## Assumptions

- Month-end balances represent each month; movements within a month are not reflected.
- Stock is valued at current unit cost.
- Aging uses FIFO on the ledger's recorded order.

## Blockers and data issues

- About 55,000 IN/OUT rows do not reconcile with their recorded quantities. About 11,300 cannot be explained by same-day ordering. Raise with the data owner if available.
- Ledger runs to 28 January 2025, past the sales period.
- First-row opening balances were treated as zero in the diagnostic. Minor.
- Earlier per-product and category files are superseded. Use the `_corrected` files.

## Peer contributions

- [Name]: [what they did]
- [Name]: [what they did]
- [Name]: [what they did]

## Next week (Week 6)

- Warehouse space utilisation (C1) and throughput (C2).
- Overstock and understock detection (B8) on the corrected figures.

## Submission

- Repo link pasted into the CadetX portal: [date and status]
- Files committed: week-05 scripts and output, README, results, and these sprint notes.
