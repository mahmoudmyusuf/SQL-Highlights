# Key Takeaways and Notes

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

## 📌 Aliases  
Aliasing is commonly used to:  
- **Rename tables** for shorter references.  
- **Rename columns** in query results to make them more readable.  

**Example of table aliasing:**  
```sql
SELECT c.name, o.order_date  
FROM customers AS c  
JOIN orders AS o ON c.id = o.customer_id;
```
or without AS:
```sql
SELECT c.name, o.order_date  
FROM customers c  
JOIN orders o ON c.id = o.customer_id;
```

💡 By following these key takeaways, you can write better, cleaner, and more efficient SQL queries! 🚀
