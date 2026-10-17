# Week 1: Data Profiling and Validation

**Programme:** Heavy Supplier, Inventory & Warehouse Analytics (CadetX)
**Phase:** 1 · Foundation & Exploration
**Scrum Master:** Harsh Pandey (individual project)
**Status:** Completed, with one open item (data dictionary descriptions)

## Sprint goal

Profile all 12 tables, define the join keys and KPIs, and produce a validated, reproducible Week 1 notebook.

## Scope

The dataset consists of 12 CSV files supplied with the programme brief:

- branches.csv
- customers.csv
- inventory_master.csv
- invoices.csv
- payments.csv
- products.csv
- purchase_orders_header.csv
- purchase_orders_lines.csv
- sales_orders_header.csv
- sales_orders_lines.csv
- stock_ledger.csv
- suppliers.csv

The field reference is in `Fields Documentation.docx`.

## What was done

| Task | Status |
|---|---|
| Profiling and primary keys | Completed |
| Relationship checks and ER diagram | Completed |
| Inventory reconciliation and stock checks | Completed |
| Purchasing and supplier timing checks | Completed |
| Invoice and payment checks | Completed |
| KPI definitions and analysis questions | Completed |
| Data dictionary descriptions | Open: 134 of 135 descriptions still blank |
| README and sprint notes | Completed |

## Method

The notebook was first built and tested on synthetic data, then run on the 12 real CSV files. Two issues were found in the real data and fixed in the notebook: shared invoice IDs and shared payment IDs.

## Results

| Measure | Result |
|---|---|
| Tables profiled | 12 of 12 |
| Relationships checked | 16 |
| Orphan keys | 0 (all relationships PASS) |
| Tables with unique primary keys | 10 of 12 |
| Invoice ID collisions | 197 shared IDs |
| Payment ID collisions | 202 shared IDs |
| Validation checks flagged | 4 |
| Inventory pairs reconciled exactly | 1 of 180 |
| Inventory pairs within 1% of current stock | 180 of 180 |
| Pending purchase orders | 2,370 of 24,000 (9.9%) |

### Validation flags

1. Shared invoice IDs
2. Shared payment IDs
3. Stock not reconciling exactly
4. ADJUSTMENT direction unknown

## Blockers and decisions

| Issue | Decision | Owner | Question for CadetX |
|---|---|---|---|
| Shared invoice IDs: 197 IDs, 393 rows | Excluded from payment KPIs | Harsh Pandey | Which sales order does each ID belong to? |
| Shared payment IDs: 202 IDs, 403 rows | Kept and flagged as ID collisions | Harsh Pandey | Are payment IDs meant to be unique? |
| ADJUSTMENT movements: 2,454 rows, all positive | Excluded from reconciliation | Harsh Pandey | Do adjustments add or remove stock? |
| Stock scale: current stock 88,853 to 121,013 per product-branch; largest ledger movement 300 | Open | Harsh Pandey | What is the unit of measure, and is the ledger complete? |
| Excluded order statuses (Cancelled, Returned) | Open | Harsh Pandey | Are these the correct exclusions? |

## Open items

- Complete the 134 blank data dictionary descriptions.
- Get answers from CadetX on the five questions above.
- Submit the repository link in the portal Submission area (not yet submitted).

## Folder contents

- `README.md`: this file
- `sprint-notes-week1.md`: sprint notes (to be added)
- Notebook and run logs: to be added to this folder
