# 🛒 Sales Trend Analysis - Task 6 (Data Analyst Internship)

## 📌 Objective
Analyze monthly **revenue** and **order volume** using SQL aggregation techniques from the `online_sales` dataset.

---

## 🛠 Tools Used
- MySQL Workbench
- SQL (Structured Query Language)

---

## 📂 Dataset
- Table: `online_sales`
- Columns: `order_id`, `order_date`, `product_id`, `amount`

---

## 📊 Analysis Performed
- Extracted **month** and **year** from `order_date`
- Calculated:
  - **Monthly Revenue** using `SUM(amount)`
  - **Order Volume** using `COUNT(DISTINCT order_id)`
- Grouped data by `MONTH` and `YEAR`
- Sorted results by `MONTHLY REVENUE` in descending order
- Limited output to show **Top 3 Highest Sales Months**

---

## 🧠 Key SQL Concepts Used
- `EXTRACT(MONTH FROM order_date)`
- `GROUP BY`, `ORDER BY`
- Aggregate functions: `SUM()`, `COUNT(DISTINCT ...)`
- Handling NULLs with `COALESCE()` (if applicable)

---

## ❓ Interview Questions
1. How do you group data by month and year?  
2. What's the difference between `COUNT(*)` and `COUNT(DISTINCT col)`?  
3. How do you calculate monthly revenue?  
4. What are aggregate functions in SQL?  
5. How to handle NULLs in aggregates?  
6. What’s the role of `ORDER BY` and `GROUP BY`?  
7. How do you get the top 3 months by sales?

---

## 📜 SQL Queries

```sql
-- 1) Create database
CREATE DATABASE sales_analysis;

-- 2) Use database
USE sales_analysis;

-- 3) Create table
CREATE TABLE online_sales (
    order_id INT,
    order_date DATE,
    product_id INT,
    amount DECIMAL(10,2)
);

-- 4) Insert 50 records
-- (Records already inserted in SQL file)

-- 5) View all records
SELECT * FROM online_sales;

-- 6) Total revenue for each month
SELECT MONTH(order_date) AS month, SUM(amount) AS total_revenue
FROM online_sales
GROUP BY MONTH(order_date);

-- 7) Number of distinct orders each month
SELECT MONTH(order_date) AS month, COUNT(DISTINCT order_id) AS total_orders
FROM online_sales
GROUP BY MONTH(order_date);

-- 8) Total revenue for each year
SELECT YEAR(order_date) AS year, SUM(amount) AS total_revenue
FROM online_sales
GROUP BY YEAR(order_date);

-- 9) Total revenue for each product
SELECT product_id, SUM(amount) AS total_revenue
FROM online_sales
GROUP BY product_id;

-- 10) Total orders per product
SELECT product_id, COUNT(order_id) AS total_orders
FROM online_sales
GROUP BY product_id;

-- 11) Month with highest number of orders
SELECT MONTH(order_date) AS month, COUNT(DISTINCT order_id) AS total_orders
FROM online_sales
GROUP BY MONTH(order_date)
ORDER BY total_orders DESC
LIMIT 1;

-- 12) Month with lowest revenue
SELECT MONTH(order_date) AS month, SUM(amount) AS total_revenue
FROM online_sales
GROUP BY MONTH(order_date)
ORDER BY total_revenue ASC
LIMIT 1;

-- 13) Monthly revenue sorted from highest to lowest
SELECT MONTH(order_date) AS month, SUM(amount) AS total_revenue
FROM online_sales
GROUP BY MONTH(order_date)
ORDER BY total_revenue DESC;

-- 14) Monthly order volume (distinct orders)
SELECT MONTH(order_date) AS month, COUNT(DISTINCT order_id) AS order_volume
FROM online_sales
GROUP BY MONTH(order_date);

-- 15) Total revenue per product for January
SELECT product_id, SUM(amount) AS revenue
FROM online_sales
WHERE MONTH(order_date) = 1
GROUP BY product_id;
