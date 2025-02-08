
# SQL Query Essentials

## 📖 Overview  
SQL (Structured Query Language) is the standard language for interacting with relational databases, used to **retrieve, manipulate, and manage data** stored in databases.  
This guide covers the **core SQL statements** needed to **query data effectively**, including `SELECT`, `TOP`, `ORDER BY`, `WHERE`, `LIKE`, and `IN`.

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
SELECT * FROM Sales.SalesOrderHeader;
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

### 4.1 Filtering Numeric Data  
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

### 4.2 Filtering Non-Numeric Data  
Retrieve **customers from London**:
```sql
SELECT BusinessEntityID, FirstName, LastName, City  
FROM Person.Person  
WHERE City = 'London';
```
Retrieve **customers NOT from London**:
```sql
SELECT BusinessEntityID, FirstName, LastName, City  
FROM Person.Person  
WHERE City != 'London';
```

### 4.3 Using WHERE with Operators  
#### LIKE (Pattern Matching)  
Find customers whose **first name starts with "A"**:
```sql
SELECT BusinessEntityID, FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'A%';
```
Find customers whose **last name contains "son"**:
```sql
SELECT BusinessEntityID, FirstName, LastName  
FROM Person.Person  
WHERE LastName LIKE '%son%';
```

#### NOT LIKE (Excluding Patterns)  
Find customers whose **first name does not start with "A"**:
```sql
SELECT BusinessEntityID, FirstName, LastName  
FROM Person.Person  
WHERE FirstName NOT LIKE 'A%';
```

#### IN (Multiple Values)  
Find customers from **London, Paris, or Sydney**:
```sql
SELECT BusinessEntityID, FirstName, LastName, City  
FROM Person.Person  
WHERE City IN ('London', 'Paris', 'Sydney');
```

#### NOT IN (Excluding Values)  
Find customers **not from London or Paris**:
```sql
SELECT BusinessEntityID, FirstName, LastName, City  
FROM Person.Person  
WHERE City NOT IN ('London', 'Paris');
```

#### AND (Combining Conditions)  
Find orders where **TotalDue is greater than 1000** **and** the **OrderDate is after January 1, 2024**:
```sql
SELECT SalesOrderID, OrderDate, TotalDue  
FROM Sales.SalesOrderHeader  
WHERE TotalDue > 1000  
  AND OrderDate > '2024-01-01';
```

#### OR (Alternative Conditions)  
Find orders where the **TotalDue is less than 500** **or** the **CustomerID is 10001**:
```sql
SELECT SalesOrderID, OrderDate, TotalDue  
FROM Sales.SalesOrderHeader  
WHERE TotalDue < 500  
   OR CustomerID = 10001;
```

#### BETWEEN (Range of Values)  
Find orders where **TotalDue is between 500 and 1000**:
```sql
SELECT SalesOrderID, OrderDate, TotalDue  
FROM Sales.SalesOrderHeader  
WHERE TotalDue BETWEEN 500 AND 1000;
```

#### IS (Null Values)  
Find **orders where `ShippedDate` is `NULL`** (i.e., not yet shipped):
```sql
SELECT SalesOrderID, OrderDate, ShippedDate  
FROM Sales.SalesOrderHeader  
WHERE ShippedDate IS NULL;
```

#### IS NOT (Not Null Values)  
Find **orders where `ShippedDate` is NOT `NULL`** (i.e., shipped orders):
```sql
SELECT SalesOrderID, OrderDate, ShippedDate  
FROM Sales.SalesOrderHeader  
WHERE ShippedDate IS NOT NULL;
```

#### NULL as a Special Case  
When dealing with `NULL`, SQL treats it as a special case. **NULLs**:
- are a datatype that specifies where no data exists in SQL. They differ from zeros or spaces.  
- often ignored in aggregation functions.  
- When identifying `NULL` values in a `WHERE` clause, we use **`IS NULL`** or **`IS NOT NULL`** instead of `=`. **`NULL`** isn't considered a value in SQL, but rather a property of the data.  
- **NULLs** frequently occur when performing **Joins** or dealing with missing data.

---

## 5️⃣ SQL Best Practices  

### Case Sensitivity  
- SQL commands (`SELECT`, `FROM`, `WHERE`, etc.) **are NOT case-sensitive**.
- **Best Practice:** Use **uppercase for SQL commands** and lowercase for table/column names.

### Naming Conventions  
- Use **underscores (`_`)** instead of spaces for column names.
- If a table or column name **has spaces**, use **double quotes**:  
```sql
SELECT "Order Date" FROM Sales.SalesOrderHeader;
```

### Handling Text Data  
- **Use single quotes (`'`) for text values**:
```sql
SELECT FirstName FROM Person.Person WHERE FirstName = 'John';
```
- **If text contains an apostrophe (`'`), use double quotes (`"`)**:
```sql
SELECT FirstName FROM Person.Person WHERE FirstName = "O'Brien";
```

### SQL Query Formatting  
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
```

---

This updated `.md` file includes examples for `NOT LIKE`, `AND`, `OR`, `BETWEEN`, `IS`, `IS NOT`, and the special handling of `NULL` values. Let me know if you need further refinements!
# SQL Query Essentials

## 📖 Overview  
SQL (Structured Query Language) is the standard language for interacting with relational databases, used to **retrieve, manipulate, and manage data** stored in databases.  
This guide covers the **core SQL statements** needed to **query data effectively**, including `SELECT`, `TOP`, `ORDER BY`, `WHERE`, `LIKE`, and `IN`.

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
SELECT * FROM Sales.SalesOrderHeader;
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

### 4.1 Filtering Numeric Data  
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

### 4.2 Filtering Non-Numeric Data  
Retrieve **customers from London**:
```sql
SELECT BusinessEntityID, FirstName, LastName, City  
FROM Person.Person  
WHERE City = 'London';
```
Retrieve **customers NOT from London**:
```sql
SELECT BusinessEntityID, FirstName, LastName, City  
FROM Person.Person  
WHERE City != 'London';
```

### 4.3 Using WHERE with Operators  
#### LIKE (Pattern Matching)  
Find customers whose **first name starts with "A"**:
```sql
SELECT BusinessEntityID, FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'A%';
```
Find customers whose **last name contains "son"**:
```sql
SELECT BusinessEntityID, FirstName, LastName  
FROM Person.Person  
WHERE LastName LIKE '%son%';
```

#### IN (Multiple Values)  
Find customers from **London, Paris, or Sydney**:
```sql
SELECT BusinessEntityID, FirstName, LastName, City  
FROM Person.Person  
WHERE City IN ('London', 'Paris', 'Sydney');
```

#### NOT IN (Excluding Values)  
Find customers **not from London or Paris**:
```sql
SELECT BusinessEntityID, FirstName, LastName, City  
FROM Person.Person  
WHERE City NOT IN ('London', 'Paris');
```

---

## 5️⃣ SQL Best Practices  

### Case Sensitivity  
- SQL commands (`SELECT`, `FROM`, `WHERE`, etc.) **are NOT case-sensitive**.
- **Best Practice:** Use **uppercase for SQL commands** and lowercase for table/column names.

### Naming Conventions  
- Use **underscores (`_`)** instead of spaces for column names.
- If a table or column name **has spaces**, use **double quotes**:  
```sql
SELECT "Order Date" FROM Sales.SalesOrderHeader;
```

### Handling Text Data  
- **Use single quotes (`'`) for text values**:
```sql
SELECT FirstName FROM Person.Person WHERE FirstName = 'John';
```
- **If text contains an apostrophe (`'`), use double quotes (`"`)**:
```sql
SELECT FirstName FROM Person.Person WHERE FirstName = "O'Brien";
```

### SQL Query Formatting  
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
| SQL Statement  | Purpose | Example |
|---------------|---------|---------|
| **SELECT** | Retrieve data | `SELECT * FROM Sales.SalesOrderHeader;` |
| **TOP** | Limit rows (SQL Server) | `SELECT TOP 10 * FROM Sales.SalesOrderHeader;` |
| **ORDER BY** | Sort results | `ORDER BY OrderDate DESC;` |
| **WHERE** | Filter data | `WHERE TotalDue > 1000;` |
| **LIKE** | Pattern matching | `WHERE FirstName LIKE 'A%';` |
| **IN** | Match multiple values | `WHERE City IN ('London', 'Paris');` |

This guide provides SQL essentials using **AdventureWorks2022** in **Microsoft SQL Server**. 🚀  

---
