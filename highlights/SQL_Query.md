
# SQL Query Essentials

## 📖 Overview  
SQL (Structured Query Language) is the standard language for interacting with relational databases, used to **retrieve, manipulate, and manage data** stored in databases.  
This guide covers the **core SQL statements** needed to **query data effectively**, including `SELECT`, `TOP`, `ORDER BY`, `WHERE`, `LIKE`, `IN`, **Derived Columns**, and **SQL Aggregation**.  

This document provides an overview of essential SQL statements using **AdventureWorks2022** in **Microsoft SQL Server**.  

---

## 1️⃣ SELECT Statement  
The `SELECT` statement is used in every query to retrieve data from a database. It consists of **clauses** that specify what data to return.

### Syntax:
```sql
SELECT column1, column2, ...  
FROM table_name;
```
- `SELECT` specifies **which columns** you want to retrieve.
- `FROM` specifies **which table** to retrieve the data from.
- If you want **all columns**, use `*`:
```sql
SELECT *
FROM Sales.SalesOrderHeader;
```
- Selecting specific columns:
```sql
SELECT SalesOrderID, OrderDate, TotalDue  
FROM Sales.SalesOrderHeader;
```
📝 **Note:** The `SELECT` statement does **not** create a new table, it only retrieves and displays the data.

---

## 2️⃣ TOP Statement  
The `TOP` statement restricts the number of rows returned in the query results. SQL Server **uses `TOP`**, while other SQL servers can use `LIMIT` instead.

### Example:  
Retrieve the first **10 rows** from `Sales.SalesOrderHeader`:
```sql
SELECT TOP 10 *  
FROM Sales.SalesOrderHeader;
```
Using `TOP` to limit specific columns:
```sql
SELECT TOP 5 SalesOrderID, OrderDate, TotalDue  
FROM Sales.SalesOrderHeader;
```
📝 **Note:** `TOP` is placed **immediately after `SELECT`**.

---

## 3️⃣ ORDER BY Statement  
The `ORDER BY` clause sorts query results. By default, sorting is **ascending (ASC)**.

### Examples:
Sort **orders by OrderDate (ascending)**:
```sql
SELECT SalesOrderID, OrderDate, TotalDue  
FROM Sales.SalesOrderHeader  
ORDER BY OrderDate;
```
Sort **orders by OrderDate (descending)**:
```sql
SELECT SalesOrderID, OrderDate, TotalDue  
FROM Sales.SalesOrderHeader  
ORDER BY OrderDate DESC;
```
Sort by **CustomerID first, then OrderDate (descending)**:
```sql
SELECT SalesOrderID, CustomerID, OrderDate, TotalDue  
FROM Sales.SalesOrderHeader  
ORDER BY CustomerID, OrderDate DESC;
```
📝 **Note:** `ORDER BY` does **not** change the order in the database, only in query results.

---

## 4️⃣ WHERE Statement (Filtering Data)  
The `WHERE` clause **filters** results based on conditions. It can be split into the following sections:

### 6.1 Filtering Numeric Data  
Retrieve **orders placed after January 1, 2024**:
```sql
SELECT SalesOrderID, OrderDate, TotalDue  
FROM Sales.SalesOrderHeader  
WHERE OrderDate > '2024-01-01';
```
Retrieve **orders where TotalDue is greater than 1000**:
```sql
SELECT SalesOrderID, OrderDate, TotalDue  
FROM Sales.SalesOrderHeader  
WHERE TotalDue > 1000;
```
Retrieve **orders where CustomerID is 10001**:
```sql
SELECT SalesOrderID, OrderDate, TotalDue  
FROM Sales.SalesOrderHeader  
WHERE CustomerID = 10001;
```

---

## 5️⃣ NULLs: Special Case  
NULLs represent missing data or undefined values and are not equal to zeros or spaces. They are often ignored in aggregation functions. **NULLs** frequently occur when performing **Joins** or dealing with missing data.

#### Handling NULLs:
- Use `IS NULL` or `IS NOT NULL` to check for NULL values instead of `=`. **`NULL`** isn't considered a value in SQL, but rather a property of the data. 
- Example:
    ```sql
    SELECT *
    FROM Sales.SalesOrderDetail
    WHERE ShipDate IS NULL;
    ```
---

## 6️⃣ SQL Aggregation (Without GROUP BY)  
SQL aggregation functions are used to summarize or aggregate data. These functions can be used independently of the `GROUP BY` clause to aggregate values across all rows.

### Common Aggregation Functions:
- **COUNT()**: Counts the number of rows.
- **SUM()**: Adds up values.
- **AVG()**: Calculates the average value.
- **MIN()**: Finds the minimum value.
- **MAX()**: Finds the maximum value.

### Examples:

#### COUNT()
Count the **total number of orders**:
```sql
SELECT COUNT(*)  
FROM Sales.SalesOrderHeader;
```
📝 **Note:** `COUNT(*)` counts **all rows**, including those with `NULL` values.

#### SUM()
Find the **total sales amount** for all orders:
```sql
SELECT SUM(TotalDue)  
FROM Sales.SalesOrderHeader;
```
📝 **Note:** `SUM()` can only be used on numeric columns. `NULL` values are ignored in the calculation.

**Adding Condtion for Aggregation**
```sql
SELECT SUM(LineTotal) AS TotalSales
FROM Sales.SalesOrderDetail
WHERE LineTotal > 500;
```
The `SUM(LineTotal)` sums up the values that passed the filter, returning the total sales where LineTotal is greater than 500.

#### MIN()
Find the **earliest order date**:
```sql
SELECT MIN(OrderDate)  
FROM Sales.SalesOrderHeader;
```

#### AVG()
Find the **average total due** for all orders:
```sql
SELECT AVG(TotalDue)  
FROM Sales.SalesOrderHeader;
```
📝 **Note:** `AVG()` can only be used on numeric columns, and `NULL` values are ignored in the calculation.

---

## 7️⃣ SQL Aggregation (With GROUP BY)  
When you want to aggregate data grouped by certain columns, you use the `GROUP BY` clause.

### Example with SUM:  
Find the **total sales** for each **product**:
```sql
SELECT ProductID, SUM(LineTotal) AS TotalSales  
FROM Sales.SalesOrderDetail  
GROUP BY ProductID;
```

### Example with COUNT:
Count the **number of orders** for each **customer**:
```sql
SELECT CustomerID, COUNT(SalesOrderID) AS OrderCount  
FROM Sales.SalesOrderHeader  
GROUP BY CustomerID;
```

### Using Aggregation with `HAVING`  
You can filter the results of an aggregation using `HAVING`:
```sql
SELECT ProductID, SUM(LineTotal) AS TotalSales  
FROM Sales.SalesOrderDetail  
GROUP BY ProductID  
HAVING SUM(LineTotal) > 500;
```
📝 **Note:** `Aggregators` only aggregate vertically — the values of a column.If you want to perform a calculation across rows, you would do this with simple arithmetic..

---

## 8️⃣ Derived Columns  
Derived columns are calculated dynamically from existing data within the query. These columns are temporary and only exist in the output of the query.

### Example:
To calculate the **TotalPrice** for each order based on `Quantity` and `UnitPrice`:
```sql
SELECT ProductID, Quantity, UnitPrice, (Quantity * UnitPrice) AS TotalPrice  
FROM Sales.SalesOrderDetail;
```

---

## 9️⃣ SQL Best Practices  

### Case Sensitivity  
- SQL commands (`SELECT`, `FROM`, `WHERE`, etc.) **are NOT case-sensitive**.
- **Best Practice:** Use **uppercase for SQL commands** and lowercase for table/column names.
- **SQL is case-sensitive** when it comes to **text data** stored in SQL tables.  

### Naming Conventions  
- Use **underscores (`_`)** instead of spaces for column names.
- If a table or column name **has spaces**, use **double quotes**:  
```sql
SELECT "Order Date"
FROM Sales.SalesOrderHeader;
```

### Handling Text Data  
- **You can use single (`'`) or double (`"`) quotes for text values.**
```sql
SELECT FirstName
FROM Person.Person
WHERE FirstName = 'John';
```
- **If text contains an apostrophe (`'`), use double quotes (`"`)**:
```sql
SELECT FirstName
FROM Person.Person
WHERE FirstName = "O'Brien";
```

### SQL Query Formatting  
- **Best practice**: End each statement with a **semicolon (`;`)**.  
   - Some SQL environments **require** a semicolon at the end of your query to execute it.
- Save SQL query files with a `.sql` extension in **Atom** or **Sublime** to enable **SQL syntax highlighting**. 
- **SQL queries ignore spaces**, so you can add as many spaces and blank lines between code as needed.  
- **Use indentation & spacing** for readability:
```sql
SELECT  
    SalesOrderID,  
    OrderDate,  
    TotalDue  
FROM Sales.SalesOrderHeader  
WHERE OrderDate > '2024-01-01'  
ORDER BY TotalDue DESC;
```

---

## 🔹 Summary  

### SQL Statements Overview

| SQL Statement  | Purpose | Example |
|---------------|---------|---------|
| **SELECT** | Retrieve data | `SELECT * FROM Sales.SalesOrderHeader;` |
| **TOP** | Limit rows (SQL Server) | `SELECT TOP 10 * FROM Sales.SalesOrderHeader;` |
| **ORDER BY** | Sort results | `ORDER BY OrderDate DESC;` |
| **WHERE** | Filter data | `WHERE TotalDue > 1000;` |
| **LIKE** | Pattern matching | `WHERE FirstName LIKE 'A%';` |
| **NOT LIKE** | Exclude pattern | `WHERE FirstName NOT LIKE 'A%';` |
| **AND** | Combine conditions | `WHERE TotalDue > 1000 AND OrderDate > '2024-01-01';` |
| **OR** | Alternative conditions | `WHERE TotalDue < 500 OR CustomerID = 10001;` |
| **BETWEEN** | Range of values | `WHERE TotalDue BETWEEN 500 AND 1000;` |
| **IS** | Check for NULL values | `WHERE ShippedDate IS NULL;` |
| **IS NOT** | Check for NOT NULL values | `WHERE ShippedDate IS NOT NULL;` |
| **IN** | Match multiple values | `WHERE City IN ('London', 'Paris');` |
| **NOT IN** | Exclude multiple values | `WHERE City NOT IN ('London', 'Paris');` |

### SQL Aggregation Functions

| Aggregation Function | Purpose | Example |
|----------------------|---------|---------|
| **COUNT()** | Count rows | `SELECT COUNT(*) FROM Sales.SalesOrderHeader;` |
| **SUM()** | Total of a column | `SELECT SUM(TotalDue) FROM Sales.SalesOrderHeader;` |
| **MIN()** | Minimum value | `SELECT MIN(OrderDate) FROM Sales.SalesOrderHeader;` |
| **AVG()** | Average value | `SELECT AVG(TotalDue) FROM Sales.SalesOrderHeader;` |

