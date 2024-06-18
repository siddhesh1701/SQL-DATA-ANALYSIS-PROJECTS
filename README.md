# SQL-DATA-ANALYSIS-PROJECTS
SQL DATA ANALYSIS PROJECTS
# SQL Analysis README File

This README provides a detailed explanation of the SQL queries used for various data manipulations and analyses on tables such as `employees`, `customers`, `orders`, `orderdetails`, `products`, `productlines`, and `payments`. Each query addresses a specific question, with the purpose of demonstrating how to update, insert, delete, and retrieve data effectively.

## Questions and SQL Queries:

### Q-1: Correcting Office Codes in the `employees` Table
**Objective:** Update the `officeCode` for employees who currently have an `officeCode` of 3 to 5.
```sql
UPDATE employees
SET officeCode = 5
WHERE officeCode = 3;
```
**Analysis:** This query ensures that employees are assigned to the correct office by updating the office code from 3 to 5.

### Q-2: Inserting a New Customer into the `customers` Table
**Objective:** Add a new customer with specific details.
```sql
INSERT INTO customers 
VALUES (1122, 'Highway 21', 'Turner', 'Elizabeth', 'Portland', 'OR', '97205', 'USA', '1501', 30000);
```
**Analysis:** This query inserts a new row into the `customers` table with the given customer details.

### Q-3: Deleting an Incorrect Order from the `orders` Table
**Objective:** Remove an order with `orderNumber` 10123.
```sql
DELETE FROM orders 
WHERE orderNumber = 10123;
```
**Analysis:** This query deletes the specified order, ensuring data integrity by removing an incorrect entry.

### Q-4: Converting `quantityOrdered` Data Type in the `orderdetails` Table
**Objective:** Change the data type of `quantityOrdered` from VARCHAR to INTEGER.
```sql
ALTER TABLE orderdetails
MODIFY quantityOrdered INTEGER;
```
**Analysis:** This query corrects the data type to ensure numerical operations can be performed on the `quantityOrdered` column.

### Q-5: Calculating Total Price for Each Order
**Objective:** Calculate and display the total price for each order.
```sql
SELECT orderNumber, SUM(quantityOrdered * priceEach) AS TotalPrice
FROM orderdetails
GROUP BY orderNumber;
```
**Analysis:** This query calculates the total price for each order by multiplying `quantityOrdered` by `priceEach` and summing the results for each `orderNumber`.

### Q-6: Identifying Products with Low Stock
**Objective:** Find products with `quantityInStock` below 50 units.
```sql
SELECT *
FROM products
WHERE quantityInStock < 50;
```
**Analysis:** This query identifies products that have stock levels below the safety threshold, allowing for restocking decisions.

### Q-7: Inserting Multiple Customers into the `customers` Table
**Objective:** Add two new customer entries.
```sql
INSERT INTO customers 
VALUES 
    (495, 'Diecast Collectables', 'Franco', 'Valarie', 'Boston', 'MA', '51003', 'USA', '1188', 85100),
    (496, 'Kelly\'s Gift Shop', 'Snowden', 'Tony', 'Auckland', NULL, NULL, 'New Zealand', '1612', 110000);
```
**Analysis:** This query inserts two new rows into the `customers` table with the provided details.

### Q-8: Updating Job Titles in the `employees` Table
**Objective:** Correct the job title to 'Sales Rep' where `officeCode` is 4.
```sql
UPDATE employees
SET jobTitle = 'Sales Rep'
WHERE officeCode = 4;
```
**Analysis:** This query standardizes the job title for employees in office code 4 to 'Sales Rep'.

### Q-9: Inserting a New Employee into the `employees` Table
**Objective:** Add a new employee with specific details.
```sql
INSERT INTO employees 
VALUES (1102, 'Bondur', 'Gerard', 'x5408', 'gbondur@classicmodelcars.com', 4, '1056', 'Sale Manager(EMEA)');
```
**Analysis:** This query inserts a new row into the `employees` table with the given employee details.

### Q-10: Deleting a Product Line from the `productlines` Table
**Objective:** Remove the 'Boats' entry from the `productlines` table.
```sql
DELETE FROM productlines
WHERE productLine = 'Boats';
```
**Analysis:** This query deletes the 'Boats' product line, reflecting changes in the product offerings.

### Q-11: Retrieving Employees with the Job Title “Sales Rep”
**Objective:** List all employees with the job title 'Sales Rep'.
```sql
SELECT * 
FROM employees
WHERE jobTitle = 'Sales Rep';
```
**Analysis:** This query retrieves all employees with the specified job title, useful for workforce analysis.

### Q-12: Counting Total Number of Employees
**Objective:** Find the total number of employees and alias it as "Total_Employees".
```sql
SELECT COUNT(*) AS Total_Employees
FROM employees;
```
**Analysis:** This query counts the total number of employees, providing a summary metric of workforce size.

### Q-13: Counting Customers in Australia
**Objective:** Determine the number of customers from Australia.
```sql
SELECT COUNT(customerNumber) AS Australia_Customers
FROM customers
WHERE country = 'Australia';
```
**Analysis:** This query counts the number of customers located in Australia, useful for regional analysis.

### Q-14: Checking Stock Quantity for Specific Products
**Objective:** Retrieve the quantity in stock for "Red Start Diecast" products in the "Vintage Cars" line.
```sql
SELECT quantityInStock
FROM products
WHERE productVendor = 'Red Start Diecast'
AND productLine = 'Vintage Cars';
```
**Analysis:** This query finds the stock level for specific products, aiding inventory management.

### Q-15: Counting Unshipped Orders
**Objective:** Count the total number of orders that have not been shipped yet.
```sql
SELECT COUNT(orderNumber) AS Total_orders
FROM orders
WHERE status = 'In Process';
```
**Analysis:** This query identifies orders that are still in process, important for tracking order fulfillment.

### Q-16: Identifying Top Three Countries with Maximum Customers
**Objective:** Find the top three countries with the highest number of customers.
```sql
SELECT country, COUNT(customerNumber) AS max_count
FROM customers
GROUP BY country
ORDER BY max_count DESC
LIMIT 3;
```
**Analysis:** This query ranks countries by the number of customers, highlighting key markets.

### Q-17: Calculating Average Credit Limit for Singapore Customers
**Objective:** Determine the average credit limit for customers in Singapore.
```sql
SELECT AVG(creditLimit) AS Average_limit 
FROM customers
WHERE country = 'Singapore';
```
**Analysis:** This query calculates the average credit limit for Singaporean customers, useful for financial analysis.

### Q-18: Calculating Total Payments for a Specific Customer
**Objective:** Find the total amount paid by the customer named “Euro+ Shopping Channel”.
```sql
SELECT SUM(amount) AS TotalAmountToBePaid
FROM payments
WHERE customerNumber = (
    SELECT customerNumber
    FROM customers
    WHERE customerName = 'Euro+ Shopping Channel'
);
```
**Analysis:** This query calculates the total payments made by a specific customer, providing financial insights.

### Q-19: Identifying the Month with Maximum Payments
**Objective:** Determine which month received the maximum aggregated payments.
```sql
SELECT MONTH(paymentDate), SUM(amount) AS payment 
FROM payments
GROUP BY MONTH(paymentDate)
ORDER BY payment DESC
LIMIT 1;
```
**Analysis:** This query finds the month with the highest total payments, useful for financial planning and analysis.

### Q-20: Aggregated Value of Payments in the Top Month
**Objective:** Calculate the total payment amount received in the month with maximum payments.
**Answer:** 1,645,923.26

This README serves as a comprehensive guide for understanding and performing various data operations and analyses using SQL queries. Each query is designed to address specific business questions, providing insights and maintaining data integrity across different tables.
