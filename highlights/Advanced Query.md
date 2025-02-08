# Understanding SQL JOINs with Examples from AdventureWorks

## Introduction
The purpose of JOIN statements is to allow us to pull data from more than one table at a time. JOINs are useful for retrieving related data stored across multiple tables. This is both simple and powerful at the same time.

With the addition of the JOIN statement to our toolkit, we also introduce the **ON** clause. The **ON** clause specifies a JOIN condition—a logical statement that combines tables in **FROM** and **JOIN** statements.

## JOIN Condition
Our SQL query includes two tables:
- One in the **FROM** clause (referred to as the LEFT table)
- One in the **JOIN** clause (referred to as the RIGHT table)

In the **ON** clause, we will always match the **Primary Key (PK)** of one table to the **Foreign Key (FK)** of the other table.

## Types of JOINs

### INNER JOIN
Retrieves only matching rows that exist in both tables.

```sql
SELECT p.BusinessEntityID, p.FirstName, p.LastName, e.JobTitle 
FROM Person.Person p
JOIN HumanResources.Employee e
ON p.BusinessEntityID = e.BusinessEntityID;
```
*Example:* This query retrieves employees from the `Employee` table and their corresponding personal details from the `Person` table where there is a match in `BusinessEntityID`.

---
### LEFT JOIN (LEFT OUTER JOIN)
Retrieves all rows from the LEFT table and the matching rows from the RIGHT table. If there is no match, NULL values are returned for columns from the RIGHT table.

```sql
SELECT p.BusinessEntityID, p.FirstName, p.LastName, e.JobTitle 
FROM Person.Person p
LEFT JOIN HumanResources.Employee e
ON p.BusinessEntityID = e.BusinessEntityID;
```
*Example:* This query retrieves all people from the `Person` table, along with their job titles from the `Employee` table. If a person is not an employee, their job title will be NULL.

---
### RIGHT JOIN (RIGHT OUTER JOIN)
Retrieves all rows from the RIGHT table and the matching rows from the LEFT table. If there is no match, NULL values are returned for columns from the LEFT table.

```sql
SELECT e.BusinessEntityID, e.JobTitle, p.FirstName, p.LastName 
FROM HumanResources.Employee e
RIGHT JOIN Person.Person p
ON p.BusinessEntityID = e.BusinessEntityID;
```
*Example:* This query retrieves all employees and their corresponding personal details. If an employee does not have a corresponding record in `Person`, NULL values will appear in those columns.

---
### FULL OUTER JOIN
Retrieves all rows from both tables, matching rows where possible. If no match is found, NULL values are used for columns from the missing table.

```sql
SELECT p.BusinessEntityID, p.FirstName, p.LastName, e.JobTitle 
FROM Person.Person p
FULL OUTER JOIN HumanResources.Employee e
ON p.BusinessEntityID = e.BusinessEntityID;
```
*Example:* This query retrieves all people and employees, even if they do not have a match in the other table. NULL values appear where there is no match.

## NULL Values in JOINs
New JOINs allow us to pull rows that might only exist in one of the two tables. This introduces a new data type called **NULL**, which represents missing values. NULLs will be covered in detail in a future lesson.

## Execution Order
When executing a query, the database processes the **JOIN** and everything in the **ON** clause first. Understanding this helps optimize queries and avoid unexpected results.

## Conclusion
JOINs are essential in SQL for combining data from multiple tables. The type of JOIN used depends on the desired result:
- **INNER JOIN** → Matching rows only
- **LEFT JOIN** → All left table rows + matched right table rows
- **RIGHT JOIN** → All right table rows + matched left table rows
- **FULL OUTER JOIN** → All rows from both tables

By mastering JOINs, you can efficiently retrieve complex data relationships from databases like AdventureWorks.
