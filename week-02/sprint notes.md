# Sprint 2 (Week 2) notes

**Sprint goal:** Clean the 12 source tables, handle missing values, validate the cleaned data, and build one analytical dataset (one row per product and branch) for later weeks.

**Scrum Master:** Harsh Pandey (individual project)

## Task allocation
| Task | Owner | Status |
|---|---|---|
| Missing-value rule (one column with blanks: received_date) | Harsh Pandey | [x] Completed |
| Cleaning rules in code (spaces, dates, branch capacity, shared IDs, ADJUSTMENT) | Harsh Pandey | [x] Completed |
| Validation checks (row counts, unique keys, links between tables, revenue totals) | Harsh Pandey | [x] Completed: 25 of 25 pass |
| Monthly sales, days of stock and lead time features | Harsh Pandey | [x] Completed |
| Analytical dataset (180 rows, 18 columns) | Harsh Pandey | [x] Completed |
| Data dictionary for analytical dataset (18 columns, draft descriptions) | Harsh Pandey | [x] Completed: draft, verify against Fields Documentation |
| Stock unit confirmed with CadetX | Harsh Pandey | [ ] Open |
| README and sprint notes | Harsh Pandey | [x] Completed |
| Sprint 2 submitted in portal | Harsh Pandey | [ ] Not yet |

## Stand-up log
This is an individual project, so there are no team stand-ups. Progress was tracked in this file and the notebook run logs.
- **Planning:** goal set and tasks listed above.
- **Build:** notebook written, then simplified for readability. Run on the real 12 CSVs with no errors.
- **Submission:** repo updated and Sprint 2 submitted in portal: [ ]

## Results summary
- Tables loaded: 12 of 12 (sales lines 130,402; purchase lines 155,495; stock ledger 237,230)
- Validation checks: 25 of 25 pass (docs/validation_checks.csv)
- Missing values: 2,370 blank cells, all in purchase_orders.received_date (pending POs). Kept blank, not imputed.
- Branch capacity: 6 of 6 values converted to numbers, with the unit kept separately (sqft)
- Shared invoice IDs: 393 invoice rows flagged, kept
- Shared payment IDs: 403 payment rows flagged, kept
- ADJUSTMENT stock movements: 2,454 rows, direction unknown, excluded from stock checks
- Monthly sales: 12,955 product-branch-month rows (latest month December 2024)
- Median days from order to receipt: 17.9 days (quoted median 18 days)
- Analytical dataset: 180 product-branch pairs
- Median days of stock: 52,625, which is not plausible. Flagged in docs/open_flags.csv.

## Blockers and decisions
- **Stock unit (open flag):** current stock is about 1,173 months of average demand, so days of stock, stock value, reorder and stockout flags are not reliable. Do not use them until CadetX confirms the unit. Owner: Harsh Pandey.
- **Shared invoice IDs:** which sales order each ID belongs to. Owner: Harsh Pandey.
- **Shared payment IDs:** whether payment IDs are meant to be unique. Owner: Harsh Pandey.
- **ADJUSTMENT direction:** whether adjustments add or remove stock. Owner: Harsh Pandey.
- **Excluded order statuses:** confirm Cancelled and Returned are the right exclusions. Owner: Harsh Pandey.
