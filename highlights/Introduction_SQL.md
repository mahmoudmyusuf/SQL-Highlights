# Introduction to SQL 
This introduction covers key concepts in SQL, including data storage in tables, common SQL statements, and essential terms like primary and foreign keys. It highlights SQL database types, best practices for query writing, and tips for using aliases, naming conventions, and formatting to improve query efficiency and readability.

---

## 📌 Data Stored in SQL Databases  
1. Stored in **tables**, similar to Excel spreadsheets, with **rows** and **columns**.  
2. Each **row** holds data for a **transaction**.  
3. Each **column** represents a **specific aspect** of the data.  
4. All data in the same **column** must have the same **data type**.  

---

## 📌 SQL Databases  
There are many different types of **SQL databases**, each designed for different purposes. They may have differences in **syntax** and **available functions**.

### 🔹 Some of the most popular SQL databases:  
1. **MySQL**  
2. **Microsoft Access**  
3. **Oracle**  
4. **Microsoft SQL Server**  
5. **PostgreSQL**  

🚀 In these **highlights**, we will use **Microsoft SQL Server**.  

---

## 📌 SQL Statement  
A **SQL statement** is a correctly written **SQL code** that tells the database what action to perform on the data.

### 🔹 Common SQL Statements:  
- `CREATE TABLE` → Creates a **new table** in a database.  
- `DROP TABLE` → Removes a **table** from a database.  
- `SELECT` → Reads and displays **data** from a table (**query**).  

💡 The `SELECT` statement is the most commonly used by **data analysts**.  

---

## 📌 Some Definitions  

### 🔹 Primary Key (PK)  
A **primary key** is a **unique column** in a table that identifies each row.  
- It is commonly the **first column** in tables.  

### 🔹 Foreign Key (FK)  
A **foreign key** is a column in one table that serves as a **primary key in another table**.  

### 🔹 PK & FK Relationships  
- **One-to-One** and **One-to-Many** relationships are the most preferred.  
- **Many-to-Many** relationships are not typically allowed in traditional databases as they complicate the schema.  

### 🔹 Entity Relationship Diagrams (ERD)  
A common way to **visualize data** in a database. These diagrams help analyze database structure by showing:  
1. **Table names**  
2. **Columns in each table**  
3. **Relationships between tables**  

---

## 📌 Database Normalization  
Normalization ensures:  
1. **Tables store logical groupings of data**.  
2. **Data changes occur in a single location**, rather than being duplicated across multiple tables.  
3. **Data can be accessed and manipulated efficiently**.  

💡 *As a data analyst, you don’t need to worry too much about normalization—your main goal is to extract and analyze the data.*  

---

## 📌 SQL Best Practices  

### Case Sensitivity  
- SQL commands (`SELECT`, `FROM`, `WHERE`, etc.) **are NOT case-sensitive**.
- **Best Practice:** Use **uppercase for SQL commands** and lowercase for table/column names.
- **SQL is case-sensitive** when it comes to **text data** stored in SQL tables.  

### Naming Conventions  
- Use **underscores (`_`)** instead of spaces for column names.
- If a table or column name **has spaces**, use **double quotes**:  
```sql
SELECT OrderDate
FROM Sales.SalesOrderHeader;
```

### Handling Text Data  
- **SQL Server can accept single quote (`'`) or double (`"`) quotes for text values.**
- **In MS SQL Server only use single quote (`'`)**
```sql
SELECT FirstName
FROM Person.Person
WHERE FirstName = 'John';
```
- **If text contains an apostrophe (`'`)**:
   - In MS SQL Server, if a string contains a single quote (`'`), you need to **escape it** by doubling the single quote (`''`). 

```sql
SELECT FirstName
FROM Person.Person
WHERE FirstName = 'O''Brien';
```

- Other SQL Server, that  accept single quote (`'`) and double (`"`) quotes for text values, Can deal with the single quote in `"O'Brien"` by using the double (`"`) quotes:

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
WHERE OrderDate > '2011-01-01'  
ORDER BY TotalDue DESC;
```

---
## 📌 Aliases  
Aliasing is commonly used to:  
- **Rename tables** for shorter references.  
- **Rename columns** in query results to make them more readable.  

**Example of table aliasing:**  
```sql
SELECT p.BusinessEntityID, p.FirstName, p.LastName, e.JobTitle 
FROM Person.Person As p
JOIN HumanResources.Employee As e
ON p.BusinessEntityID = e.BusinessEntityID;
```
or without AS:
```sql
SELECT p.BusinessEntityID, p.FirstName, p.LastName, e.JobTitle 
FROM Person.Person p
JOIN HumanResources.Employee e
ON p.BusinessEntityID = e.BusinessEntityID;
```

💡 By following these key takeaways, you can write better, cleaner, and more efficient SQL queries! 🚀

---

### 🔗 Navigation
⬅️ **Previous:** [`Setting Up SQL Server and Database`](setup.md) | ➡️ **Next:** [`SQL Query Essentials`](SQL_Query.md)
