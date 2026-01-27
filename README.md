# SQL Cheat Sheet

## Introduction

**What is SQL?**  
- SQL stands for **Structured Query Language**  
- SQL lets you access and manipulate databases  
- SQL became a standard of ANSI in 1986 and ISO in 1987  

**What Can SQL Do?**  
- Execute queries against a database  
- Retrieve data from a database  
- Insert records in a database  
- Update records in a database  
- Delete records from a database  
- Create new databases  
- Create new tables in a database  
- Create stored procedures in a database  
- Create views in a database  
- Set permissions on tables, procedures, and views  

**RDBMS**  
- RDBMS stands for **Relational Database Management System**  
- RDBMS is the basis for SQL  

---

## Database Tables

- A database contains **one or more tables**  
- Each table has a **name** (e.g., "Customers", "Orders")  
- Tables contain **records (rows)** with data  

**Keep in Mind**  
- SQL keywords are **NOT case sensitive**: `select` is the same as `SELECT`  

---

## Basic SQL Commands

| Command | Description |
|--------|-------------|
| SELECT | Extracts data from a database |
| UPDATE | Updates data in a database |
| DELETE | Deletes data from a database |
| INSERT INTO | Inserts new data into a database |
| CREATE DATABASE | Creates a new database |
| ALTER DATABASE | Modifies a database |
| CREATE TABLE | Creates a new table |
| ALTER TABLE | Modifies a table |
| DROP TABLE | Deletes a table |
| CREATE INDEX | Creates an index (search key) |
| DROP INDEX | Deletes an index |

---

## Semicolon in SQL

- Some database systems require a semicolon `;` at the end of each SQL statement  
- Semicolon is the standard way to separate multiple SQL statements in one call to the server  

---

## SELECT Statement

| Command | Description |
|--------|-------------|
| `SELECT * FROM Customers;` | Select all records from the Customers table |
| `SELECT CustomerName, City FROM Customers;` | Select specific columns |
| `SELECT DISTINCT Country FROM Customers;` | Return only distinct (different) values |
| `SELECT COUNT(DISTINCT Country) FROM Customers;` | Count distinct values (not supported in MS Access) |
| MS Access workaround: | `SELECT Count(*) AS DistinctCountries FROM (SELECT DISTINCT Country FROM Customers);` |

## WHERE Clause

- The **WHERE** clause is used to **filter records**  
- It extracts only those records that fulfill a specified condition  

## WHERE Clause Examples

| Command | Description |
|---------|------------|
| `SELECT * FROM Customers WHERE Country='Mexico';` | Select all customers from Mexico |
| `SELECT * FROM Customers WHERE CustomerID=1;` | Select all customers with CustomerID = 1 |
| `SELECT * FROM Customers WHERE CustomerID > 80;` | Select all customers with CustomerID > 80 |

## SQL Operators

| Command | Description |
|---------|------------|
| `=`        | Equal |
| `>`        | Greater than |
| `<`        | Less than |
| `>=`       | Greater than or equal |
| `<=`       | Less than or equal |
| `<>`       | Not equal (some SQL versions allow `!=`) |
| `BETWEEN`  | Between a certain range |
| `LIKE`     | Search for a pattern |
| `IN`       | Specify multiple possible values |

## ORDER BY Examples

- The **ORDER BY** keyword sorts records in ascending order by default  
- Use **DESC** to sort in descending order  

| Command | Description |
|---------|------------|
| `SELECT * FROM Products ORDER BY Price DESC;` | Sort products from highest to lowest price |
| `SELECT * FROM Products ORDER BY Price;` | Sort products by price ascending |
| `SELECT * FROM Products ORDER BY ProductName;` | Sort products alphabetically by ProductName |
| `SELECT * FROM Products ORDER BY ProductName DESC;` | Sort products reverse alphabetically by ProductName |
| `SELECT * FROM Customers ORDER BY Country, CustomerName;` | Sort customers by Country and CustomerName |
| `SELECT * FROM Customers ORDER BY Country ASC, CustomerName DESC;` | Sort ascending by Country and descending by CustomerName |

## AND, OR, NOT Operators

| Command | Description |
|---------|------------|
| `SELECT * FROM Customers WHERE Country = 'Spain' AND CustomerName LIKE 'G%';` | The AND operator displays a record if all conditions are TRUE |
| `SELECT * FROM Customers WHERE Country = 'Spain' AND (CustomerName LIKE 'G%' OR CustomerName LIKE 'R%');` | Combines AND and OR to filter records based on multiple conditions |
| `SELECT column1, column2, ... FROM table_name WHERE condition1 OR condition2 OR condition3 ...;` | The OR operator displays a record if any of the conditions are TRUE |
| `SELECT * FROM Customers WHERE CustomerName NOT LIKE 'A%';` | The NOT operator gives the opposite result of LIKE |
| `SELECT * FROM Customers WHERE CustomerID NOT BETWEEN 10 AND 60;` | The NOT operator reverses BETWEEN condition |
| `SELECT * FROM Customers WHERE City NOT IN ('Paris', 'London');` | The NOT operator reverses IN condition |
| `SELECT * FROM Customers WHERE NOT CustomerID > 50;` | The NOT operator reverses greater than condition |
| `SELECT * FROM Customers WHERE NOT CustomerID < 50;` | The NOT operator reverses less than condition |

## INSERT INTO

### INSERT INTO Syntax

It is possible to write the INSERT INTO statement in two ways:

| Command | Description |
|---------|------------|
| `INSERT INTO table_name (column1, column2, column3, ...) VALUES (value1, value2, value3, ...);` | Specify both the column names and the values to be inserted |
| `INSERT INTO table_name VALUES (value1, value2, value3, ...);` | Insert values for all columns without specifying column names (order must match table columns) |
| `INSERT INTO table_name (column1, column2, column3, ...) VALUES (value1, value2, value3, ...);` | Insert data into specific columns only. The order of values must match the specified columns |
| `INSERT INTO table_name VALUES (value1, value2, value3, ...);` | Insert data into all columns without specifying column names. The order of values must match the table column order |
| ```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES
(value1a, value2a, value3a, ...),
(value1b, value2b, value3b, ...),
(value1c, value2c, value3c, ...);
``` | Insert multiple rows of data in a single statement. Each set of values must be separated by a comma `,` |

