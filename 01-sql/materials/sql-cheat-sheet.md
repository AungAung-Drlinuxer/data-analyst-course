# SQL Cheat Sheet — အားလုံးအကျဉ်းချုပ်

## Database Commands

```sql
-- Create Database
CREATE DATABASE DatabaseName;

-- Use Database
USE DatabaseName;

-- Delete Database
DROP DATABASE DatabaseName;

-- View Databases
SELECT name FROM sys.databases;
```

## Table Commands (DDL)

```sql
-- Create Table
CREATE TABLE TableName (
    Column1 INT PRIMARY KEY,
    Column2 VARCHAR(100) NOT NULL,
    Column3 DECIMAL(10,2) DEFAULT 0,
    Column4 DATE
);

-- Alter Table
ALTER TABLE TableName ADD ColumnName DataType;
ALTER TABLE TableName DROP COLUMN ColumnName;
ALTER TABLE TableName ALTER COLUMN ColumnName NewDataType;

-- Drop Table
DROP TABLE TableName;
TRUNCATE TABLE TableName;
```

## Data Manipulation (DML)

```sql
-- Insert
INSERT INTO TableName VALUES (val1, val2, val3);
INSERT INTO TableName (Col1, Col2) VALUES (val1, val2);
INSERT INTO TableName SELECT * FROM AnotherTable;

-- Update
UPDATE TableName SET Column1 = Value1 WHERE Condition;

-- Delete
DELETE FROM TableName WHERE Condition;
```

## Data Query (DQL) — SELECT

```sql
SELECT [DISTINCT] Column1, Column2
FROM Table1
JOIN Table2 ON Table1.Key = Table2.Key
WHERE Condition
GROUP BY Column1
HAVING AggregateCondition
ORDER BY Column1 [ASC|DESC]
OFFSET N ROWS FETCH NEXT M ROWS ONLY;
```

### WHERE Filters

| Operator | Example | Description |
|----------|--------|-------------|
| = | WHERE City = 'Yangon' | တူညီခြင်း |
| <> | WHERE Status <> 'X' | မတူညီခြင်း |
| >, < | WHERE Price > 100 | ကြီး/ငယ်ခြင်း |
| BETWEEN | WHERE Price BETWEEN 50 AND 100 | ကြားကာလ |
| IN | WHERE City IN ('A', 'B', 'C') | စာရင်းထဲမှ |
| LIKE | WHERE Name LIKE 'Aung%' | ပုံစံတူခြင်း |
| IS NULL | WHERE Email IS NULL | NULL စစ်ခြင်း |
```

## JOIN Types

```sql
INNER JOIN  -- Matching rows only
LEFT JOIN   -- All left, matching right
RIGHT JOIN  -- All right, matching left
FULL JOIN   -- All rows both tables
CROSS JOIN  -- Cartesian product
```

## Aggregate Functions

| Function | Description | NULL Handling |
|----------|-------------|---------------|
| COUNT(*) | Row အရေအတွက် | NULL ပါထည့်တွက် |
| COUNT(Col) | Non-NULL row အရေအတွက် | NULL မထည့်တွက် |
| SUM(Col) | စုစုပေါင်း | NULL မထည့်တွက် |
| AVG(Col) | ပျမ်းမျှ | NULL မထည့်တွက် |
| MIN(Col) | အနည်းဆုံး | NULL မထည့်တွက် |
| MAX(Col) | အများဆုံး | NULL မထည့်တွက် |
```

## Window Functions

```sql
ROW_NUMBER() OVER (PARTITION BY Col ORDER BY Col)
RANK() OVER (ORDER BY Col)
DENSE_RANK() OVER (ORDER BY Col)
NTILE(N) OVER (ORDER BY Col)
LAG(Col, N) OVER (ORDER BY Col)
LEAD(Col, N) OVER (ORDER BY Col)
SUM(Col) OVER (PARTITION BY Col ORDER BY Col)
```

## String Functions

| Function | Example | Result |
|----------|---------|--------|
| CONCAT(a, b) | CONCAT('Hello', 'World') | HelloWorld |
| SUBSTRING(s, start, len) | SUBSTRING('Hello', 2, 3) | ell |
| LEFT(s, n) | LEFT('Hello', 2) | He |
| RIGHT(s, n) | RIGHT('Hello', 2) | lo |
| LEN(s) | LEN('Hello') | 5 |
| REPLACE(s, old, new) | REPLACE('ABC', 'B', 'X') | AXC |
| UPPER(s) | UPPER('hello') | HELLO |
| LOWER(s) | LOWER('HELLO') | hello |
| TRIM(s) | TRIM(' Hello ') | Hello |
| CHARINDEX(find, s) | CHARINDEX('l', 'Hello') | 3 |
```

## Date Functions

| Function | Description |
|----------|-------------|
| GETDATE() | ယခုအချိန် (datetime) |
| DATEADD(day, n, date) | ရက်/လ/နှစ် ပေါင်းထည့် |
| DATEDIFF(day, d1, d2) | ရက်/လ/နှစ် ကွာခြားချက် |
| YEAR(date) | နှစ်ဖြတ်ထုတ် |
| MONTH(date) | လဖြတ်ထုတ် |
| DAY(date) | ရက်ဖြတ်ထုတ် |
| EOMONTH(date) | လကုန်ရက် |
| FORMAT(date, fmt) | ရက်စွဲပုံစံချ |
```

## Constraints

1. PRIMARY KEY — Unique + Not Null (table တစ်ခုလျှင်တစ်ခုသာ)
2. FOREIGN KEY — Referential integrity (table ချိတ်ဆက်ရန်)
3. UNIQUE — Column values ထပ်မရ
4. CHECK — Value validation (e.g., Price > 0)
5. DEFAULT — Default value (e.g., GETDATE())
6. NOT NULL — Value ရှိရမည်

## Query Execution Order

FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT/OFFSET

## Performance Tips

1. Avoid SELECT * — Specify only needed columns
2. Use WHERE filters early — Reduce data volume
3. Index JOIN columns — Foreign keys need indexes
4. Prefer JOIN over subquery — Better optimization
5. Use EXISTS over IN — Better with large subqueries
6. Avoid functions in WHERE — SARGable queries
7. Update statistics regularly — Help query optimizer
8. Use appropriate data types — INT for IDs, not VARCHAR
9. Monitor execution plans — Look for table scans
10. Use UNION ALL instead of UNION — If duplicates OK


### Practical Examples

**Example 1: Find Customers Who Haven't Ordered in 90 Days**
```sql
SELECT c.CustomerID, c.Name, c.Email, MAX(o.OrderDate) AS LastOrder
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.Name, c.Email
HAVING MAX(o.OrderDate) IS NULL 
   OR MAX(o.OrderDate) < DATEADD(DAY, -90, GETDATE());
```

**Example 2: Product Category Sales Summary with Running Total**
```sql
SELECT 
    YEAR(o.OrderDate) AS Year,
    p.Category,
    SUM(oi.Quantity * oi.UnitPrice) AS TotalSales,
    DENSE_RANK() OVER (PARTITION BY YEAR(o.OrderDate) ORDER BY SUM(oi.Quantity * oi.UnitPrice) DESC) AS CategoryRank
FROM Orders o
JOIN OrderItems oi ON o.OrderID = oi.OrderID
JOIN Products p ON oi.ProductID = p.ProductID
GROUP BY YEAR(o.OrderDate), p.Category
ORDER BY Year, TotalSales DESC;
```

### Common Interview Questions

1. What is the difference between clustered and non-clustered index?
2. Explain the difference between RANK, DENSE_RANK, and ROW_NUMBER.
3. When would you use a CTE instead of a subquery?
4. What is query execution order in SQL?
5. Explain the difference between UNION and UNION ALL.


### Practical Examples

**Example 1: Find Customers Who Haven't Ordered in 90 Days**
```sql
SELECT c.CustomerID, c.Name, c.Email, MAX(o.OrderDate) AS LastOrder
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.Name, c.Email
HAVING MAX(o.OrderDate) IS NULL 
   OR MAX(o.OrderDate) < DATEADD(DAY, -90, GETDATE());
```

**Example 2: Product Category Sales Summary with Running Total**
```sql
SELECT 
    YEAR(o.OrderDate) AS Year,
    p.Category,
    SUM(oi.Quantity * oi.UnitPrice) AS TotalSales,
    DENSE_RANK() OVER (PARTITION BY YEAR(o.OrderDate) ORDER BY SUM(oi.Quantity * oi.UnitPrice) DESC) AS CategoryRank
FROM Orders o
JOIN OrderItems oi ON o.OrderID = oi.OrderID
JOIN Products p ON oi.ProductID = p.ProductID
GROUP BY YEAR(o.OrderDate), p.Category
ORDER BY Year, TotalSales DESC;
```

### Common Interview Questions

1. What is the difference between clustered and non-clustered index?
2. Explain the difference between RANK, DENSE_RANK, and ROW_NUMBER.
3. When would you use a CTE instead of a subquery?
4. What is query execution order in SQL?
5. Explain the difference between UNION and UNION ALL.


### Practical Examples

**Example 1: Find Customers Who Haven't Ordered in 90 Days**
```sql
SELECT c.CustomerID, c.Name, c.Email, MAX(o.OrderDate) AS LastOrder
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.Name, c.Email
HAVING MAX(o.OrderDate) IS NULL 
   OR MAX(o.OrderDate) < DATEADD(DAY, -90, GETDATE());
```

**Example 2: Product Category Sales Summary with Running Total**
```sql
SELECT 
    YEAR(o.OrderDate) AS Year,
    p.Category,
    SUM(oi.Quantity * oi.UnitPrice) AS TotalSales,
    DENSE_RANK() OVER (PARTITION BY YEAR(o.OrderDate) ORDER BY SUM(oi.Quantity * oi.UnitPrice) DESC) AS CategoryRank
FROM Orders o
JOIN OrderItems oi ON o.OrderID = oi.OrderID
JOIN Products p ON oi.ProductID = p.ProductID
GROUP BY YEAR(o.OrderDate), p.Category
ORDER BY Year, TotalSales DESC;
```

### Common Interview Questions

1. What is the difference between clustered and non-clustered index?
2. Explain the difference between RANK, DENSE_RANK, and ROW_NUMBER.
3. When would you use a CTE instead of a subquery?
4. What is query execution order in SQL?
5. Explain the difference between UNION and UNION ALL.


### Practical Examples

**Example 1: Find Customers Who Haven't Ordered in 90 Days**
```sql
SELECT c.CustomerID, c.Name, c.Email, MAX(o.OrderDate) AS LastOrder
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.Name, c.Email
HAVING MAX(o.OrderDate) IS NULL 
   OR MAX(o.OrderDate) < DATEADD(DAY, -90, GETDATE());
```

**Example 2: Product Category Sales Summary with Running Total**
```sql
SELECT 
    YEAR(o.OrderDate) AS Year,
    p.Category,
    SUM(oi.Quantity * oi.UnitPrice) AS TotalSales,
    DENSE_RANK() OVER (PARTITION BY YEAR(o.OrderDate) ORDER BY SUM(oi.Quantity * oi.UnitPrice) DESC) AS CategoryRank
FROM Orders o
JOIN OrderItems oi ON o.OrderID = oi.OrderID
JOIN Products p ON oi.ProductID = p.ProductID
GROUP BY YEAR(o.OrderDate), p.Category
ORDER BY Year, TotalSales DESC;
```

### Common Interview Questions

1. What is the difference between clustered and non-clustered index?
2. Explain the difference between RANK, DENSE_RANK, and ROW_NUMBER.
3. When would you use a CTE instead of a subquery?
4. What is query execution order in SQL?
5. Explain the difference between UNION and UNION ALL.


### Practical Examples

**Example 1: Find Customers Who Haven't Ordered in 90 Days**
```sql
SELECT c.CustomerID, c.Name, c.Email, MAX(o.OrderDate) AS LastOrder
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.Name, c.Email
HAVING MAX(o.OrderDate) IS NULL 
   OR MAX(o.OrderDate) < DATEADD(DAY, -90, GETDATE());
```

**Example 2: Product Category Sales Summary with Running Total**
```sql
SELECT 
    YEAR(o.OrderDate) AS Year,
    p.Category,
    SUM(oi.Quantity * oi.UnitPrice) AS TotalSales,
    DENSE_RANK() OVER (PARTITION BY YEAR(o.OrderDate) ORDER BY SUM(oi.Quantity * oi.UnitPrice) DESC) AS CategoryRank
FROM Orders o
JOIN OrderItems oi ON o.OrderID = oi.OrderID
JOIN Products p ON oi.ProductID = p.ProductID
GROUP BY YEAR(o.OrderDate), p.Category
ORDER BY Year, TotalSales DESC;
```

### Common Interview Questions

1. What is the difference between clustered and non-clustered index?
2. Explain the difference between RANK, DENSE_RANK, and ROW_NUMBER.
3. When would you use a CTE instead of a subquery?
4. What is query execution order in SQL?
5. Explain the difference between UNION and UNION ALL.
