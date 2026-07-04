# Module 8: LIMIT, ORDER BY, OFFSET, GROUP BY & HAVING

## ORDER BY Clause (ဒေတာစီခြင်း)

ORDER BY clause သည် query result များကိုသတ်မှတ်ထားသော column အလိုက်စီပေးပါသည်။ မူလအားဖြင့် ascending (ASC) ဖြစ်ပြီး descending (DESC) ကိုသတ်မှတ်နိုင်ပါသည်။ ORDER BY သည် SELECT statement ၏နောက်ဆုံး clause ဖြစ်ပြီး result set ကိုစီရန်သာအသုံးပြုပါသည်။

### ORDER BY Syntax နှင့်နမူနာများ

```sql
-- Ascending order (မူလ)
SELECT ProductName, Price FROM Products ORDER BY Price ASC;

-- Descending order
SELECT ProductName, Price FROM Products ORDER BY Price DESC;

-- Column များစွာဖြင့်စီခြင်း
SELECT Department, LastName, FirstName, Salary
FROM Employees
ORDER BY Department ASC, Salary DESC;
-- Department အလိုက်စီပြီး Department တူပါက Salary ကြီးသူကအရင်

-- Column position ဖြင့်စီခြင်း (အကြံမပြု)
SELECT ProductName, Price, Category FROM Products ORDER BY 2 DESC;
-- Column 2 (Price) ဖြင့်စီခြင်း

-- Expression ဖြင့်စီခြင်း
SELECT ProductName, Price, Quantity, Price * Quantity AS Total
FROM Sales
ORDER BY Total DESC;
```

### ORDER with NULL Values

NULL များကို မူလအားဖြင့် ascending တွင် နောက်ဆုံး၊ descending တွင် ရှေ့ဆုံးတွင်ထားပါသည်။

```sql
-- SQL Server: NULL ကအရင်
SELECT Name, Email FROM Customers ORDER BY Email ASC;
-- NULL emails များကအရင်ပေါ်မည်

-- NULL ကိုနောက်ဆုံးထားရန်
SELECT Name, Email FROM Customers 
ORDER BY CASE WHEN Email IS NULL THEN 1 ELSE 0 END, Email;
```

## LIMIT / OFFSET-FETCH (ဒေတာကန့်သတ်ခြင်း)

Result set မှ row အရေအတွက်ကိုကန့်သတ်ရန်အသုံးပြုပါသည်။ Pagination (စာမျက်နှာခွဲပြခြင်း) အတွက်အဓိကအသုံးပြုပါသည်။

```sql
-- SQL Server (OFFSET-FETCH, SQL 2012+)
SELECT ProductName, Price 
FROM Products 
ORDER BY Price DESC
OFFSET 0 ROWS          -- ပထမ row ကစ
FETCH NEXT 10 ROWS ONLY;  -- 10 row ယူမည်

-- Page 2 (rows 11-20)
SELECT ProductName, Price 
FROM Products 
ORDER BY Price DESC
OFFSET 10 ROWS 
FETCH NEXT 10 ROWS ONLY;

-- PostgreSQL / MySQL (LIMIT-OFFSET)
SELECT * FROM Products ORDER BY Price DESC LIMIT 10;
SELECT * FROM Products ORDER BY Price DESC LIMIT 10 OFFSET 20;
SELECT * FROM Products ORDER BY Price DESC LIMIT 10, 20;  -- MySQL alternative
```

### Pagination Best Practice

Keyset pagination သည် OFFSET pagination ထက်ပိုမြန်ပါသည် (large dataset များအတွက်)။

```sql
-- Keyset Pagination (performance အကောင်းဆုံး)
SELECT ProductID, ProductName, Price
FROM Products
WHERE ProductID > @LastProductID  -- နောက်ဆုံးမြင်ခဲ့ရသော ID
ORDER BY ProductID
FETCH NEXT 20 ROWS ONLY;
```

## GROUP BY Clause (အုပ်စုဖွဲ့ခြင်း)

GROUP BY သည် rows များကို column တစ်ခုသို့မဟုတ်များစွာအလိုက်အုပ်စုဖွဲ့ပြီး aggregate functions များနှင့်တွဲသုံးပါသည်။

### GROUP BY Rules

1. SELECT clause တွင် GROUP BY မှာပါသော columns များသာပါရမည်
2. Aggregate functions (SUM, COUNT, AVG) များပါဝင်နိုင်
3. GROUP BY မှာမပါသော column ကို SELECT ထဲမှာထည့်၍မရ

```sql
-- တစ်ခုတည်းဖြင့်အုပ်စုဖွဲ့ခြင်း
SELECT Department, COUNT(*) AS EmployeeCount
FROM Employees
GROUP BY Department;

-- Column များစွာဖြင့်အုပ်စုဖွဲ့ခြင်း
SELECT Department, JobTitle, COUNT(*) AS EmpCount, AVG(Salary) AS AvgSalary
FROM Employees
GROUP BY Department, JobTitle
ORDER BY Department, AvgSalary DESC;

-- GROUP BY with expressions
SELECT 
    YEAR(OrderDate) AS OrderYear,
    MONTH(OrderDate) AS OrderMonth,
    COUNT(*) AS OrderCount,
    SUM(TotalAmount) AS TotalSales
FROM Orders
GROUP BY YEAR(OrderDate), MONTH(OrderDate)
ORDER BY OrderYear DESC, OrderMonth DESC;
```

### Aggregate Functions with GROUP BY

```sql
SELECT 
    Category,
    COUNT(*) AS ProductCount,
    COUNT(DISTINCT SupplierID) AS SupplierCount,
    AVG(Price) AS AvgPrice,
    MIN(Price) AS MinPrice,
    MAX(Price) AS MaxPrice,
    SUM(StockQuantity) AS TotalStock
FROM Products
GROUP BY Category
ORDER BY AvgPrice DESC;
```

## HAVING Clause (Group စစ်ထုတ်ခြင်း)

HAVING သည် GROUP BY ပြီးမှ group များကိုစစ်ထုတ်ပါသည်။ WHERE က row အဆင့်တွင်စစ်ပြီး HAVING က group အဆင့်တွင်စစ်ပါသည်။

### WHERE vs HAVING

| Aspect | WHERE | HAVING |
|--------|-------|--------|
| အသုံးပြုချိန် | GROUP BY မလုပ်မီ | GROUP BY လုပ်ပြီး |
| Aggregate function | မသုံးနိုင် | သုံးနိုင် |
| Row/Group filter | Row အဆင့် | Group အဆင့် |
| Performance | ပိုမြန် | နှေးနိုင် |

```sql
-- WHERE vs HAVING နှိုင်းယှဉ်ချက်
SELECT Department, AVG(Salary) AS AvgSalary
FROM Employees
WHERE Status = 'Active'              -- Row အဆင့်စစ် (Active employees)
GROUP BY Department
HAVING AVG(Salary) > 50000          -- Group အဆင့်စစ် (Avg salary > 50K)
ORDER BY AvgSalary DESC;

-- ဌာနတစ်ခုစီမှာ အနည်းဆုံး employee 5 ယောက်ရှိရန်
SELECT Department, COUNT(*) AS EmpCount, AVG(Salary) AS AvgSalary
FROM Employees
WHERE Status = 'Active'
GROUP BY Department
HAVING COUNT(*) >= 5
ORDER BY EmpCount DESC;
```

## GROUP BY Variations

### GROUP BY ROLLUP
```sql
SELECT Department, JobTitle, COUNT(*) AS EmpCount
FROM Employees
GROUP BY ROLLUP(Department, JobTitle);
-- Subtotal နှင့် Grand total များပါထည့်ပေးပါသည်
```

### GROUP BY CUBE
```sql
SELECT Department, JobTitle, COUNT(*) AS EmpCount
FROM Employees
GROUP BY CUBE(Department, JobTitle);
-- All possible combinations အတွက် subtotals
```

### GROUP BY GROUPING SETS
```sql
SELECT Department, JobTitle, COUNT(*) AS EmpCount
FROM Employees
GROUP BY GROUPING SETS (
    (Department, JobTitle),
    (Department),
    ()
);
-- သတ်မှတ်ထားသော groupings အတွက်သာ subtotals
```

## Exercises

1. Orders table မှ customer အလိုက် order အရေအတွက်နှင့် စုစုပေါင်းပမာဏကိုထုတ်ပါ။
2. ပျမ်းမျှလစာ 40000 ကျော်သော department များကိုရှာပါ။
3. Products မှ category အလိုက် product အရေအတွက်နှင့် ပျမ်းမျှဈေးကိုထုတ်ပါ။
4. Order အများဆုံး 5 ယောက်ကိုရှာပါ (TOP 5 with GROUP BY)။
5. ရက်စွဲအလိုက် စုစုပေါင်းရောင်းအား၏ running total ကိုတွက်ပါ။

## GROUP BY အသေးစိတ် (Advanced Grouping Techniques)

GROUP BY သည် rows များကို column တစ်ခုသို့မဟုတ်များစွာအလိုက်အုပ်စုဖွဲ့ပြီး aggregate functions များနှင့်တွဲသုံးပါသည်။ ၎င်းသည် data ကိုအကျဉ်းချုပ်တွက်ချက်ရန်အတွက်အဓိက clause တစ်ခုဖြစ်ပါသည်။

### GROUP BY ၏လုပ်ဆောင်ပုံ

GROUP BY လုပ်ဆောင်သည့်အခါ အောက်ပါအဆင့်များအတိုင်းလုပ်ဆောင်ပါသည် —
၁။ WHERE clause ကိုအရင် apply လုပ်ပြီး rows များကိုစစ်ထုတ်ပါသည်
၂။ GROUP BY column အလိုက် rows များကိုအုပ်စုဖွဲ့ပါသည်
၃။ အုပ်စုတစ်ခုချင်းစီအတွက် aggregate functions များကိုတွက်ချက်ပါသည်
၄။ HAVING clause ဖြင့်အုပ်စုများကိုထပ်မံစစ်ထုတ်ပါသည်
၅။ SELECT clause မှ columns များကိုပြသပါသည်

### GROUP BY Rules (အရေးကြီးသောစည်းမျဉ်းများ)

၁။ SELECT clause တွင် GROUP BY ထဲမှာပါသော columns များသာပါရမည်
၂။ Aggregate functions (SUM, COUNT, AVG, MIN, MAX) များပါဝင်နိုင်
၃။ GROUP BY မှာမပါသော column ကို SELECT ထဲမှာထည့်၍မရ (error ဖြစ်မည်)
၄။ Column alias ကို GROUP BY မှာမသုံးရ (actual column name ကိုသုံးရမည်)
၅။ Expressions (YEAR(), MONTH()) များကိုသုံးနိုင်ပါသည်

### GROUP BY နမူနာများစွာ

```sql
-- 1. ဌာနအလိုက် employee အရေအတွက်နှင့်ပျမ်းမျှလစာ
SELECT Department, COUNT(*) AS Count, AVG(Salary) AS AvgSalary
FROM Employees
WHERE Status = 'Active'
GROUP BY Department;

-- 2. နှစ်နှင့်လအလိုက် စုစုပေါင်းရောင်းအား
SELECT YEAR(OrderDate) AS Year, MONTH(OrderDate) AS Month,
       SUM(TotalAmount) AS TotalSales
FROM Orders
GROUP BY YEAR(OrderDate), MONTH(OrderDate)
ORDER BY Year, Month;

-- 3. ဌာနနှင့်ရာထူးအလိုက် လစာခွဲခြမ်းစိတ်ဖြာခြင်း
SELECT Department, JobTitle,
       COUNT(*) AS EmpCount,
       AVG(Salary) AS AvgSal,
       MIN(Salary) AS MinSal,
       MAX(Salary) AS MaxSal
FROM Employees
GROUP BY Department, JobTitle
ORDER BY Department, AvgSal DESC;
```

### HAVING vs WHERE ကွာခြားချက်အသေးစိတ်

WHERE သည် GROUP BY မလုပ်မီ row အဆင့်တွင်စစ်ပါသည်။ HAVING သည် GROUP BY ပြီးမှ group အဆင့်တွင်စစ်ပါသည်။

```sql
-- WHERE: rows များကိုအရင်စစ်
-- HAVING: groups များကိုနောက်မှစစ်
SELECT Department, AVG(Salary) AS AvgSalary
FROM Employees
WHERE Status = 'Active'         -- Step 1: Filter rows
GROUP BY Department             -- Step 2: Group
HAVING AVG(Salary) > 50000     -- Step 3: Filter groups
ORDER BY AvgSalary DESC;
```

### GROUP BY Performance Tips

၁။ GROUP BY columns များတွင် index ထားပါ — query ပိုမြန်ပါသည်
၂။ WHERE clause ဖြင့်အရင်စစ်ပါ — GROUP BY မလုပ်မီ data ကိုလျှော့ချပါ
၃။ GROUP BY column များတွင် functions များရှောင်ပါ — WHERE YEAR(Date) ထက် WHERE Date >= ကိုသုံးပါ
၄။ အလွန်အကျွံ GROUP BY columns များကိုရှောင်ပါ — performance ထိခိုက်နိုင်
၅။ COUNT(DISTINCT col) ကိုသတိသုံးပါ — performance နှေးတတ်ပါသည်
