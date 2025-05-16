# Retail Sales Analysis SQL Project

## Synopsis

This SQL project is a hands-on analysis of retail sales data designed to demonstrate data wrangling, querying, and business insight generation using SQL. It involves setting up a database, cleaning data, performing exploratory data analysis (EDA), and addressing specific business queries.

## Project Overview

**Project Title**: Retail Sales Analysis  
**Database**: SQL_Project1

This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries. 

## Objectives

1. **Set up a retail sales database**: Create and populate a retail sales database with the provided sales data.
2. **Data Cleaning**: Identify and remove any records with missing or null values.
3. **Exploratory Data Analysis (EDA)**: Perform basic exploratory data analysis to understand the dataset.
4. **Business Analysis**: Use SQL to answer specific business questions and derive insights from the sales data.

## Project Structure

### 1. Database Setup

- **Database Creation**: The project starts by creating a database named `SQL_Project1`.
- **Table Creation**: A table named `retail_sales` is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

```sql
CREATE DATABASE SQL_Project1;

CREATE TABLE retail_sales
(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,	
    sale_time TIME,
    customer_id INT,	
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,	
    cogs FLOAT,
    total_sale FLOAT
);
```

### 2. Data Exploration & Cleaning

- **Record Count**: Determine the total number of records in the dataset.
- **Customer Count**: Find out how many unique customers are in the dataset.
- **Category Count**: Identify all unique product categories in the dataset.
- **Null Value Check**: Check for any null values in the dataset and delete records with missing data.

```sql
SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;

SELECT * FROM public.retail_sales
WHERE	 transactions_id IS NULL
 		 OR
		 sale_date IS NULL
		 OR
		 gender IS NULL
		 OR
		 category IS NULL
		 OR
		 quantity IS NULL
		 OR
		 cogs IS NULL
		 OR
		 total_sale IS NULL;
		 
DELETE FROM public.retail_sales
WHERE	 transactions_id IS NULL
 		 OR
		 sale_date IS NULL
		 OR
		 gender IS NULL
		 OR
		 category IS NULL
		 OR
		 quantity IS NULL
		 OR
		 cogs IS NULL
		 OR
		 total_sale IS NULL;
```

### 3. Data Analysis & SQL Queries

SQL queries to answer business questions:

```sql
-- 1. **Write a SQL query to retrieve all columns for sales made on '2022-11-05**:
```sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';

-- 2. **Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022**:
```sql
SELECT *
FROM public.retail_sales
WHERE category = 'Clothing'
AND quantity >= 4
AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11';

-- 3. **Write a SQL query to calculate the total sales (total_sale) for each category.**:
```sql
SELECT category, SUM(total_sale)
FROM public.retail_sales
GROUP BY category;

-- 4. **Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.**:
```sql
SELECT AVG(age)
FROM public.retail_sales
WHERE category = 'Beauty';

-- 5. **Write a SQL query to find all transactions where the total_sale is greater than 1000.**:
```sql
SELECT *
FROM public.retail_sales
WHERE total_sale > 1000;

-- 6. **Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.**:
SELECT category, gender, count(*)
FROM public.retail_sales
GROUP BY gender, category;

-- 7. **Write a SQL query to calculate the average sale for each month**:
SELECT
EXTRACT(YEAR FROM sale_date) as year, EXTRACT(MONTH FROM sale_date) as month, AVG(total_sale) as avg_sales
FROM public.retail_sales
GROUP BY year, month
ORDER BY year, month ASC;

-- 8. **Top 5 customers by total sales**:
SELECT customer_id, SUM(total_sale) FROM public.retail_sales
GROUP BY customer_id ORDER BY SUM(total_sale) DESC LIMIT 5;

-- 9. Unique customers per category
SELECT category, COUNT(DISTINCT customer_id) as cnt_unique_cs
FROM retail_sales GROUP BY category;

-- 10. **Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17)**:
WITH hourly_sale AS (
SELECT *, CASE
WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
ELSE 'Evening' END as shift FROM retail_sales)
SELECT shift, COUNT(*) as total_orders FROM hourly_sale GROUP BY shift;
```

## Findings

- **Customer Demographics**: Sales span diverse age groups and genders.
- **High-Value Transactions**: Multiple sales over ₹1000 indicate premium buying behavior.
- **Sales Trends**: Seasonality and monthly trends observed.
- **Customer Insights**: Top 5 customers and product category preferences discovered.

## Reports Generated

- **Sales Summary**: Sales totals by category, value, and volume.
- **Trend Analysis**: Sales patterns by month and time of day.
- **Customer Insights**: Engagements by age, gender, and category.

## How Was This Project Useful?

This project reinforced critical SQL skills like data cleaning, grouping, aggregating, and condition-based querying. It simulated real-world data analysis scenarios where businesses use SQL to extract value from raw transactional data. It is particularly useful for preparing for data analyst and business analyst roles.

## Upstream and Downstream of the Project

- **Upstream (Input Sources & Data)**:
  - Raw retail transaction data (CSV or database dump).
  - Database setup and schema design.
  - Data insertion/ingestion into PostgreSQL or similar RDBMS.

- **Downstream (Usage & Business Value)**:
  - Used by business analysts to understand sales trends and customer behaviors.
  - Insights fed into marketing and inventory decision-making processes.

## Conclusion

This project serves as a comprehensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.

## Author

**Aditya Sharma**  
This project is part of my portfolio, showcasing the SQL skills essential for business analyst roles.  
Feel free to connect for feedback, queries, or collaboration!

---

**Thank you!**
