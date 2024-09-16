# Retail-Sales-Analysis
## Project Overview
Project Title: Retail Sales Analysis
<br>
Level: Beginner
<br>
Database: retail_db

This project is designed to demonstrate SQL skills and techniques typically used to explore, clean, and analyze retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries. This project is ideal for building a solid foundation in SQL.
## Objective
1.Set up a retail sales database: Create retail sales database and import the data.
2.Data Cleaning: Identify and remove any records with missing or null values.
3.Exploratory Data Analysis (EDA): Perform basic exploratory data analysis to understand the dataset.
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
### Data Exploration & Cleaning
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
