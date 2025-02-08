# SQL JOINs Explained with AdventureWorks Examples

## 📖 Overview  
The purpose of **JOIN** statements is to pull data from multiple tables in a relational database. They enable the retrieval of related data stored across different tables, making queries more efficient and powerful. 

When using **JOINs**, we also utilize the **ON** clause, which specifies a logical condition to combine tables. The query always includes:  
- A **LEFT table** (in the `FROM` statement)
- A **RIGHT table** (in the `JOIN` statement)

The **ON** clause ensures that the **Primary Key (PK)** in one table is matched to the **Foreign Key (FK)** in the other table.

---

## 🔗 Types of JOINs

### 1️⃣ INNER JOIN  
Retrieves only matching rows that exist in both tables.

```sql
SELECT p.BusinessEntityID, p.FirstName, p.LastName, e.JobTitle 
FROM Person.Person p
JOIN HumanResources.Employee e
ON p.BusinessEntityID = e.BusinessEntityID;
```
📌 *Example:* This query retrieves employees and their corresponding personal details from the `Person` table where there is a match in `BusinessEntityID`.

---

### 2️⃣ LEFT JOIN (LEFT OUTER JOIN)  
Retrieves all rows from the LEFT table and the matching rows from the RIGHT table. If there is no match, NULL values are returned.

```sql
SELECT p.BusinessEntityID, p.FirstName, p.LastName, e.JobTitle 
FROM Person.Person p
LEFT JOIN HumanResources.Employee e
ON p.BusinessEntityID = e.BusinessEntityID;
```
📌 *Example:* This query retrieves all people from `Person`, along with job titles from `Employee`. If a person is not an employee, their job title will be NULL.

---

### 3️⃣ RIGHT JOIN (RIGHT OUTER JOIN)  
Retrieves all rows from the RIGHT table and the matching rows from the LEFT table. If there is no match, NULL values are returned.

```sql
SELECT e.BusinessEntityID, e.JobTitle, p.FirstName, p.LastName 
FROM HumanResources.Employee e
RIGHT JOIN Person.Person p
ON p.BusinessEntityID = e.BusinessEntityID;
```
📌 *Example:* This query retrieves all employees and their corresponding personal details. If an employee does not have a corresponding record in `Person`, NULL values will appear.

---

### 4️⃣ FULL OUTER JOIN  
Retrieves all rows from both tables, matching rows where possible. If no match is found, NULL values are used.

```sql
SELECT p.BusinessEntityID, p.FirstName, p.LastName, e.JobTitle 
FROM Person.Person p
FULL OUTER JOIN HumanResources.Employee e
ON p.BusinessEntityID = e.BusinessEntityID;
```
📌 *Example:* This query retrieves all people and employees, even if they do not have a match in the other table. NULL values appear where there is no match.

---

## ⚠️ NULL Values in JOINs  
All JOINs except `INNER JOIN` allow us to pull rows that might exist only in one of the tables. This introduces **NULL**, representing missing values. For NULL handling strategies, refer to [SQL_Query](SQL_Query.md).

---

## 🔄 Execution Order  
When executing a query, SQL processes the **JOIN** and everything in the **ON** clause first. Understanding this helps optimize queries and avoid unexpected results.

---

## ✅ Summary  
- **INNER JOIN** → Matching rows only  
- **LEFT JOIN** → All LEFT table rows + matched RIGHT table rows  
- **RIGHT JOIN** → All RIGHT table rows + matched LEFT table rows  
- **FULL OUTER JOIN** → All rows from both tables  

By mastering JOINs, you can efficiently retrieve complex data relationships from databases like **AdventureWorks**.
