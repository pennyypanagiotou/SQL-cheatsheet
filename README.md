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
