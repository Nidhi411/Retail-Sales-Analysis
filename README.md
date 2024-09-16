# Retail-Sales-Analysis
## Project Overview
Project Title: Retail Sales Analysis
<br>
Level: Beginner
<br>
Database: p1_retail_db

This project is designed to demonstrate SQL skills and techniques typically used to explore, clean, and analyze retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries. This project is ideal for building a solid foundation in SQL.
### Project Structre
## 1. Database Setup
**Database Creation:** The project starts by creating a database named retail_db.
**Table Creation:** A table named retail_sales is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

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
