# SQL Cheat Sheet pt.2

## SQL Aliases

SQL aliases are used to give a **temporary name** to a table or a column.  
Aliases exist **only for the duration of the query** and are used to make results more readable.  
The `AS` keyword is optional.

---

### Alias Syntax

| Command | Description |
|--------|------------|
| `SELECT column_name AS alias_name FROM table_name;` | Alias for a column |
| `SELECT column_name alias_name FROM table_name;` | Column alias without using AS |
| `SELECT column_name FROM table_name AS alias_name;` | Alias for a table |
| `SELECT column_name FROM table_name alias_name;` | Table alias without AS |
| `SELECT column_name AS "My Great Column" FROM table_name;` | Column alias with spaces |
| `SELECT CustomerName, Address + ', ' + PostalCode + ' ' + City + ', ' + Country AS Address FROM Customers;` | Alias combining multiple columns for SQL |
| `SELECT CustomerName, CONCAT(Address, ', ', PostalCode, ', ', City, ', ', Country) AS Address FROM Customers;` | Alias combining multiple columns for MySQL |
| `SELECT CustomerName, (Address || ', ' || PostalCode || ' ' || City || ', ' || Country) AS Address FROM Customers;` | Alias combining multiple columns for Oracle |

---


## SQL JOIN

A JOIN clause is used to **combine rows from two or more tables** based on a related column.

---

### Types of JOINs

| JOIN Type | Description |
|----------|------------|
| INNER JOIN | Returns records that have matching values in both tables |
| LEFT JOIN | Returns all records from the left table and matched records from the right table |
| RIGHT JOIN | Returns all records from the right table and matched records from the left table |
| FULL JOIN | Returns all records when there is a match in either table |

---

## JOIN Syntax

| Command | Description |
|--------|------------|
| `SELECT column_name(s) FROM table1 INNER JOIN table2 ON table1.column_name = table2.column_name;` | General INNER JOIN syntax |
| `SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName FROM ((Orders INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID) INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID);` | Multiple INNER JOINs |
| `SELECT column_name(s) FROM table1 LEFT JOIN table2 ON table1.column_name = table2.column_name;` | LEFT JOIN – returns all records from left table and matched records from right table |
| `SELECT column_name(s) FROM table1 RIGHT JOIN table2 ON table1.column_name = table2.column_name;` | RIGHT JOIN – returns all records from right table and matched records from left table |
| `SELECT column_name(s) FROM table1 FULL OUTER JOIN table2 ON table1.column_name = table2.column_name WHERE condition;` | FULL OUTER JOIN – returns all records when there is a match in either table |

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

---

### UNION Syntax

| Command | Description |
|--------|------------|
| `SELECT column_name(s) FROM table1 UNION SELECT column_name(s) FROM table2;` | Combine results from two SELECT statements (duplicates removed) |

---

### UNION with WHERE Clause

| Command | Description |
|--------|------------|
| `SELECT City, Country FROM Customers WHERE Country='Germany' UNION SELECT City, Country FROM Suppliers WHERE Country='Germany' ORDER BY City;` | Combine results from multiple tables with filtering and sorting |