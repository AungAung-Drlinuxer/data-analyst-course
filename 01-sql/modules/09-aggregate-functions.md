# Module 9: Aggregate Functions

## Aggregate Functions ဆိုတာဘာလဲ?

Aggregate functions များသည် row အုပ်စုတစ်ခုမှ တစ်ခုတည်းသောတန်ဖိုး (single value) ကိုပြန်ပေးပါသည်။ ၎င်းတို့ကို GROUP BY clause နှင့်တွဲသုံးလေ့ရှိပြီး data များကိုအကျဉ်းချုပ်တွက်ချက်ရန်အသုံးပြုပါသည်။

Aggregate functions များသည် NULL တန်ဖိုးများကို ignore လုပ်ပါသည် (COUNT(*) မှလွဲ၍)။ ဆိုလိုသည်မှာ NULL ရှိသော rows များကိုတွက်ချက်မှုတွင်မထည့်ပါ။

### အဓိက Aggregate Functions များ

| Function | Description | Return Type | NULL Handling |
|----------|-------------|-------------|---------------|
| COUNT(*) | Row အားလုံးအရေအတွက် | INT | NULL ပါထည့်တွက် |
| COUNT(column) | Non-NULL rows အရေအတွက် | INT | NULL မထည့်တွက် |
| SUM() | စုစုပေါင်းတန်ဖိုး | Numeric | NULL မထည့်တွက် |
| AVG() | ပျမ်းမျှတန်ဖိုး | Numeric | NULL မထည့်တွက် |
| MIN() | အနည်းဆုံးတန်ဖိုး | Same as column | NULL မထည့်တွက် |
| MAX() | အများဆုံးတန်ဖိုး | Same as column | NULL မထည့်တွက် |

### COUNT Function အသေးစိတ်

```sql
-- COUNT(*) - rows အားလုံး (NULL ပါထည့်တွက်)
SELECT COUNT(*) AS TotalRows FROM Employees;

-- COUNT(column) - non-NULL rows သာ
SELECT COUNT(Email) AS EmployeesWithEmail FROM Employees;

-- COUNT(DISTINCT) - unique values အရေအတွက်
SELECT COUNT(DISTINCT Department) AS UniqueDepts FROM Employees;

-- Conditional count (CASE + COUNT)
SELECT 
    COUNT(*) AS Total,
    COUNT(CASE WHEN Gender = 'Male' THEN 1 END) AS MaleCount,
    COUNT(CASE WHEN Gender = 'Female' THEN 1 END) AS FemaleCount
FROM Employees;
```

### SUM Function အသေးစိတ်

```sql
-- Basic SUM
SELECT SUM(TotalAmount) AS TotalSales FROM Orders;

-- SUM with condition
SELECT SUM(TotalAmount) AS Q1Sales 
FROM Orders 
WHERE OrderDate BETWEEN '2024-01-01' AND '2024-03-31';

-- SUM with DISTINCT
SELECT SUM(DISTINCT Price) AS UniquePriceTotal FROM Products;

-- Running total with window function
SELECT OrderDate, Amount,
       SUM(Amount) OVER (ORDER BY OrderDate) AS RunningTotal
FROM DailySales;
```

### AVG Function အသေးစိတ်

```sql
-- Basic AVG
SELECT AVG(Salary) AS AverageSalary FROM Employees;

-- AVG with ROUND
SELECT ROUND(AVG(Salary), 2) AS AvgSalary FROM Employees;

-- AVG with NULL handling
SELECT AVG(ISNULL(Salary, 0)) AS AvgSalary FROM Employees;
-- NULL များကို 0 အဖြစ်သတ်မှတ်ပြီးတွက်

-- Weighted average (SUM/SUM)
SELECT 
    SUM(Quantity * Price) / SUM(Quantity) AS WeightedAvgPrice
FROM OrderItems;
```

### MIN / MAX Functions အသေးစိတ်

```sql
-- Numeric
SELECT 
    MIN(Price) AS Cheapest,
    MAX(Price) AS MostExpensive,
    MAX(Price) - MIN(Price) AS PriceRange
FROM Products;

-- Date
SELECT 
    MIN(OrderDate) AS FirstOrder,
    MAX(OrderDate) AS LastOrder,
    DATEDIFF(DAY, MIN(OrderDate), MAX(OrderDate)) AS DaysOfOperation
FROM Orders;

-- String (alphabetical)
SELECT 
    MIN(ProductName) AS FirstProduct,
    MAX(ProductName) AS LastProduct
FROM Products;
```

### Aggregate Functions with GROUP BY (ပေါင်းစပ်အသုံးပြုခြင်း)

```sql
SELECT 
    Department,
    COUNT(*) AS EmployeeCount,
    AVG(Salary) AS AvgSalary,
    MIN(Salary) AS MinSalary,
    MAX(Salary) AS MaxSalary,
    SUM(Salary) AS TotalSalary,
    AVG(DATEDIFF(YEAR, HireDate, GETDATE())) AS AvgTenure
FROM Employees
WHERE Status = 'Active'
GROUP BY Department
HAVING COUNT(*) >= 3
ORDER BY AvgSalary DESC;
```

### Aggregate with CASE (Pivot Style)

```sql
SELECT 
    Department,
    SUM(CASE WHEN Gender = 'M' THEN 1 ELSE 0 END) AS MaleCount,
    SUM(CASE WHEN Gender = 'F' THEN 1 ELSE 0 END) AS FemaleCount,
    AVG(CASE WHEN Gender = 'M' THEN Salary END) AS MaleAvgSalary,
    AVG(CASE WHEN Gender = 'F' THEN Salary END) AS FemaleAvgSalary
FROM Employees
GROUP BY Department;
```

## Exercises

1. Orders မှ 2024 ခုနှစ်အတွက် စုစုပေါင်းရောင်းအား (SUM)၊ ပျမ်းမျှ (AVG)၊ အမြင့်ဆုံး (MAX) နှင့် အနိမ့်ဆုံး (MIN) ကိုထုတ်ပါ။
2. Customer တစ်ယောက်ချင်းစီအတွက် order အရေအတွက်နှင့် စုစုပေါင်းပမာဏကိုထုတ်ပါ။
3. တစ်နှစ်ချင်းစီအတွက် ရောင်းအားကိုတွက်ပါ (YEAR ဖြင့် GROUP BY)။
4. Category အလိုက် product အရေအတွက်၊ ပျမ်းမျှဈေး၊ စုစုပေါင်း stock ကိုထုတ်ပါ။

## Aggregate Functions အသေးစိတ် (Complete Reference)

Aggregate functions များသည် row အုပ်စုတစ်ခုမှတစ်ခုတည်းသောတန်ဖိုး (single value) ကိုပြန်ပေးပါသည်။ ၎င်းတို့သည် NULL တန်ဖိုးများကို ignore လုပ်ပါသည် (COUNT(*) မှလွဲ၍)။

### COUNT Function သုံးပုံသုံးနည်းများ

COUNT(*) — rows အားလုံးကိုရေတွက်သည် (NULL ပါထည့်တွက်သည်)
COUNT(column) — non-NULL rows များကိုသာရေတွက်သည်
COUNT(DISTINCT column) — unique values အရေအတွက်ကိုရေတွက်သည်

```sql
SELECT 
    COUNT(*) AS TotalRows,
    COUNT(Email) AS Emails,
    COUNT(DISTINCT City) AS UniqueCities
FROM Customers;
```

### SUM Function အသေးစိတ်

SUM သည် numeric column တစ်ခု၏စုစုပေါင်းကိုတွက်ပါသည်။ NULL values များကိုထည့်မတွက်ပါ။

```sql
SELECT 
    SUM(Quantity) AS TotalQuantity,
    SUM(Quantity * UnitPrice) AS TotalRevenue,
    SUM(DISTINCT Price) AS UniquePriceTotal
FROM OrderItems;
```

### AVG Function သုံးပုံ

AVG သည် ပျမ်းမျှတန်ဖိုးကိုတွက်ပါသည်။ NULL values များကိုထည့်မတွက်ပါ။

```sql
SELECT 
    AVG(Salary) AS MeanSalary,
    ROUND(AVG(Salary), 2) AS RoundedAvg,
    AVG(ISNULL(Salary, 0)) AS AvgWithZeros  -- NULL ကို 0 အဖြစ်သတ်မှတ်
FROM Employees;
```

### MIN / MAX Functions

MIN နှင့် MAX သည် numeric, date, string တို့အတွက်အသုံးပြုနိုင်ပါသည်။

```sql
SELECT 
    MIN(Price) AS Cheapest,
    MAX(Price) AS MostExpensive,
    MAX(Price) - MIN(Price) AS PriceRange,
    MIN(OrderDate) AS FirstOrder,
    MAX(OrderDate) AS LastOrder,
    MIN(ProductName) AS FirstAlphabetically,
    MAX(ProductName) AS LastAlphabetically
FROM Products;
```

### Aggregate with GROUP BY (ပေါင်းစပ်အသုံးပြုခြင်း)

```sql
SELECT 
    Department,
    COUNT(*) AS EmpCount,
    AVG(Salary) AS AvgSal,
    MIN(Salary) AS MinSal,
    MAX(Salary) AS MaxSal,
    SUM(Salary) AS TotalSal,
    AVG(DATEDIFF(YEAR, HireDate, GETDATE())) AS AvgYears
FROM Employees
WHERE Status = 'Active'
GROUP BY Department
HAVING COUNT(*) >= 3
ORDER BY AvgSal DESC;
```

### Practical Business Examples

**Example 1: Sales Summary by Category**
```sql
SELECT 
    COALESCE(c.CategoryName, 'Uncategorized') AS Category,
    COUNT(DISTINCT p.ProductID) AS Products,
    SUM(oi.Quantity) AS UnitsSold,
    SUM(oi.Quantity * oi.UnitPrice) AS Revenue,
    AVG(oi.UnitPrice) AS AvgPrice
FROM Categories c
LEFT JOIN Products p ON c.CategoryID = p.CategoryID
LEFT JOIN OrderItems oi ON p.ProductID = oi.ProductID
GROUP BY c.CategoryName
ORDER BY Revenue DESC;
```

**Example 2: Customer Purchase Behavior**
```sql
SELECT 
    CustomerID,
    COUNT(*) AS OrderCount,
    SUM(TotalAmount) AS TotalSpent,
    AVG(TotalAmount) AS AvgOrder,
    MIN(TotalAmount) AS MinOrder,
    MAX(TotalAmount) AS MaxOrder,
    COUNT(CASE WHEN TotalAmount > 1000 THEN 1 END) AS LargeOrders
FROM Orders
GROUP BY CustomerID
ORDER BY TotalSpent DESC;
```

### Common Mistakes with Aggregate Functions

၁။ **Aggregate နှင့် Non-aggregate Column တွဲသုံးခြင်း** — GROUP BY မပါပဲ aggregate function နှင့် regular column တွဲသုံးပါက error ဖြစ်ပါသည်
```sql
-- မှားသည် (Error)
SELECT Name, MAX(Salary) FROM Employees;

-- မှန်သည်
SELECT Name, Salary FROM Employees WHERE Salary = (SELECT MAX(Salary) FROM Employees);
```

၂။ **NULL တန်ဖိုးများကိုထည့်မတွက်ခြင်း** — AVG, SUM, COUNT(column) တို့သည် NULL ကိုထည့်မတွက်ပါ
```sql
-- သတိထားရန်
SELECT AVG(Salary) FROM Employees;  -- NULL များကိုထည့်မတွက်ပါ
SELECT SUM(Salary)/COUNT(*) FROM Employees;  -- NULL ကို 0 အဖြစ်သတ်မှတ်မည်
```

၃။ **GROUP BY မေ့ခြင်း** — Aggregate သုံးပါက GROUPby လိုအပ်သည်မဟုတ်သော်လည်း detail လိုပါက GROUP BY သုံးရန်

### Exercises

၁။ Products table မှ category အလိုက် product အရေအတွက်၊ ပျမ်းမျှဈေး၊ စုစုပေါင်း stock ကိုထုတ်ပါ
၂။ Orders table မှ 2024 ခုနှစ်အတွင်း တစ်လချင်းစီရဲ့ စုစုပေါင်းရောင်းအား၊ ပျမ်းမျှ order ပမာဏနှင့် order အရေအတွက်ကိုတွက်ပါ
၃။ Customers မှ city အလိုက် customer အရေအတွက်နှင့် စုစုပေါင်းရောင်းအားကိုတွက်ပါ
၄။ ဌာနတစ်ခုစီမှာ လစာအမြင့်ဆုံးနှင့်အနိမ့်ဆုံး employee များကိုရှာပါ
၅။ ပျမ်းမျှလစာထက်များသော employees များကိုရှာပါ (subquery သုံးပါ)

### Statistical Aggregate Functions

SQL Server တွင် standard aggregates အပြင် statistical aggregates များလည်းပါဝင်ပါသည်-

```sql
SELECT 
    AVG(Price) AS Mean,
    STDEV(Price) AS StdDev,    -- Standard deviation
    STDEVP(Price) AS PopStdDev, -- Population standard deviation
    VAR(Price) AS Variance,     -- Variance
    VARP(Price) AS PopVariance  -- Population variance
FROM Products;
```

**GROUP BY with ROLLUP, CUBE, GROUPING SETS** —

```sql
-- ROLLUP: Subtotals + Grand Total
SELECT Department, JobTitle, COUNT(*) AS EmpCount
FROM Employees
GROUP BY ROLLUP(Department, JobTitle);

-- GROUPING: Identify subtotal rows
SELECT 
    CASE WHEN GROUPING(Department) = 1 THEN 'All Depts' ELSE Department END AS Dept,
    CASE WHEN GROUPING(JobTitle) = 1 THEN 'All Roles' ELSE JobTitle END AS Role,
    COUNT(*) AS Count
FROM Employees
GROUP BY ROLLUP(Department, JobTitle);
```
