# Week 07 Results Summary

**Project:** CadetX Heavy Supplier, Inventory & Warehouse Analytics
**Team:** [Team name]
**Analysis period:** 2026-09-30 to 2024-12-31

## D1: Supplier contribution (confirmed)

**Result:** Eight suppliers, all in China, supply 21,630 received purchase orders worth 312 billion. Each supplier holds between 12.1% and 12.9% of purchase value.
**Largest:** Tianjin OEM Supplies (SUP0005), 12.9%. **Smallest:** Guangzhou Local Vendor Supplies (SUP0002), 12.1%.
**Meaning:** No single supplier dependency. The concentration risk is at country level, since all suppliers are in China.
**Checks:** 2,370 cancelled POs excluded. Header totals match their lines on all received POs (0 mismatches).
**Source:** `output/week7_supplier_contribution.csv`

## D2: Supplier reliability (confirmed, with a data caveat)

**Result:**

| Supplier | On-time rate | Median lead time (days) |
|---|---|---|
| Tianjin OEM Supplies | 85.3% | 28 |
| Qingdao Distributor Supplies | 85.2% | 10 |
| Guangzhou Local Vendor Supplies | 85.0% | 10 |
| Shanghai Distributor Supplies | 85.0% | 16 |
| Shenzhen OEM Supplies | 84.9% | 19 |
| Ningbo Distributor Supplies | 84.8% | 18 |
| Suzhou Local Vendor Supplies | 84.7% | 12 |
| Hangzhou OEM Supplies | 84.2% | 26 |

**Meaning:** On-time performance is nearly identical across suppliers (84.2% to 85.3%), so timeliness does not separate them.
**Data caveat:** 80.4% of received POs arrive on the expected date, and days late range only from -3 to +7. Actual lead time equals quoted lead time for every supplier. The dates appear to be derived from the quoted lead time, so these results describe the data, not necessarily supplier behaviour.
**Not measurable:** fill rate and defect rate. The PO lines hold the ordered quantity only.
**Source:** `output/week7_supplier_reliability.csv`

## D3: Supplier cost per unit (confirmed)

**Result:** Cost per unit ranges from 13,671 (Guangzhou, SUP0002) to 14,132 (Hangzhou, SUP0008), a spread of about 3.4%.
**Meaning:** Guangzhou is 1.9% below the average cost per unit and Hangzhou 1.4% above. This is the only supplier measure that separates the suppliers, and the gap is small.
**Source:** `output/week7_supplier_cost_per_unit.csv`

## E1: Customer behaviour, delivered orders (confirmed)

**Result:**
- Delivered sales orders: 18,033 (1,967 cancelled excluded)
- All 500 customers have ordered
- Orders per customer: 36.1 on average
- Top 50 customers hold 14.3% of delivered order value

| Customer type | Customers | Avg orders | Value (billions) |
|---|---|---|---|
| Government | 114 | 35.7 | 6.43 |
| Corporate | 104 | 35.3 | 6.01 |
| Dealer | 99 | 36.7 | 5.97 |
| Fleet Owner | 95 | 36.4 | 5.62 |
| Retail | 88 | 36.3 | 5.22 |

**Meaning:** No customer concentration risk, and no customer type behaves differently on order frequency.
**Source:** `output/week7_customer_behaviour_delivered.csv`

## Charts and KPI file

Pending the Day 5 run. Expected outputs: `week7_chart1_supplier_share.png`, `week7_chart2_cost_per_unit.png`, `week7_chart3_customer_value.png`, and `week7_kpis.csv`.

## Headline findings

1. Purchase value is spread evenly across eight Chinese suppliers, so there is no supplier dependency.
2. On-time rate and lead time do not separate suppliers, and received dates follow the expected dates closely. The supplier reliability score in `suppliers.csv` is not supported by the order data.
3. Cost per unit varies by 3.4%, with Guangzhou the lowest and Hangzhou the highest.

## Recommended actions

1. Ask procurement to review the reliability score in `suppliers.csv`, since it doesn't match order performance.
2. Use the 3.4% cost gap to test whether moving volume to the lowest-cost supplier is viable.
3. Request received-quantity data from CadetX so fill rate and defect rate can be measured.

## Data issues

- 2,370 purchase orders are cancelled (not pending) and are excluded from supplier measures.
- Received dates equal expected dates for 80.4% of POs, which limits any on-time analysis.
- Fill rate and defect rate cannot be calculated from these files.
- Sales order counts in an earlier E1 pass included cancelled orders; the restated figures above use delivered orders only.
