# Sprint 1 (Week 1) notes

**Sprint goal:** Profile all 12 tables, define the join keys and KPIs, and produce a validated, reproducible Week 1 notebook.

**Scrum Master:** Harsh Pandey (individual project)

## Task allocation
| Task | Owner | Status |
|---|---|---|
| Profiling and primary keys | Harsh Pandey | [x] Completed |
| Relationship checks and ER diagram | Harsh Pandey | [x] Completed |
| Inventory reconciliation and stock checks | Harsh Pandey | [x] Completed |
| Purchasing and supplier timing checks | Harsh Pandey | [x] Completed |
| Invoice and payment checks | Harsh Pandey | [x] Completed |
| KPI definitions and analysis questions | Harsh Pandey | [x] Completed |
| Data dictionary descriptions | Harsh Pandey | [ ] Open: 134 of 135 descriptions still blank |
| README and sprint notes | Harsh Pandey | [x] Completed |

## Stand-up log
This is an individual project, so there are no team stand-ups. Progress was tracked in this file and the notebook run logs.
- **Planning:** goal set, tasks listed above.
- **Build:** notebook built, tested on synthetic data, then run on the real 12 CSVs. Two issues found and fixed: shared invoice IDs and shared payment IDs.
- **Submission:** repo link submitted in portal: [ ] Not yet

## Results summary
- Tables profiled: 12 of 12
- Relationships checked: 16, orphan keys: 0 (all PASS)
- Primary-key checks: 10 of 12 tables unique. `invoices` (197 shared IDs) and `payments` (202 shared IDs) are not unique.
- Validation checks flagged: 4 (shared invoice IDs, shared payment IDs, stock not reconciling exactly, ADJUSTMENT direction unknown)
- Inventory pairs reconciled: 1 of 180 exact; 180 of 180 within 1% of current stock
- Pending purchase orders: 2,370 of 24,000 (9.9%)

## Blockers and decisions
- **Shared invoice IDs (197 IDs, 393 rows):** excluded from payment KPIs. Ask CadetX which sales order each ID belongs to. Owner: Harsh Pandey.
- **Shared payment IDs (202 IDs, 403 rows):** kept, flagged as ID collisions. Ask CadetX whether payment IDs are meant to be unique. Owner: Harsh Pandey.
- **ADJUSTMENT movements (2,454 rows):** all quantities are positive, so direction is unknown. Excluded from reconciliation. Ask CadetX whether adjustments add or remove stock. Owner: Harsh Pandey.
- **Stock scale:** current stock is 88,853 to 121,013 units per product-branch, while the largest ledger movement is 300. Confirm the unit of measure and whether the ledger is complete. Owner: Harsh Pandey.
- **Business rules:** confirm excluded order statuses (Cancelled, Returned). Owner: Harsh Pandey.
