# SQL Cheat Sheet

## 1️⃣ Introduction & Basics
This cheat sheet covers SQL syntax and common commands used to manage and query databases.

### SQL Comments
- **Single-line comments**: `--`  
- **Multi-line comments**: `/* comment */`

---

### Semicolon in SQL
- Some database systems require a semicolon `;` at the end of each SQL statement.  
- Semicolon separates multiple statements in one call.
---

### SQL Arithmetic Operators

| Operator | Description |
|----------|------------|
| `+`      | Addition |
| `-`      | Subtraction |
| `*`      | Multiplication |
| `/`      | Division |
| `%`      | Modulo |
---

### SQL Aliases
- Give a temporary name to a column or table.  
- `AS` keyword is optional.

| Command | Description |
|---------|------------|
| `SELECT column_name AS alias_name FROM table_name;` | Column alias using AS |
| `SELECT column_name alias_name FROM table_name;` | Column alias without AS |
| `SELECT column_name FROM table_name AS alias_name;` | Table alias using AS |
| `SELECT column_name FROM table_name alias_name;` | Table alias without AS |

---

## 2️⃣ Retrieving Data

### SELECT

| Command | Description |
|---------|------------|
| `SELECT * FROM Customers;` | Select all records |
| `SELECT CustomerName, City FROM Customers;` | Select specific columns |
| `SELECT DISTINCT Country FROM Customers;` | Return distinct values |
| `SELECT COUNT(DISTINCT Country) FROM Customers;` | Count distinct values |

---

#### Logical Operators

| Command | Description |
|---------|------------|
| `AND` | All conditions must be TRUE |
| `OR` | Any condition TRUE |
| `NOT` | Reverses a condition |

#### SQL Operators

| Operator | Description |
|----------|------------|
| `=` | Equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater or equal |
| `<=` | Less or equal |
| `<>` or `!=` | Not equal |
| `BETWEEN` | Within a range |
| `LIKE` | Pattern match |
| `IN` | Multiple values |

---

### WHERE
Filters rows that meet a condition.
| Command | Description |
|---------|------------|
| `SELECT * FROM Customers WHERE Country='Mexico';` | Customers from Mexico |
| `SELECT * FROM Customers WHERE CustomerID > 80;` | Customers with ID > 80 |

**NULL Values**
| Command | Description |
|---------|------------|
| `SELECT column_names FROM table_name WHERE column_name IS NULL;` | Selects records where the column value is NULL |
| `SELECT column_names FROM table_name WHERE column_name IS NOT NULL;` | Selects records where the column value is NOT NULL |

### LIKE Operator & Wildcards

Use `LIKE` in `WHERE` to match patterns.

| Wildcard | Meaning |
|----------|--------|
| `%` | Any number of characters |
| `_` | Single character |
| `[]` | Any single character in set (SQL Server/Oracle) |
| `-` | Range inside `[]` |
| `^` | Not in set (SQL Server/Oracle) |

**Examples:**

| Pattern | Description |
|---------|------------|
| `'La%'` | Starts with 'La' |
| `'%a'` | Ends with 'a' |
| `'%or%'` | Contains 'or' |
| `'a__%'` | Starts with 'a' + at least 3 chars |
| `'_r%'` | 'r' in 2nd position |
| `'Spain'` | Exact match |

### IN / NOT IN Operator
| Command | Description |
|---------|------------|
| `SELECT * FROM table WHERE column_name IN (value1, value2, ...)` | Returns rows where the column matches any value in the list |
| `SELECT * FROM table WHERE column_name NOT IN (value1, value2, ...)` | Returns rows where the column does not match any value in the list |
| `SELECT * FROM table WHERE column_name IN (SELECT column_name FROM table_name)` | Returns rows matching values from a subquery |
| `SELECT * FROM table WHERE column_name NOT IN (SELECT column_name FROM table_name)` | Returns rows not matching values from a subquery |

---

### BETWEEN / NOT BETWEEN Operator

Selects values within a range (inclusive).

| Command | Description |
|---------|------------|
| `SELECT * FROM table WHERE column_name BETWEEN value1 AND value2` | Returns rows where the column is within the range |
| `SELECT * FROM table WHERE column_name NOT BETWEEN value1 AND value2` | Returns rows where the column is outside the range |
| `SELECT * FROM table WHERE column_name BETWEEN 'Text1' AND 'Text2'` | Works with text values (alphabetical range) |
| `SELECT * FROM table WHERE column_name BETWEEN 'StartDate' AND 'EndDate'` | Works with dates |
---

### EXISTS Operator

The `EXISTS` operator tests for the existence of any record in a subquery.  
Returns TRUE if the subquery returns one or more rows. Used in a `WHERE` clause.

| Command | Description |
|---------|------------|
| `SELECT * FROM table WHERE EXISTS (SELECT column_name FROM table_name WHERE condition);` | Returns rows from the outer table if the subquery returns any record |
| `SELECT * FROM table WHERE NOT EXISTS (SELECT column_name FROM table_name WHERE condition);` | Returns rows from the outer table if the subquery returns no record |

---

### SQL ANY / ALL Operators

Used in a `WHERE` clause to compare a column with values from a subquery.

| Command                                                                                         | Description                                                    |
| ----------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| `SELECT * FROM table WHERE column_name = ANY (SELECT column_name FROM table2 WHERE condition);` | TRUE if **any** value in the subquery meets the condition      |
| `SELECT * FROM table WHERE column_name > ANY (SELECT column_name FROM table2 WHERE condition);` | TRUE if **at least one** value in the subquery satisfies the condition |
| `SELECT * FROM table WHERE column_name = ALL (SELECT column_name FROM table2 WHERE condition);` | TRUE only if **all** values in the subquery meet the condition |
| `SELECT * FROM table WHERE column_name < ALL (SELECT column_name FROM table2 WHERE condition);` | TRUE if **every** value in the subquery satisfies the condition |

**Notes:**  
- `ANY` → condition is true if **any one** value meets it.  
- `ALL` → condition is true only if **all** values meet it.  
- Works with standard comparison operators: `=, <>, !=, >, >=, <, <=`.
 
 ---

### ORDER BY
Sort results (ASC default, DESC for descending).

| Command | Description |
|---------|------------|
| `SELECT * FROM Products ORDER BY Price;` | Ascending |
| `SELECT * FROM Products ORDER BY Price DESC;` | Descending |
| `SELECT * FROM Customers ORDER BY Country, CustomerName;` | Multiple columns |

### SELECT TOP / LIMIT / FETCH
Return limited rows.

| DB | Command | 
|----|--------|
| SQL Server | `SELECT TOP 10 * FROM table;`|
| MySQL | `SELECT * FROM table LIMIT 10;` 
| Oracle 12+ | `SELECT * FROM table FETCH FIRST 10 ROWS ONLY;`|

---

## 3️⃣ Aggregations & Grouping

### Aggregate Functions
Aggregate functions perform a calculation on a set of values and return a **single value**.

| Command | Description |
|----------|------------|
| `SELECT MIN(column) FROM TABLE` | Smallest value |
| `SELECT MAX(column) FROM TABLE` | Largest value |
| `SELECT COUNT(column) FROM TABLE` | Count non-NULL |
| `SELECT COUNT(*) FROM TABLE` | Count all rows |
| `SELECT SUM(column) FROM TABLE` | Sum of numeric values |
| `SELECT AVG(column) FROM TABLE` | Average value |

---

### GROUP BY
The **GROUP BY** clause is used to **group rows that have the same values** in specified columns.  
It is often used with **aggregate functions** (COUNT, SUM, AVG, MIN, MAX) to return **summary information per group**.  

| Command | Description |
|---------|------------|
| `SELECT Country, COUNT(*) FROM Customers GROUP BY Country;` | Groups customers by `Country` and counts the number of customers in each country |
| `SELECT Country, COUNT(*) FROM Customers GROUP BY Country HAVING COUNT(*) > 5;` | Groups customers by `Country`, counts them, and **filters groups** where the count is greater than 5 |

**Notes:**  
- `HAVING` is like `WHERE` but **applies to groups** rather than individual rows.

---

### CASE Expression
The **CASE** expression allows you to implement **conditional logic** in SQL queries.  
It works like an `IF-THEN-ELSE` statement and can be used in `SELECT`, `UPDATE`, `ORDER BY`, and other clauses.

| Command | Description |
|---------|------------|
| `CASE WHEN condition1 THEN result1 WHEN condition2 THEN result2 ... WHEN conditionN THEN resultN ELSE result END;` | Evaluates multiple conditions sequentially and **returns the corresponding result** for the first condition that is true. |

**Notes:**  
- You can have multiple `WHEN ... THEN ...` clauses to handle different conditions.  
- The `ELSE` clause is optional; if omitted, unmatched rows return `NULL`.  
---

## 4️⃣ Modifying Data

### INSERT INTO

| Command | Description |
|---------|------------|
| `INSERT INTO table_name (col1, col2) VALUES (val1, val2);` | Insert specific columns |
| `INSERT INTO table_name VALUES (val1, val2, ...);` | Insert all columns |
| `INSERT INTO table_name (col1, col2) VALUES (val1a, val2a), (val1b, val2b);` | Multiple rows (not Oracle) |

---

### UPDATE

| Command | Description |
|---------|------------|
| `UPDATE Customers SET ContactName='Juan' WHERE CustomerID=1;` | Update specific row(s) |
| `UPDATE Customers SET ContactName='Juan';` | Update all rows |

---

### DELETE

| Command | Description |
|---------|------------|
| `DELETE FROM Customers WHERE CustomerID=1;` | Delete specific rows |
| `DELETE FROM Customers;` | Delete all rows |

---

### SELECT INTO
Copy data into a new table.

| Command | Description |
|---------|------------|
| `SELECT * INTO new_table FROM old_table;` | Copy all columns |
| `SELECT col1, col2 INTO new_table FROM old_table;` | Copy specific columns |

---

### INSERT INTO … SELECT
Copy data into an existing table.

| Command | Description |
|---------|------------|
| `INSERT INTO table2 SELECT * FROM table1;` | Copy all columns |
| `INSERT INTO table2 (col1, col2) SELECT col3, col4 FROM table1;` | Copy specific columns |

---

## 5️⃣ Table & Database Management

### CREATE / DROP DATABASE

| Command | Description |
|---------|------------|
| `CREATE DATABASE dbname;` | Create database |
| `DROP DATABASE dbname;` | Drop database |

---

### BACKUP DATABASE (SQL Server)

| Command | Description |
|---------|------------|
| `BACKUP DATABASE dbname TO DISK = 'filepath';` | Full backup |

---

### CREATE / DROP TABLE

| Command | Description |
|---------|------------|
| `CREATE TABLE table_name (column1 datatype, column2 datatype, ...);` | Creates a new table with specified columns and data types |
| `CREATE TABLE new_table AS SELECT column1, column2 FROM existing_table WHERE ...;` | Creates a new table from an existing table with optional filtering |
| `DROP TABLE table_name;` | Delete table |
| `ALTER TABLE table_name ADD col datatype;` | Add column |
| `ALTER TABLE table_name DROP COLUMN col;` | Drop column |
| `ALTER TABLE table_name ALTER/MODIFY COLUMN col datatype;` | Change column type |
| `ALTER TABLE table_name RENAME COLUMN old TO new;` | Rename column |

---

### SQL ALTER TABLE

| Command | Description |
|--------|------------|
| `ALTER TABLE table_name ADD column_name datatype;` | Adds a new column to an existing table |
| `ALTER TABLE table_name DROP COLUMN column_name;` | Deletes a column from a table (some DBs may not allow this) |
| `ALTER TABLE table_name RENAME COLUMN old_name TO new_name;` | Renames a column (SQL standard) |
| `EXEC sp_rename 'table_name.old_name', 'new_name', 'COLUMN';` | Renames a column in SQL Server |
| `ALTER TABLE table_name ALTER COLUMN column_name datatype;` | Changes the data type of a column (SQL Server / MS Access) |
| `ALTER TABLE table_name MODIFY COLUMN column_name datatype;` | Changes the data type of a column (MySQL / Oracle) |

---

### Constraints

| Constraint | Description |
|------------|------------|
| `NOT NULL` | Cannot be NULL |
| `UNIQUE` | Unique values |
| `PRIMARY KEY` | Unique identifier |
| `FOREIGN KEY` | Referential integrity between tables|
| `CHECK` | Condition check |
| `DEFAULT` | Default value |
| `CREATE INDEX` | Creates an index to improve data retrieval speed |

---

## 6️⃣ Advanced Queries 

### JOINs

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
### Union 
The **UNION** operator combines the result-set of two or more `SELECT` statements  
and **removes duplicate rows** by default.

## UNION Requirements
- Same number of columns in each SELECT  
- Similar data types  
- Same column order  

| Command | Description |
|---------|------------|
| `SELECT column_name(s) FROM table1 UNION SELECT column_name(s) FROM table2;` | Combines results from two `SELECT` statements **removing duplicate rows** |
| `SELECT column_name(s) FROM table1 UNION ALL SELECT column_name(s) FROM table2;` | Combines results from two `SELECT` statements **keeping all rows**, including duplicates |

### Primary and foreign keys
## FIND TABLE'S PRIMARY KEY OR COMPOSITE KEY (KEY1,KEY2)
SELECT cols.column_name
FROM user_constraints cons
JOIN user_cons_columns cols
  ON cons.constraint_name = cols.constraint_name
WHERE cons.constraint_type = 'P'
  AND cons.table_name = 'TABLE_NAME';


## FIND TABLE'S FOREIGN KEY(S)
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