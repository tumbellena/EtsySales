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





