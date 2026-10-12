<div align="center">

<img src="assets/banner.svg" alt="CadetX Warehouse Analytics banner" width="900"/>
<br/>


![Last commit](https://img.shields.io/github/last-commit/HARSHPANDEY9756/cadetx-warehouse-analytics?style=for-the-badge&color=0969da)
![Stars](https://img.shields.io/github/stars/HARSHPANDEY9756/cadetx-warehouse-analytics?style=for-the-badge&color=8250df)
![Top language](https://img.shields.io/github/languages/top/HARSHPANDEY9756/cadetx-warehouse-analytics?style=for-the-badge&color=2da44e)
![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![SQL Server](https://img.shields.io/badge/SQL%20Server-T--SQL-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboards-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)

</div>

---

## About the project

A 12-week applied data project on heavy-equipment supply-chain data. The goal is to **reduce dead stock, prevent stockouts, and improve supplier reliability** across six warehouses.

The project covers supplier performance, inventory optimisation, warehouse operations, and demand forecasting.

## Dataset at a glance

<div align="center">
<img src="assets/dataset_size.svg" alt="Dataset size bar chart" width="760"/>
</div>

| Item | Value |
|---|---|
| Time period | 2019 – 2024 |
| Customers | 500 |
| Suppliers | 8 |
| Products (SKUs) | 30 |
| Warehouses (branches) | 6 |
| Purchase orders | 24,000 |

<div align="center">
<img src="assets/po_status.svg" alt="Purchase orders received vs pending" width="760"/>
</div>

> **Data note:** 2,370 purchase orders (9.9%) have no received date yet. They are flagged as *pending* and left blank, not filled in. The validation checks are recorded in `docs/validation_log.csv`.

<div align="center">
<img src="assets/movement_mix.svg" alt="Stock movement mix" width="760"/>
</div>

## Data model

```mermaid
erDiagram
    CUSTOMERS ||--o{ SALES_ORDERS_HEADER : places
    SALES_ORDERS_HEADER ||--|{ SALES_ORDERS_LINES : contains
    PRODUCTS ||--o{ SALES_ORDERS_LINES : sold_as
    SALES_ORDERS_HEADER ||--o| INVOICES : billed_by
    INVOICES ||--o{ PAYMENTS : settled_by
    SUPPLIERS ||--o{ PURCHASE_ORDERS_HEADER : receives
    PURCHASE_ORDERS_HEADER ||--|{ PURCHASE_ORDERS_LINES : contains
    PRODUCTS ||--o{ PURCHASE_ORDERS_LINES : bought_as
    BRANCHES ||--o{ INVENTORY_MASTER : stocks
    PRODUCTS ||--o{ INVENTORY_MASTER : tracked_in
    BRANCHES ||--o{ STOCK_LEDGER : records
    PRODUCTS ||--o{ STOCK_LEDGER : moves
```

## Roadmap

<div align="center">
<img src="assets/roadmap_progress.svg" alt="Roadmap progress bar" width="760"/>
</div>

- [ ] Week 1 — Dataset exploration and exploratory data analysis *(in progress)*
- [ ] Week 2 — Data cleaning and missing-value treatment
- [ ] Week 3 — SQL database design and data validation
- [ ] Week 4 — Supplier performance analysis
- [ ] Week 5 — Inventory health and dead-stock analysis
- [ ] Week 6 — Stockout and replenishment analysis
- [ ] Week 7 — Warehouse performance comparison
- [ ] Week 8 — Demand forecasting
- [ ] Week 9 — Inventory optimisation models
- [ ] Week 10 — KPI dashboard development in Power BI
- [ ] Week 11 — Model evaluation and business recommendations
- [ ] Week 12 — Final report, documentation, and deployment

## Week 1: Dataset exploration

### Team
| Name | Role | Ownership (from Week 2 onward) |
|---|---|---|
| Harsh Pandey | Analyst / Scrum Master (Week 1) | Inventory and warehouse |
| Harsh Pandey | Analyst | Supplier and customer |
| Harsh Pandey | Data scientist | Forecasting and risk models |

### Week 1 delivered
- Profiling of all 12 source tables (row counts, nulls, duplicates, primary keys)
- Relationship checks: 16 joins, orphan keys counted
- Cleaning and validation log (`docs/cleaning_log.csv`, `docs/validation_log.csv`)
- Inventory reconciliation: opening stock + IN − OUT vs current stock
- KPI definitions (10) and analysis questions (10) in `notebooks/week-01-eda.ipynb`, section 9
- Draft data dictionary (`docs/data_dictionary.csv`)

### Key findings (from the real data run)
- 2,370 of 24,000 purchase orders (9.9%) are pending, with no received date.
- [Finding 2: N payments are dated before their invoice]
- [Finding 3: N product-branch pairs do not reconcile to the stock ledger]

### Open items
- Data dictionary descriptions (fill from *Fields Documentation.docx*)
- Confirm business rules: excluded order statuses, payment-to-invoice link
- Decide action on each flagged check in the validation log

### How to run
1. Put the 12 CSVs in `data/raw/`.
2. Run all cells in `notebooks/week-01-eda.ipynb`.
3. Outputs appear in `data/cleaned/` and `docs/`.

### Week 1 outputs

| File | What it contains |
|---|---|
| `docs/table_summary.csv` | Row counts, duplicates, nulls and primary-key checks for all 12 tables |
| `docs/relationship_checks.csv` | 16 join checks with orphan-key counts |
| `docs/validation_log.csv` | Data-quality checks with rows failed and the proposed action |
| `docs/cleaning_log.csv` | Every cleaning change, with rows affected |
| `docs/data_dictionary.csv` | Column-level dictionary for the 12 source tables |

## Key KPIs

KPIs are calculated from validated source data. No unverified results are reported.

| Area | KPIs |
|---|---|
| Supplier | On-time delivery rate · Fulfilment rate · Average lead time · Defect rate · Reliability score |
| Inventory | Turnover ratio · Days of inventory on hand · Stockout rate · Dead-stock value · Carrying cost · Reorder-point accuracy |
| Warehouse | Fulfilment rate · Order cycle time · Backorder rate · Branch utilisation · Fill rate |
| Finance | Outstanding invoice value · Days sales outstanding · Purchase-order ageing |
| Forecasting | Forecast accuracy |

## Models to build

- Demand forecasting (statistical and machine-learning methods)
- Supplier reliability scoring
- Inventory segmentation using ABC analysis
- Reorder-point and safety-stock estimation
- Stockout risk prediction
- Dead-stock identification
- Inventory optimisation recommendations

## Quick start

**1. Clone the repository**

```bash
git clone https://github.com/HARSHPANDEY9756/cadetx-warehouse-analytics.git
cd cadetx-warehouse-analytics
```

**2. Create a virtual environment**

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

**3. Install dependencies**

```bash
python -m pip install --upgrade pip
pip install pandas numpy scikit-learn statsmodels matplotlib seaborn jupyter sqlalchemy
```

**4. Explore the dataset**

```bash
jupyter notebook notebooks/week-01-eda.ipynb
```

Put the 12 source CSVs in `data/raw/` first. The notebook writes its outputs to `data/cleaned/` and `docs/`.

**5. Run the data-cleaning pipeline**

```bash
python src/data_cleaning.py
```

**6. Rebuild the README charts (optional)**

Edit `assets/metrics.json`, then run:

```bash
python scripts/build_readme_assets.py
```

The charts also rebuild automatically on GitHub when `metrics.json` changes (see `.github/workflows/update-readme-assets.yml`).

**Prerequisites:** Python 3.8 or later, the project dataset (download from the CadetX portal), and the notebook and script files above. If the project uses SQL Server, configure the database connection separately.

## Technology stack

| Category | Tools |
|---|---|
| Programming | Python |
| Data analysis | Pandas, NumPy |
| Machine learning | Scikit-learn, Statsmodels |
| Visualisation | Matplotlib, Seaborn, Power BI |
| Database | SQL Server, T-SQL, SQLAlchemy |
| Development | Jupyter Notebook, Google Colab |
| Version control | Git, GitHub |

## Repository structure

```
cadetx-warehouse-analytics/
├── .github/workflows/update-readme-assets.yml
├── assets/              # SVG charts and metrics.json (used by this README)
├── data/                # Raw and cleaned data (large files are git-ignored)
│   ├── raw/             # the 12 source CSVs (not committed)
│   └── cleaned/         # generated by the notebook (not committed)
├── docs/                # validation_log.csv, cleaning_log.csv, relationship_checks.csv,
│                        # table_summary.csv, data_dictionary.csv
├── notebooks/           # week-01-eda.ipynb and later notebooks
├── scripts/             # build_readme_assets.py
├── src/                 # data_cleaning.py
├── .gitignore
├── README.md
└── requirements.txt
```

## Project progress

Progress is tracked in the roadmap above and in the chart at the top of that section. Add validated charts, model results, and Power BI screenshots as the project develops.

## Author

**Harsh Pandey** — Data Science Analyst

- GitHub: [github.com/harshpandey97](https://github.com/harshpandey97)
- LinkedIn: [linkedin.com/in/harsh-pandey-395a10237](https://www.linkedin.com/in/harsh-pandey-395a10237)
- Email: harshpandey6012@gmail.com

## License

Released under the MIT License. Add a `LICENSE` file to the repository to make this official.
