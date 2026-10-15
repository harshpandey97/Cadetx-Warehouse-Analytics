# Week 2: Cleaning, missing values and integration

## Files
| File | What it is |
|---|---|
| `week-02-cleaning.ipynb` | Main notebook. Run top to bottom. Colab upload step included. |
| `data-cleaned/analytical_dataset.csv` | One row per product-branch (180 rows, 24 columns) |
| `docs/cleaning_log.csv` | Every cleaning rule applied, with rows affected |
| `docs/missing_values.csv` | Every column with blanks and the rule applied |
| `docs/validation_after_cleaning.csv` | 37 validation checks, all passing |
| `docs/feature_dictionary.csv` | Definitions of the 9 engineered features |
| `docs/analytical_dataset_dictionary.csv` | Definition, source and status for all 24 analytical columns |
| `docs/open_flags.csv` | Known problems that block use of some features |

## Missing values
Only one column has blanks: `purchase_orders.received_date` (2,370 of 24,000, 9.9%). A blank means the PO is still pending. It is kept blank, never imputed, and excluded from delivery and lead-time measures.

## Cleaning rules applied
- Text trimmed and dates parsed (no failures).
- Branch capacity text such as `45230 sqft` converted to a number, with the unit kept in its own column (6 of 6 parsed).
- Invoice IDs shared by more than one invoice are flagged, not dropped (393 rows). They are kept in sales views and excluded from payment features.
- Payment IDs shared by more than one payment are flagged, not dropped (403 rows).
- Payments on shared invoice IDs are flagged and excluded from payment features (417 rows).
- Revenue uses `line_total`. The 0 lines where it differs from quantity x unit price are flagged.
- ADJUSTMENT ledger movements (2,454) have no direction in the source. They are excluded from stock reconciliation until CadetX confirms.

## Validation
37 of 37 checks pass: row counts kept, primary keys unique (apart from the flagged shared IDs), no orphan foreign keys, and header and line revenue totals agree.

## Features
- **Monthly sales:** units and revenue per product and branch per month, KPI orders only (Cancelled and Returned excluded).
- **Average monthly units:** over the last 12 months.
- **Days of stock:** current stock divided by average daily OUT movement over the last 90 days.
- **Lead time:** actual days from PO order to receipt, per product (median 17.9 days, against a quoted median of 18 days). Mean gap to quoted lead time is 0.9 days.

## Open flags (block some features)
- **Stock quantities are implausible against demand.** Current stock is about 1,173 months of average demand. The ledger's OUT movements match KPI sales within 2%, so demand is consistent. The problem is the stock side.
- **Effects:** median days of stock is 52,625. No product-branch is flagged for reorder or stockout, and stock value totals about 281 billion. Do not use `days_of_stock`, `needs_reorder`, `is_stockout` or `stock_value` until CadetX confirms the unit.
- **Question for CadetX:** what unit are current stock and opening stock measured in, and do they match the ledger quantities?

## Open questions for CadetX (carried from Week 1)
1. Which sales order does each shared invoice ID belong to?
2. Are payment IDs meant to be unique?
3. Does an ADJUSTMENT add or remove stock?
4. What unit of measure is stock held in?
5. Confirm the excluded order statuses (Cancelled, Returned).

## How to run
1. Put the 12 CSVs in `data/raw/`.
2. Run all cells in `week-02-cleaning.ipynb`. The notebook stops if a validation check fails or a column with blanks has no rule.
3. Outputs appear in `data/cleaned/` and `docs/`.
