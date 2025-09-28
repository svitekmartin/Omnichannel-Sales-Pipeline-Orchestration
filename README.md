# Omnichannel Sales Data Pipeline-Orchestration & Unification (Shopify + Walmart)

Build a centralized, dbt-powered pipeline that merges Shopify e-commerce orders with Walmart in-store sales to deliver a single, trustworthy view of omnichannel performance.

---

## 🎯 Business Case

A mid-sized retailer struggled with siloed channel data (Shopify vs. Walmart). This project resolves that by modeling both sources in a unified Snowflake warehouse, enabling:

* **Revenue Tracking:** Real-time comparison of online vs. in-store sales.
* **Customer Insights:** Cross-channel behavior analysis to inform marketing and merchandising.
* **Operational Efficiency:** Automated reporting and fewer reconciliation errors.

End result: a fully automated ELT pipeline that ingests, transforms, tests, and publishes analytics-ready marts.

---

## 🛠️ Tech Stack

* **Transformation:** dbt (Core or Cloud)
* **Warehouse:** Snowflake
* **BI:** Looker Studio
* **Version Control:** Git / GitHub

---

## 📊 Data Sources

**Shopify Orders (e-commerce)**
Typical columns: `ORDER_ID, SKU, PRODUCT_NAME, CATEGORY, CHANNEL, CUSTOMER_EMAIL, PRICE, QUANTITY, ORDER_DATE, WEEK, YEAR`

**Walmart Sales (in-store)**
Typical columns:
`TRANSACTION_ID, PRODUCT_ID, PRODUCT_NAME, CATEGORY, CUSTOMER_AGE, CUSTOMER_GENDER, CUSTOMER_ID, CUSTOMER_INCOME, CUSTOMER_LOYALTY_LEVEL, FORECASTED_DEMAND, HOLIDAY_INDICATOR, INVENTORY_LEVEL, PAYMENT_METHOD, PROMOTION_APPLIED, PROMOTION_TYPE, QUANTITY_SOLD, REORDER_POINT, REORDER_QUANTITY, STOCKOUT_INDICATOR, STORE_ID, STORE_LOCATION, SUPPLIER_ID, SUPPLIER_LEAD_TIME, TRANSACTION_DATE, UNIT_PRICE, WEATHER_CONDITIONS, WEEKDAY, ACTUAL_DEMAND`

> Raw source files used to stage data into Snowflake live under the repo’s `data/` directory (for reference/reproducibility).

---

## 🧱 Data Modeling (dbt)

The project follows a three-layer approach:

1. **Staging** – normalize raw schemas, cast types, standardize naming, light cleaning.
2. **Intermediate** – business rules, filters, conforming dimensions, keys.
3. **Analytics (Marts)** – consolidated fact & dimension models, including the **`unified_sales`** table for BI.

(See the `models/` directory for model-by-model details.)

---

## 🚀 Quickstart

### 1) Clone

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

### 2) Prepare Snowflake

Ensure the following raw tables exist in `RETAIL_PROJECT.PUBLIC`:

* `SHOPIFY_ORDERS`
* `WALMART`

### 3) Configure dbt

* Install: `pip install dbt-snowflake` (for dbt Core), or use dbt Cloud.
* Set Snowflake credentials in `~/.dbt/profiles.yml` (Core) or in dbt Cloud (Account, User, Auth, Role, Warehouse, Database, Schema).
  *Do not commit secrets.*

### 4) Build & Test

```bash
# Build all models and run tests
dbt build

# Or run a specific mart
dbt run --select unified_sales
```

### 5) Docs (Optional, Recommended)

```bash
dbt docs generate
dbt docs serve
```

(In dbt Cloud, open the **Docs** tab.)

---

## 📈 Analysis

Once `unified_sales` is created, connect Snowflake to Looker Studio to explore:

* Channel mix, revenue, and units over time
* Product/Category performance by channel
* Customer segments and cross-channel behavior
* Promotion impact & inventory signals

(See the dashboard notes for commentary and next steps.)

---

## 📂 Repo Structure (excerpt)

```
data/                  # Reference raw files used for Snowflake staging
models/
  staging/             # Source-specific staging models
  intermediate/        # Business logic and conformed entities
  marts/
    unified_sales.sql  # Consolidated omnichannel fact/mart
tests/                 # dbt tests (schema + custom)
```

---

## ✅ What This Delivers

* A single source of truth for omnichannel sales
* Reusable, versioned transformations with dbt
* Automated testing + documentation
* BI-ready tables for downstream analytics

---

*About / Resources / Activity / Releases / Packages:*
This repository focuses on the pipeline and models; no releases or packages are currently published.
