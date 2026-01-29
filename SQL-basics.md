# SQL Cheat Sheet

## Introduction

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

## SELECT 

| Command | Description |
|--------|-------------|
| `SELECT * FROM Customers;` | Select all records from the Customers table |
| `SELECT CustomerName, City FROM Customers;` | Select specific columns |
| `SELECT DISTINCT Country FROM Customers;` | Return only distinct (different) values |
| `SELECT COUNT(DISTINCT Country) FROM Customers;` | Count distinct values (not supported in MS Access) |
| MS Access workaround: | `SELECT Count(*) AS DistinctCountries FROM (SELECT DISTINCT Country FROM Customers);` |

---

## WHERE 

- The **WHERE** clause is used to **filter records**  
- It extracts only those records that fulfill a specified condition  

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

## SQL Logical Operators (AND, OR, NOT)

| Command | Description |
|---------|------------|
| `SELECT * FROM table_name WHERE condition1 AND condition2;` | Returns rows where **all conditions** are TRUE |
| `SELECT * FROM table_name WHERE condition1 OR condition2;` | Returns rows where **any condition** is TRUE |
| `SELECT * FROM table_name WHERE condition1 AND (condition2 OR condition3);` | Combines AND and OR for complex filtering |
| `SELECT * FROM table_name WHERE NOT condition;` | Reverses the condition, returns rows where the condition is FALSE |
| `SELECT * FROM table_name WHERE column NOT LIKE 'pattern';` | Returns rows where column does **not** match the pattern |
| `SELECT * FROM table_name WHERE column NOT BETWEEN value1 AND value2;` | Returns rows where column is **not** within the specified range |
| `SELECT * FROM table_name WHERE column NOT IN (value1, value2, ...);` | Returns rows where column value is **not** in the specified list |

---

## ORDER BY 

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

---

## INSERT INTO
The INSERT INTO statement is used to insert new records in a table.

### INSERT INTO Syntax

| Command | Description |
|---------|------------|
| `INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);` | Specify both the column names and the values to be inserted |
| `INSERT INTO table_name (column1, column2...) VALUES (value1, value2,...);` | Insert data into specific columns only. The order of values must match the specified columns |
| `INSERT INTO table_name VALUES (value1, value2,...);` | Insert data into all columns without specifying column names. The order of values must match the table column order |
| `INSERT INTO table_name (column1, column2, column3, ...) VALUES (value1a, value2a, value3a, ...), (value1b, value2b, value3b, ...),(value1c, value2c, value3c, ...);` | Insert multiple rows of data in a single statement. Each set of values must be separated by a comma `,` |

---

## NULL Values

A field with a NULL value is a field with no value.  
If a field is optional, it can be left empty when inserting or updating a record.

| Command | Description |
|---------|------------|
| `SELECT column_names FROM table_name WHERE column_name IS NULL;` | Selects records where the column value is NULL |
| `SELECT column_names FROM table_name WHERE column_name IS NOT NULL;` | Selects records where the column value is NOT NULL |

---

## UPDATE

The UPDATE statement is used to **modify existing records** in a table.  
Be careful: omitting the WHERE clause updates **all records** in the table.

| Command | Description |
|---------|------------|
| `UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;` | General syntax to update one or more columns for records matching the condition |
| `UPDATE Customers SET ContactName='Juan' WHERE Country='Mexico';` | Example: update specific records based on a condition |
| `UPDATE Customers SET ContactName='Juan';` | Updates **all records** in the table (no WHERE clause) |

---

## DELETE

The DELETE statement is used to **remove existing records** from a table.  
Be careful: omitting the WHERE clause deletes **all rows**.

| Command | Description |
|---------|------------|
| `DELETE FROM table_name WHERE condition;` | Deletes only the rows that match the condition |
| `DELETE FROM table_name;` | Deletes **all rows** but keeps the table structure and indexes intact |


## DROP TABLE 

Use the DROP TABLE statement to **completely remove a table** from the database.

| Command | Description |
|---------|------------|
| `DROP TABLE table_name;` | Deletes the table and all its data permanently |
| `DROP TABLE Customers;` | Example: completely remove the Customers table |

---
