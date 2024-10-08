# Retail-Sales-Analysis
## Project Overview
Project Title: Retail Sales Analysis
<br>
Level: Beginner
<br>
Database: retail_db

This project is designed to demonstrate SQL skills and techniques typically used to explore, clean, and analyze retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries. This project is ideal for building a solid foundation in SQL.
## Objectives
1.Set up a retail sales database: Create retail sales database and import the data.
<br>
2.Data Cleaning: Identify and remove any records with missing or null values.
<br>
3.Exploratory Data Analysis (EDA): Perform basic exploratory data analysis to understand the dataset.
<br>
4.Business Analysis: Use SQL to answer specific business questions and derive insights from the sales data.

## Project Structre
### 1. Database Setup
**Database Creation:** The project starts by creating a database named retail_db.
<br>
**Table Creation:** A table named retail_sales is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

```sql
CREATE DATABASE retail_db;

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
**Record Count:** Determine the total number of records in the dataset.
<br>
**Customer Count:** Find out how many unique customers are in the dataset.
<br>
**Category Count:** Identify all unique product categories in the dataset.
<br>
**Null Value Check:** Check for any null values in the dataset and delete records with missing data.

```sql
SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;

SELECT * FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

DELETE FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;
```
## 3. Data Analysis & Findings
The following SQL queries were developed to answer specific business questions:
<br>
 **Q.1 Write a SQL query to retrieve all columns for sales made on '2022-11-05.**
```sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
```
**Q.2 Write a query to retrieve all transactions where the category is 'Clothing' and the quantity sold is 4 after of 05-Nov-2022.**
```sql
SELECT 
  *
FROM retail_sales
WHERE 
    category = 'Clothing'
    AND 
    sale_date > '2022-11-05'
    AND
    quantity >=4;
```
    
**Q.3 Write a SQL query to calculate the total sales for each category.**
```sql
SELECT 
    category,
    SUM(total_sale) as net_sale,
    COUNT(*) as total_orders
FROM retail_sales
GROUP BY category;
```
**Q.4 Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.**
```sql
SELECT
    ROUND(AVG(age), 2) as avg_age
FROM retail_sales
WHERE category = 'Beauty';
```
**Q.5 Write a SQL query to find all transactions where the total_sale is greater than 1000.**
```sql
SELECT * FROM retail_sales
WHERE total_sale > 1000;
```
**Q.6 Write a SQL query to find the total number of transactions made by each gender in each category.**
```sql
SELECT 
    category,
    gender,
    COUNT(*) as total_trans
FROM retail_sales
GROUP BY 
    category,
    gender
ORDER BY category;
```
**Q.7 Write a SQL query to calculate the average sale for each month. Find out best selling month in each year.**
```sql
SELECT 
       year,
       month,
    avg_sale
FROM 
(    
SELECT 
    YEAR(sale_date) as year,
    MONTH(sale_date) as month,
    AVG(total_sale) as avg_sale,
    RANK() OVER(PARTITION BY YEAR(sale_date) ORDER BY AVG(total_sale) DESC) as rnk
FROM retail_sales
GROUP BY year,month
) as t1
WHERE rnk = 1;
```
**Q.8 Write a SQL query to find the top 5 customers based on the highest total sales.** 
```sql
SELECT 
    customer_id,
    SUM(total_sale) as total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
```
**Q.9 Write a SQL query to find the number of unique customers who purchased items from each category.**
```sql
SELECT 
    category,    
    COUNT(DISTINCT customer_id) as unique_cust
FROM retail_sales
GROUP BY category;
```
**Q.10 Write a SQL query to create each shift and number of orders ex. Morning <12, Afternoon Between 12 & 17, Evening >17.**
```sql
WITH cte
AS
(
SELECT *,
    CASE
        WHEN HOUR(sale_time) < 12 THEN 'Morning'
        WHEN HOUR(sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END as shift
FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) as total_orders    
FROM cte
GROUP BY shift;
```
## Findings
**Customer Demographics:** The dataset includes customers from various age groups with sales distributed across different categories such as Clothing and Beauty.
<br>
**Sales Trends:** Monthly analysis shows variations in sales, helping identify peak seasons.
<br>
**Customer Insights:** The analysis identifies the top-spending customers and the most popular product categories.
## Conclusion
This project provides introduction to SQL by covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.




