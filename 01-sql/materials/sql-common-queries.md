# SQL Common Queries Collection

## 1. Department-wise Employee Stats

```sql
SELECT 
    d.DepartmentName,
    COUNT(e.EmployeeID) AS EmployeeCount,
    AVG(e.Salary) AS AverageSalary,
    MIN(e.Salary) AS MinSalary,
    MAX(e.Salary) AS MaxSalary
FROM Departments d
LEFT JOIN Employees e ON d.DepartmentID = e.DepartmentID
GROUP BY d.DepartmentName
ORDER BY AverageSalary DESC;
```

## 2. Daily Sales with Running Total

```sql
SELECT 
    OrderDate,
    DailyTotal,
    SUM(DailyTotal) OVER (ORDER BY OrderDate) AS RunningTotal,
    AVG(DailyTotal) OVER (ORDER BY OrderDate ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS MovingAvg7Days
FROM (
    SELECT 
        CAST(OrderDate AS DATE) AS OrderDate,
        SUM(TotalAmount) AS DailyTotal
    FROM Orders
    GROUP BY CAST(OrderDate AS DATE)
) AS Daily
ORDER BY OrderDate;
```

## 3. Customer Segmentation (RFM)

```sql
WITH CustomerSales AS (
    SELECT 
        CustomerID,
        COUNT(*) AS Frequency,
        SUM(TotalAmount) AS Monetary,
        MAX(OrderDate) AS LastOrder
    FROM Orders
    GROUP BY CustomerID
)
SELECT 
    c.Name,
    cs.Frequency,
    cs.Monetary,
    DATEDIFF(DAY, cs.LastOrder, GETDATE()) AS Recency,
    CASE 
        WHEN cs.Monetary >= 10000 THEN 'Platinum'
        WHEN cs.Monetary >= 5000 THEN 'Gold'
        ELSE 'Standard'
    END AS Segment
FROM CustomerSales cs
JOIN Customers c ON cs.CustomerID = c.CustomerID
ORDER BY cs.Monetary DESC;
```

## 4. Find and Delete Duplicates

```sql
-- Find duplicates
SELECT Email, COUNT(*) FROM Users GROUP BY Email HAVING COUNT(*) > 1;

-- Delete duplicates (keep oldest)
WITH CTE AS (
    SELECT *, ROW_NUMBER() OVER (PARTITION BY Email ORDER BY UserID) AS rn
    FROM Users
)
DELETE FROM CTE WHERE rn > 1;
```

## 5. Row-to-Column Pivot

```sql
SELECT 
    Department,
    SUM(CASE WHEN Gender = 'M' THEN 1 ELSE 0 END) AS MaleCount,
    SUM(CASE WHEN Gender = 'F' THEN 1 ELSE 0 END) AS FemaleCount
FROM Employees
GROUP BY Department;
```

## 6. Top Employee per Department (by Salary)

```sql
SELECT EmployeeID, Name, Department, Salary
FROM (
    SELECT *, RANK() OVER (PARTITION BY Department ORDER BY Salary DESC) AS rnk
    FROM Employees
) ranked WHERE rnk = 1;
```

## 7. Month-over-Month Growth

```sql
WITH Monthly AS (
    SELECT YEAR(OrderDate) Yr, MONTH(OrderDate) Mo, SUM(Amount) AS Total
    FROM Orders GROUP BY YEAR(OrderDate), MONTH(OrderDate)
)
SELECT Yr, Mo, Total,
    LAG(Total) OVER (ORDER BY Yr, Mo) AS PrevMonth,
    (Total - LAG(Total) OVER (ORDER BY Yr, Mo)) * 100.0 / 
        NULLIF(LAG(Total) OVER (ORDER BY Yr, Mo), 0) AS GrowthPct
FROM Monthly ORDER BY Yr, Mo;
```


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
