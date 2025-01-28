# Etsy Sales

-- Create database
````sql
CREATE DATABASE IF NOT EXISTS Etsysales;

````

– Create Table
````sql
CREATE TABLE Etsysales (
transaction_id SERIAL PRIMARY KEY NOT NULL,
sale_date DATE NOT NULL,
item_name VARCHAR(500) NOT NULL,
product_category VARCHAR(50) NOT NULL,
quantity INT NOT NULL,
price DECIMAL(10,2) NOT NULL,
item_total DECIMAL(10,2) NOT NULL,
ship_state VARCHAR(10),
ship_country VARCHAR(50) NOT NULL,
order_id BIGINT NOT NULL

);

````
-- Data cleaning

-- transaction_id is a BIGINT, so lets change it to BIGINT
````sql
ALTER TABLE etsysales
    ALTER COLUMN transaction_id TYPE BIGINT;
````

-- Add day_name column
````sql
SELECT sale_date, TO_CHAR (sale_date, 'FMDay') AS day_name
FROM etsysales;
````

````sql	
ALTER TABLE etsysales ADD COLUMN day_name VARCHAR(10);
````

````sql
UPDATE etsysales
SET day_name = TO_CHAR(sale_date, 'FMDay');
````

## 📌 Solution

### 1. How many unique shipping country does the data have?
````sql
SELECT COUNT (DISTINCT ship_country)
FROM etsysales;
````
**Answer:**

<img width="103" alt="Screenshot 2025-01-28 at 4 34 21 PM" src="https://github.com/user-attachments/assets/087b44f7-e8af-40f6-94fc-4454b49b044b" />


There are 14 unique shipping country in the dataset.


### 2. How many unique shipping states does the data have?
````sql
SELECT COUNT (DISTINCT ship_state)
FROM etsysales
WHERE ship_state IS NOT NULL;
````
**Answer:**

<img width="105" alt="Screenshot 2025-01-28 at 5 10 15 PM" src="https://github.com/user-attachments/assets/95b6e626-8435-4d3a-ab18-5fa954917b1c" />

There are 42 unique shipping country in the dataset.

### 3. How many unique product category does the data have?
````sql
SELECT COUNT (DISTINCT product_category)
FROM etsysales;
````
**Answer:**

<img width="105" alt="Screenshot 2025-01-28 at 5 11 41 PM" src="https://github.com/user-attachments/assets/c86afe9e-acb3-460b-a423-794c381f2150" />


### 4. What is the best selling product by category
````sql
SELECT SUM(quantity) as qty, product_category
FROM etsysales
GROUP BY product_category
ORDER BY qty desc
````

### 5. What is the total revenue for that month?
````sql
SELECT SUM(item_total) as total_revenue
FROM etsysales
````

### 6. What country has the highest total revenue
````sql
SELECT ship_country, SUM(item_total) 
FROM etsysales
GROUP BY ship_country
ORDER BY SUM(item_total) DESC
LIMIT 1
````

### 7. What product category with the largest revenue?
````sql
SELECT product_category, SUM(item_total)
FROM etsysales
GROUP BY product_category
ORDER BY SUM(item_total) DESC
LIMIT 1
````

### 8. Which country sold more products than average sold?
````sql
SELECT ship_country, AVG(item_total)
FROM etsysales
GROUP BY ship_country
ORDER BY SUM(item_total) DESC
LIMIT 1;
````

















