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
| `SELECT COUNT(DISTINCT Country) FROM Customers;` | Count distinct values |

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

- The **ORDER BY** keyword sorts records in **ascending order by default** 
- Use **DESC** to sort in descending order  

| Command | Description |
|---------|------------|
| `SELECT * FROM Products ORDER BY Price;` | Sort products from lowest to highest price |
| `SELECT * FROM Products ORDER BY Price DESC;` | Sort products from highest to lowest price |
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
| `INSERT INTO table_name (column1, column2...) VALUES (value1, value2,...);` | Insert data into specific columns only. The order of values must match the specified columns |
| `INSERT INTO table_name VALUES (value1, value2,...);` | Insert data into all columns without specifying column names. The order of values must match the table column order |
| `INSERT INTO table_name (column1, column2, column3, ...) VALUES (value1a, value2a, value3a, ...), (value1b, value2b, value3b, ...),(value1c, value2c, value3c, ...);` | Insert multiple rows of data in a single statement. Each set of values must be separated by a comma `,` **Not valid in Oracle SQL** |
 
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
| `UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;` | Update one or more columns for records matching the condition |
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

---

## SELECT TOP / LIMIT / FETCH

The **SELECT TOP** clause (or `LIMIT` / `FETCH`) is used to specify the number of records to return.  
It is useful on large tables, as returning too many records can impact performance.  

**Note:** Not all databases support `SELECT TOP`.  
- **MySQL** uses `LIMIT`.  
- **Oracle** uses `FETCH FIRST n ROWS ONLY` or `ROWNUM`.

| Database | Command | Description |
|----------|---------|------------|
| SQL Server / MS Access | `SELECT TOP number column_name(s) FROM table_name WHERE condition;` | Returns the top `number` of rows from a table |
| SQL Server / MS Access | `SELECT TOP percent column_name(s) FROM table_name WHERE condition;` | Returns the top `percent` of rows from a table |
| MySQL | `SELECT column_name(s) FROM table_name WHERE condition LIMIT number;` | Returns the first `number` of rows from a table |
| Oracle 12+ | `SELECT column_name(s) FROM table_name ORDER BY column_name(s) FETCH FIRST number ROWS ONLY;` | Returns the first `number` of rows after ordering |
| Oracle (older) | `SELECT column_name(s) FROM table_name WHERE ROWNUM <= number;` | Returns the first `number` of rows using ROWNUM |


## SQL Aggregate Functions

Aggregate functions perform a calculation on a set of values and return a **single value**.  
They are often used with the `GROUP BY` clause to return values per group.  

| Function | Description | Example |
|----------|------------|---------|
| `MIN(column)` | Returns the smallest value in a column | `SELECT MIN(Price) AS SmallestPrice FROM Products;` |
| `MAX(column)` | Returns the largest value in a column | `SELECT MAX(Price) AS LargestPrice FROM Products;` |
| `COUNT(column)` | Returns the number of non-NULL values in a column | `SELECT COUNT(CustomerID) FROM Customers;` |
| `COUNT(*)` | Returns the total number of rows (including NULLs) | `SELECT COUNT(*) FROM Customers;` |
| `SUM(column)` | Returns the sum of all values in a numeric column | `SELECT SUM(Salary) FROM Employees;` |
| `AVG(column)` | Returns the average value of a numeric column | `SELECT AVG(Salary) FROM Employees;` |

**Notes:**  
- Aggregate functions ignore `NULL` values except for `COUNT(*)`.  
- Use the `AS` keyword to give a descriptive name to the result column.  

## SQL LIKE Operator & Wildcards

The `LIKE` operator is used in a `WHERE` clause to search for a **pattern in a column**.  
Wildcards allow flexible matching:

| Wildcard | Description | Example |
|----------|------------|---------|
| `%` | Matches zero, one, or multiple characters | `SELECT * FROM Customers WHERE CustomerName LIKE 'La%';` (starts with 'La') |
| `_` | Matches exactly one character | `SELECT * FROM Customers WHERE City LIKE '_ondon';` (London, Bondon, etc.) |
| `[]` | Matches any single character inside brackets | `SELECT * FROM Customers WHERE CustomerName LIKE '[bsp]%';` (starts with b, s, or p) |
| `-` | Specifies a range of characters inside `[]` | `SELECT * FROM Customers WHERE CustomerName LIKE '[a-f]%';` (starts with a–f) |
| `{}` | Escapes special characters (Oracle / SQL Server) | - |
| `^` | Negates characters inside `[]` (not in the set) | `SELECT * FROM Customers WHERE CustomerName LIKE '[^a-c]%';` |

**Common pattern examples:**

| Pattern | Description | SQL Example |
|---------|------------|------------|
| `'La%'` | Starts with 'La' | `SELECT * FROM Customers WHERE CustomerName LIKE 'La%';` |
| `'%a'` | Ends with 'a' | `SELECT * FROM Customers WHERE CustomerName LIKE '%a';` |
| `'%or%'` | Contains 'or' | `SELECT * FROM Customers WHERE CustomerName LIKE '%or%';` |
| `'a__%'` | Starts with 'a' and at least 3 characters | `SELECT * FROM Customers WHERE CustomerName LIKE 'a__%';` |
| `'_r%'` | 'r' in the second position | `SELECT * FROM Customers WHERE CustomerName LIKE '_r%';` |
| `'Spain'` | Exact match | `SELECT * FROM Customers WHERE Country LIKE 'Spain';` |

**Microsoft Access Wildcards:**

| Symbol | Description | Example |
|--------|------------|---------|
| `*` | Zero or more characters | `bl*` finds 'bl', 'black', 'blue', 'blob' |
| `?` | Single character | `h?t` finds 'hot', 'hat', 'hit' |
| `[]` | Any single character in brackets | `h[oa]t` finds 'hot' and 'hat', not 'hit' |
| `!` | Not in brackets | `h[!oa]t` finds 'hit', not 'hot' or 'hat' |
| `-` | Range of characters in brackets | `c[a-b]t` finds 'cat', 'cbt' |
| `#` | Single numeric character | `2#5` finds 205, 215, 225, etc. |

## SQL IN / NOT IN Operator

The **IN** operator allows you to specify multiple values in a `WHERE` clause.  
It is a shorthand for multiple `OR` conditions.

| Command | Description | Example |
|---------|------------|---------|
| `column_name IN (value1, value2, ...)` | Returns rows where the column matches any value in the list | `SELECT * FROM Customers WHERE Country IN ('Germany', 'France', 'UK');` |
| `column_name NOT IN (value1, value2, ...)` | Returns rows where the column does **not** match any value in the list | `SELECT * FROM Customers WHERE Country NOT IN ('Germany', 'France', 'UK');` |
| `column_name IN (SELECT column_name FROM table_name)` | Subquery: returns rows matching values from another table | `SELECT * FROM Orders WHERE CustomerID IN (SELECT CustomerID FROM Customers WHERE Country='Germany');` |
| `column_name NOT IN (SELECT column_name FROM table_name)` | Subquery: returns rows not matching values from another table | `SELECT * FROM Orders WHERE CustomerID NOT IN (SELECT CustomerID FROM Customers WHERE Country='Germany');` |

---

## SQL BETWEEN / NOT BETWEEN Operator

The **BETWEEN** operator selects values within a given range (numbers, text, or dates).  
It is **inclusive**: both the start and end values are included.

| Command | Description | Example |
|---------|------------|---------|
| `column_name BETWEEN value1 AND value2` | Returns rows where the column is within the range | `SELECT * FROM Products WHERE Price BETWEEN 10 AND 20;` |
| `column_name NOT BETWEEN value1 AND value2` | Returns rows where the column is outside the range | `SELECT * FROM Products WHERE Price NOT BETWEEN 10 AND 20;` |
| `column_name BETWEEN value1 AND value2 AND column_name IN (value_list)` | Combine BETWEEN with IN | `SELECT * FROM Products WHERE Price BETWEEN 10 AND 20 AND CategoryID IN (1,2,3);` |
| `column_name BETWEEN 'Text1' AND 'Text2'` | Works with text values (alphabetical range) | `SELECT * FROM Products WHERE ProductName BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni';` |
| `column_name NOT BETWEEN 'Text1' AND 'Text2'` | Excludes text values in the range | `SELECT * FROM Products WHERE ProductName NOT BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni';` |
| `column_name BETWEEN 'StartDate' AND 'EndDate'` | Works with dates | `SELECT * FROM Orders WHERE OrderDate BETWEEN '1996-07-01' AND '1996-07-31';` |

**Notes:**  
- `BETWEEN` is inclusive, meaning both boundary values are included.  
- You can combine `BETWEEN` with other operators (`IN`, `AND`, `OR`) for complex filtering.  



# FIND TABLE'S PRIMARY KEY OR COMPOSITE KEY (KEY1,KEY2)
SELECT cols.column_name
FROM user_constraints cons
JOIN user_cons_columns cols
  ON cons.constraint_name = cols.constraint_name
WHERE cons.constraint_type = 'P'
  AND cons.table_name = 'TABLE_NAME';


# FIND TABLE'S FOREIGN KEY(S)
SELECT
  a.column_name,
  c_pk.table_name AS referenced_table,
  b.column_name AS referenced_column
FROM user_constraints c
JOIN user_cons_columns a
  ON c.constraint_name = a.constraint_name
JOIN user_constraints c_pk
  ON c.r_constraint_name = c_pk.constraint_name
JOIN user_cons_columns b
  ON c_pk.constraint_name = b.constraint_name
WHERE c.constraint_type = 'R'
  AND c.table_name = 'TABLE_NAME';
