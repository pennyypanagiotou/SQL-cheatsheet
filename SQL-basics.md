# SQL Cheat Sheet

## Introduction

## SQL Comments

### Single Line Comments
Single-line comments start with `--`.  
Any text between `--` and the end of the line is ignored and not executed.

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
| `SELECT * FROM Customers ORDER BY Country, CustomerName;` | Sorts the customers first alphabetically by Country, and within each country, sorts alphabetically by CustomerName. |
| `SELECT * FROM Customers ORDER BY Country ASC, CustomerName DESC;` | Sorts the customers alphabetically by Country , and within each country, sorts CustomerName in reverse alpabetically order |

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
| `column_name BETWEEN 'Text1' AND 'Text2'` | Works with text values (alphabetical range) | `SELECT * FROM Products WHERE ProductName BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni';` |
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

;

---

## SQL CREATE DATABASE

| Command | Description |
|--------|------------|
| `CREATE DATABASE databasename;` | Creates a new SQL database |

---

## SQL DROP DATABASE

| Command | Description |
|--------|------------|
| `DROP DATABASE databasename;` | Drops an existing SQL database |

---

## SQL BACKUP DATABASE (SQL Server)

| Command | Description |
|--------|------------|
| `BACKUP DATABASE databasename TO DISK = 'filepath';` | Creates a full backup of an existing database |

---

## SQL CREATE TABLE

| Command | Description |
|--------|------------|
| `CREATE TABLE table_name (column1 datatype, column2 datatype, ...);` | Creates a new table with specified columns and data types |
| `CREATE TABLE new_table AS SELECT column1, column2 FROM existing_table WHERE ...;` | Creates a new table from an existing table with optional filtering |

---

## SQL DROP TABLE

| Command | Description |
|--------|------------|
| `DROP TABLE table_name;` | Deletes an existing table from the database |

---

## SQL ALTER TABLE

| Command | Description |
|--------|------------|
| `ALTER TABLE table_name ADD column_name datatype;` | Adds a new column to an existing table |
| `ALTER TABLE table_name DROP COLUMN column_name;` | Deletes a column from a table (some DBs may not allow this) |
| `ALTER TABLE table_name RENAME COLUMN old_name TO new_name;` | Renames a column (SQL standard) |
| `EXEC sp_rename 'table_name.old_name', 'new_name', 'COLUMN';` | Renames a column in SQL Server |
| `ALTER TABLE table_name ALTER COLUMN column_name datatype;` | Changes the data type of a column (SQL Server / MS Access) |
| `ALTER TABLE table_name MODIFY COLUMN column_name datatype;` | Changes the data type of a column (MySQL / Oracle) |

---

## SQL Constraints

| Constraint | Description |
|------------|------------|
| `NOT NULL` | Column cannot have NULL values |
| `UNIQUE` | All values in the column must be unique |
| `PRIMARY KEY` | Combines NOT NULL and UNIQUE; uniquely identifies each row |
| `FOREIGN KEY` | Ensures referential integrity between tables |
| `CHECK` | Ensures column values satisfy a condition |
| `DEFAULT` | Sets a default value for a column |
| `CREATE INDEX` |  |

---

## SQL Working with Dates

### MySQL Date Data Types

| Data Type | Format | Description |
|-----------|--------|------------|
| `DATE` | YYYY-MM-DD | Stores date only |
| `DATETIME` | YYYY-MM-DD HH:MI:SS | Stores date and time |
| `TIMESTAMP` | YYYY-MM-DD HH:MI:SS | Stores timestamp value |
| `YEAR` | YYYY or YY | Stores year only |

### SQL Server Date Data Types

| Data Type | Format | Description |
|-----------|--------|------------|
| `DATE` | YYYY-MM-DD | Stores date only |
| `DATETIME` | YYYY-MM-DD HH:MI:SS | Stores date and time |
| `SMALLDATETIME` | YYYY-MM-DD HH:MI:SS | Stores date and time with less precision |
| `TIMESTAMP` | Unique number | Stores a unique timestamp value |


# SQL Cheat Sheet pt.2

## SQL GROUP BY Statement

The `GROUP BY` statement groups rows with the same values.  
Often used with aggregate functions: COUNT(), SUM(), AVG(), MIN(), MAX().

| Command | Description |
|--------|------------|
| `SELECT column_name(s) FROM table_name GROUP BY column_name(s);` | Groups rows by column(s) |
| `SELECT column_name(s) FROM table_name GROUP BY column_name(s) ORDER BY column_name(s);` | Groups rows and orders the result |
| `SELECT Country, COUNT(*) FROM Customers GROUP BY Country;` | Example: count customers per country |

---

## SQL HAVING Clause

Filters **grouped results** (cannot use WHERE with aggregates).

| Command | Description |
|--------|------------|
| `SELECT column_name(s) FROM table_name GROUP BY column_name(s) HAVING condition;` | Filters groups after aggregation |
| `SELECT Country, COUNT(*) FROM Customers GROUP BY Country HAVING COUNT(*) > 5;` | Example: only countries with more than 5 customers |

---

## SQL EXISTS Operator

Checks if a subquery returns one or more rows.

| Command | Description |
|--------|------------|
| `SELECT column_name(s) FROM table_name WHERE EXISTS (subquery);` | Returns rows if subquery has any record |
| `SELECT * FROM Customers WHERE EXISTS (SELECT * FROM Orders WHERE Orders.CustomerID = Customers.CustomerID);` | Example: only customers with orders |

---

## SQL ANY / ALL Operators

Compare a value to a set of values from a subquery.

| Command | Description |
|--------|------------|
| `column_name operator ANY (subquery)` | TRUE if **any** value in subquery meets condition |
| `column_name operator ALL (subquery)` | TRUE if **all** values in subquery meet condition |
| `SELECT * FROM Products WHERE Price > ANY (SELECT Price FROM Products WHERE CategoryID=1);` | Example using ANY |
| `SELECT * FROM Products WHERE Price > ALL (SELECT Price FROM Products WHERE CategoryID=1);` | Example using ALL |

---

## SQL SELECT INTO Statement

Copies data from one table into a **new table**.

| Command | Description |
|--------|------------|
| `SELECT * INTO new_table FROM old_table;` | Copies all columns into new table |
| `SELECT column1, column2 INTO new_table FROM old_table;` | Copies specific columns into new table |

---

## SQL INSERT INTO SELECT Statement

Copies data from one table into an **existing table**.

| Command | Description |
|--------|------------|
| `INSERT INTO table2 SELECT * FROM table1;` | Copy all columns from one table to another |
| `INSERT INTO table2 (col1, col2) SELECT col1, col2 FROM table1;` | Copy specific columns |

---

## SQL CASE Expression

Used like **if–then–else**, returns value based on conditions.

| Command | Description |
|--------|------------|
| `CASE WHEN condition THEN result ELSE result END` | General CASE syntax |
| `SELECT CustomerName, CASE WHEN Country='Germany' THEN 'DE' ELSE 'Other' END AS CountryCode FROM Customers;` | Example using CASE |

---

## Stored Procedures

Reusable SQL code that can accept parameters.

| Command | Description |
|--------|------------|
| `CREATE PROCEDURE procedure_name AS sql_statement;` | Creates a stored procedure |
| `EXEC procedure_name;` | Executes the stored procedure |

---

## SQL Arithmetic Operators

| Command | Description |
|--------|------------|
| `+` | Addition |
| `-` | Subtraction |
| `*` | Multiplication |
| `/` | Division |
| `%` | Modulo |




## SQL Aliases

SQL aliases are used to give a **temporary name** to a table or a column.  
Aliases exist **only for the duration of the query** and are used to make results more readable.  
The `AS` keyword is optional.

--

### Alias Syntax

| Command | Description |
|--------|------------|
| `SELECT column_name AS alias_name FROM table_name;` | Alias for a column |
| `SELECT column_name alias_name FROM table_name;` | Column alias without using AS |
| `SELECT column_name FROM table_name AS alias_name;` | Alias for a table |
| `SELECT column_name FROM table_name alias_name;` | Table alias without AS |
| `SELECT column_name AS "My Great Column" FROM table_name;` | Column alias with spaces |
| `SELECT CustomerName, Address + ', ' + PostalCode + ' ' + City + ', ' + Country AS Address FROM Customers;` | Alias combining multiple columns for SQL |

---


## SQL JOIN

A JOIN clause is used to **combine rows from two or more tables** based on a related column.

--

### Types of JOINs

| JOIN Type | Description |
|----------|------------|
| INNER JOIN | Returns records that have matching values in both tables |
| LEFT JOIN | Returns all records from the left table and matched records from the right table |
| RIGHT JOIN | Returns all records from the right table and matched records from the left table |
| FULL JOIN | Returns all records when there is a match in either table |

--

## JOIN Syntax

| Command | Description |
|--------|------------|
| `SELECT column_name(s) FROM table1 INNER JOIN table2 ON table1.column_name = table2.column_name;` | INNER JOIN syntax |
| `SELECT column_name(s) FROM table1 LEFT JOIN table2 ON table1.column_name = table2.column_name;` | LEFT JOIN OR LEFT OUTTER JOIN|
| `SELECT column_name(s) FROM table1 RIGHT JOIN table2 ON table1.column_name = table2.column_name;` | RIGHT JOIN OR RIGHT OUTER JOIN |
| `SELECT column_name(s) FROM table1 FULL OUTER JOIN table2 ON table1.column_name = table2.column_name WHERE condition;` | FULL OUTER JOIN OR FULL JOIN |

---

## SQL SELF JOIN

A **SELF JOIN** is a join where a table is joined with itself using aliases.

| Command | Description |
|--------|------------|
| `SELECT column_name(s) FROM table_name T1, table_name T2 WHERE condition;` | Self join using aliases for the same table |

> `T1` and `T2` are different aliases for the same table.

---

## SQL UNION Operator

The **UNION** operator combines the result-set of two or more `SELECT` statements  
and **removes duplicate rows** by default.

### UNION Requirements

- Same number of columns in each SELECT  
- Similar data types  
- Same column order  

--

### UNION Syntax

| Command | Description |
|--------|------------|
| `SELECT column_name(s) FROM table1 UNION SELECT column_name(s) FROM table2;` | Combine results from two SELECT statements (duplicates removed) |

--

### UNION with WHERE Clause

| Command | Description |
|--------|------------|
| `SELECT City, Country FROM Customers WHERE Country='Germany' UNION SELECT City, Country FROM Suppliers WHERE Country='Germany' ORDER BY City;` | Combine results from multiple tables with filtering and sorting |