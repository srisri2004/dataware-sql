# dataware-sql

# Sales Data Warehouse

## 📌 Project Overview

This project implements a **Sales Data Warehouse** using **MySQL**. It follows a dimensional data modeling approach with **Fact and Dimension tables** to support sales reporting and analytics.

The warehouse stores customer, product, date, and sales transaction data in a structured format.

## 🛠️ Technologies Used

- MySQL
- SQL
- Data Warehousing
- Dimensional Modeling
- Star Schema
- SCD Type 2

## 🏗️ Data Warehouse Architecture

The project uses a **Star Schema**:

```text
                 dim_customer
                      |
                      |
dim_date ------ fact_sales ------ dim_product
```

### Dimension Tables

#### 1. `dim_customer`

Stores customer information and maintains historical changes using **SCD Type 2**.

Important columns:
- `customer_key` – Surrogate key
- `customer_id` – Business/customer ID
- `customer_name` – Customer name
- `email` – Customer email
- `city` – Customer city
- `state` – Customer state
- `start_date` – Record validity start date
- `end_date` – Record validity end date
- `is_current` – Indicates the current customer record

#### 2. `dim_product`

Stores product information.

Important columns:
- `product_key` – Surrogate key
- `product_id` – Product ID
- `product_name` – Product name
- `category` – Product category
- `price` – Product price

#### 3. `dim_date`

Stores calendar information for sales analysis.

Includes:
- Date
- Day
- Month
- Month name
- Quarter
- Year

### Fact Table

#### `fact_sales`

Stores sales transactions and connects the dimension tables.

Important columns:
- `sales_key` – Unique sales transaction key
- `date_key` – Date dimension reference
- `customer_key` – Customer dimension reference
- `product_key` – Product dimension reference
- `quantity` – Quantity sold
- `unit_price` – Price per unit
- `total_amount` – Total sales amount

### Staging Table

#### `staging_customer`

Temporary/staging table used to load customer data before inserting or updating records in the customer dimension.

## 🔄 Data Flow

```text
Source Data
     ↓
Staging Customer
     ↓
Dimension Tables
     ↓
Fact Sales
     ↓
Reporting & Analytics
```

## 📊 Key Concepts Demonstrated

- Data Warehouse Design
- Star Schema
- Fact Tables
- Dimension Tables
- Surrogate Keys
- Foreign Keys
- Staging Tables
- SCD Type 2
- Historical Data Tracking
- Relational Data Modeling
- Sales Analytics

## 🚀 How to Run

### 1. Create the Database

Run the SQL script in MySQL:

```sql
CREATE DATABASE sales_data_warehouse;
USE sales_data_warehouse;
```

### 2. Create Tables

Execute the table creation statements for:

```text
dim_customer
dim_product
dim_date
staging_customer
fact_sales
```

### 3. Load Data

Load source customer, product, date, and sales data into the staging and dimension tables.

### 4. Verify Tables

```sql
SHOW TABLES;
```

Check the data:

```sql
SELECT * FROM dim_customer;
SELECT * FROM dim_product;
SELECT * FROM dim_date;
SELECT * FROM fact_sales;
```

## 🔍 Sample Analytics Queries

### Total Sales

```sql
SELECT SUM(total_amount) AS total_sales
FROM fact_sales;
```

### Sales by Product

```sql
SELECT 
    p.product_name,
    SUM(f.total_amount) AS total_sales
FROM fact_sales f
JOIN dim_product p
    ON f.product_key = p.product_key
GROUP BY p.product_name;
```

### Sales by Customer

```sql
SELECT 
    c.customer_name,
    SUM(f.total_amount) AS total_sales
FROM fact_sales f
JOIN dim_customer c
    ON f.customer_key = c.customer_key
GROUP BY c.customer_name;
```

### Sales by Year

```sql
SELECT 
    d.year_num,
    SUM(f.total_amount) AS total_sales
FROM fact_sales f
JOIN dim_date d
    ON f.date_key = d.date_key
GROUP BY d.year_num
ORDER BY d.year_num;
```

## 📁 Project Structure

```text
sales-data-warehouse/
│
├── README.md
├── database/
│   └── sales_data_warehouse.sql
│
├── data/
│   ├── customers.csv
│   ├── products.csv
│   └── sales.csv
│
└── queries/
    └── sales_analysis.sql
```

## 🎯 Project Objective

The main objective of this project is to build a structured **Sales Data Warehouse** that can efficiently store historical data and support analytical queries for business reporting and decision-making.

## 👨‍💻 Author

**Manchena Sri Sri**

Data Engineering / Data Analytics Enthusiast
