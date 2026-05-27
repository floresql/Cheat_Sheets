# Medallion Architecture Folder Structure Cheat Sheet

A quick reference guide for structuring directories in a modern Data Lakehouse (Databricks, Fabric, Snowflake, AWS S3).

---

## Core Directory Hierarchy

```text
lakehouse/
├── 01_bronze/          # Raw, untouched source data
│   ├── salesforce/     # Organized by source system
│   └── stripe/
├── 02_silver/          # Cleansed, deduplicated, enriched data
│   ├── finance/        # Organized by business domain
│   └── marketing/
└── 03_gold/            # Aggregated, business-ready data
    ├── customer_360/   # Organized by use-case / data mart
    └── executive_dash/
```

---

## Layer Breakdown & Folder Naming Rules

### 🥉 1. Bronze Layer (`01_bronze` / `raw`)
* **Purpose**: Landing zone for untransformed data copied "as-is" from external sources.
* **Folder Pattern**: `bronze/[source_system]/[table_or_object]/`
* **Examples**: 
  * `bronze/salesforce/accounts/`
  * `bronze/stripe/charges/`
* **Tech Tip**: Use alphanumeric prefixes (e.g., `01_bronze`) to force files to sort chronologically in UI sidebars.

### 🥈 2. Silver Layer (`02_silver` / `staging` / `cleansed`)
* **Purpose**: Cleansed, validated, and conformed data. Houses enterprise-wide foundational tables.
* **Folder Pattern**: `silver/[business_domain]/[entity]/`
* **Examples**: 
  * `silver/finance/transactions/`
  * `silver/marketing/campaign_performance/`
* **Tech Tip**: Keep data at the same grain as the Bronze layer, but enforce schemas and fix data types here.

### 🥇 3. Gold Layer (`03_gold` / `marts` / `core`)
* **Purpose**: Aggregated, project-specific, business-ready data optimized for BI reporting and ML.
* **Folder Pattern**: `gold/[use_case_or_mart]/[fact_or_dimension]/`
* **Examples**: 
  * `gold/customer_360/dim_customers/`
  * `gold/executive_dash/fact_monthly_revenue/`
* **Tech Tip**: Use `dim_` and `fact_` prefixes inside Gold folders to easily identify dimensional modeling structures.

---

## Naming Conventions & Best Practices

* **Case Style**: Always use `snake_case` for folder and table names. Avoid spaces.
* **No Abbreviations**: Spell out words completely (e.g., `customer_orders`, not `cust_ord`).
* **Singular vs Plural**: Pick a standard and stick to it. Plural is preferred for folders (e.g., `users/`), singular for tables (e.g., `user`).
* **Hidden Folders**: Prefix metadata, checkpoints, or schema files with an underscore (`_checkpoints/`) to hide them from standard directory listings.
