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

### 1. How many unique shipping countries are there in the etsy sales data?
````sql
SELECT COUNT (DISTINCT ship_country)
FROM etsysales;
````
**Answer:**

<img width="103" alt="Screenshot 2025-01-28 at 4 34 21 PM" src="https://github.com/user-attachments/assets/087b44f7-e8af-40f6-94fc-4454b49b044b" />


There are 14 unique countries where shipments have been made according to the sales data.


### 2. How many unique shipping states have been recorded in the sales data, excluding any null values?
````sql
SELECT COUNT (DISTINCT ship_state)
FROM etsysales
WHERE ship_state IS NOT NULL;
````
**Answer:**

<img width="105" alt="Screenshot 2025-01-28 at 5 10 15 PM" src="https://github.com/user-attachments/assets/95b6e626-8435-4d3a-ab18-5fa954917b1c" />

There are 42 unique shipping states recorded in the sales data, excluding any null values

### 3. How many distinct product categories are there in the sales data?
````sql
SELECT COUNT (DISTINCT product_category)
FROM etsysales;
````
**Answer:**

<img width="105" alt="Screenshot 2025-01-28 at 5 11 41 PM" src="https://github.com/user-attachments/assets/c86afe9e-acb3-460b-a423-794c381f2150" />

There are 12 unique product categories in the sales data.

### 4. What is the total quantity sold for each product category, and which category has the highest sales?"
````sql
SELECT SUM(quantity) as qty, product_category AS Best_Selling_Product_Category
FROM etsysales
GROUP BY product_category
ORDER BY qty desc
````
**Answer:**

<img width="258" alt="Screenshot 2025-01-28 at 5 24 59 PM" src="https://github.com/user-attachments/assets/a9be8b49-8e7c-4b2b-9e13-e85c23d760d8" />

The total quantity sold for each product category is as follows, with the category LIGHTS having the highest sales of 237.

### 5. What is the total revenue generated from all sales for this month?
````sql
SELECT SUM(item_total) as total_revenue
FROM etsysales
````
**Answer:**

<img width="145" alt="Screenshot 2025-01-28 at 6 02 25 PM" src="https://github.com/user-attachments/assets/74b39b0e-4d25-4635-a18f-bd9c5c57efc5" />

The total revenue generated from all sales is 9329.80

### 6. Which country generated the highest total revenue from sales, and how much was it?
````sql
SELECT ship_country, SUM(item_total) AS total_revenue
FROM etsysales
GROUP BY ship_country
ORDER BY SUM(item_total) DESC
LIMIT 1
````
**Answer:**

<img width="252" alt="Screenshot 2025-01-28 at 6 06 58 PM" src="https://github.com/user-attachments/assets/19dcc4f3-a5ad-4c80-af67-81e690472119" />

The country that generated the highest total revenue from sales is United States, with a total of 7231.63

### 7. Which product category generated the highest total revenue, and how much was it?
````sql
SELECT product_category, SUM(item_total) AS total_revenue
FROM etsysales
GROUP BY product_category
ORDER BY SUM(item_total) DESC
LIMIT 1
````

**Answer:**

<img width="256" alt="Screenshot 2025-01-28 at 6 10 42 PM" src="https://github.com/user-attachments/assets/77c12cfe-027e-40d3-9e3f-1d45968a64dd" />

The product category that generated the highest total revenue is Lights with a total of 7910.40

### 8. Which country has the highest average order value, and what is the average amount??
````sql
SELECT ship_country, AVG(item_total) AS average_amount
FROM etsysales
GROUP BY ship_country
ORDER BY SUM(item_total) DESC
LIMIT 1;
````
**Answer:**

<img width="296" alt="Screenshot 2025-01-28 at 6 15 32 PM" src="https://github.com/user-attachments/assets/903de8d3-ec29-4383-82cb-9eb7bebc0f9e" />


The country with the highest average order value is United States, with an average of 32.87

















