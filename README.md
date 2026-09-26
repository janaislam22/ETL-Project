# Sales ETL Pipeline & Flask Dashboard

An end-to-end data engineering project that extracts, cleans, and transforms data from three sources, loads it into SQL Server, and visualizes it through a Flask web dashboard.

## 📌 Overview

This project builds a complete ETL (Extract, Transform, Load) pipeline in Python that combines three data sources into a unified **Sales** table, stores it in **SQL Server**, and serves it through a **Flask dashboard**.

### Data Sources
- `customers.csv` — local file
- `orders.parquet` — local file
- `products.csv` — fetched via API from a [GitHub raw URL](https://raw.githubusercontent.com/MohammedHameds/test1455/refs/heads/main/products.csv)

## 🔄 ETL Pipeline

### 1. Extract
- Read `customers.csv` and `orders.parquet` from local storage
- Fetch `products.csv` from the remote API endpoint

### 2. Transform

**Customers**
- Remove duplicate records
- Standardize city names (consistent casing/formatting)
- Validate age values (flag/remove invalid entries)
- Handle missing email fields
- Create a derived `full_name` column

**Orders**
- Remove duplicate `order_id` entries
- Validate `quantity` values
- Convert `order_date` to proper datetime format
- Validate `customer_id` references

**Products**
- Remove duplicate records
- Standardize product name and category formatting
- Validate `unit_price` values
- Convert price fields to numeric type

### 3. Merge & Calculate

The three cleaned datasets are merged on their key columns, and total revenue per order line is calculated:

```python
sales["total_amount"] = sales["quantity"] * sales["unit_price"]
```

**Final Sales table schema:**

| Column | Description |
|---|---|
| order_id | Unique order identifier |
| customer | Customer full name |
| product | Product name |
| quantity | Units ordered |
| unit_price | Price per unit |
| total_amount | quantity × unit_price |

### 4. Load

The final `Sales` table is loaded into a **SQL Server** database, ready for querying and reporting.

## 🌐 Flask Dashboard

A Flask web application that:
1. Connects to the SQL Server database
2. Retrieves the `Sales` table
3. Renders the data in an interactive HTML dashboard

## 🛠️ Tech Stack

- **Python** — pandas for data cleaning & transformation
- **SQL Server** — data warehouse / storage layer
- **Flask** — web application framework
- **HTML/CSS** — dashboard front-end

## 📂 Project Structure

```
flask_task/
├── templates/
│   └── dashboard.htm
├── app1.ipynb
├── customers.csv
├── orders.parquet
└── sales_final
```

