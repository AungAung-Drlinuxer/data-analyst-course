# Module 14: CTEs (Common Table Expressions)

## CTE ဆိုတာဘာလဲ?

CTE (Common Table Expression) သည် query တစ်ခုအတွင်း temporary result set တစ်ခုကိုသတ်မှတ်ပေးသောနည်းလမ်းဖြစ်ပြီး WITH clause ကိုအသုံးပြုပါသည်။ CTE သည် subquery များထက်ပိုမိုရှင်းလင်းပြီး recursive queries များအတွက်အထူးသင့်တော်ပါသည်။

### CTE Syntax

```sql
WITH CTEName AS (
    -- CTE query (AS clause အတွင်းတွင်)
    SELECT column1, column2, ...
    FROM table
    WHERE condition
)
-- Main query (CTE ကိုအသုံးပြုသော)
SELECT * FROM CTEName;
```

### ရိုးရိုး CTE ဥပမာများ

```sql
-- Active employees ၏ဌာနအလိုက်ပျမ်းမျှလစာ
WITH ActiveEmployees AS (
    SELECT EmployeeID, Name, Salary, Department
    FROM Employees
    WHERE Status = 'Active'
)
SELECT Department, AVG(Salary) AS AvgSalary, COUNT(*) AS EmpCount
FROM ActiveEmployees
GROUP BY Department
ORDER BY AvgSalary DESC;

-- ရောင်းအားကောင်းသော products များ
WITH TopProducts AS (
    SELECT ProductID, SUM(Quantity * UnitPrice) AS TotalRevenue
    FROM OrderItems
    GROUP BY ProductID
)
SELECT p.ProductName, tp.TotalRevenue
FROM TopProducts tp
INNER JOIN Products p ON tp.ProductID = p.ProductID
ORDER BY tp.TotalRevenue DESC;
```

### Multiple CTEs

CTE များစွာကိုတစ်ပြိုင်နက်သတ်မှတ်နိုင်ပြီး ၎င်းတို့အချင်းချင်းလည်းရည်ညွှန်းနိုင်ပါသည်။

```sql
WITH 
SalesSummary AS (
    SELECT 
        CustomerID,
        SUM(Amount) AS TotalSpent,
        COUNT(*) AS OrderCount,
        MAX(OrderDate) AS LastOrderDate
    FROM Orders
    GROUP BY CustomerID
),
HighValueCustomers AS (
    SELECT CustomerID, TotalSpent, OrderCount
    FROM SalesSummary
    WHERE TotalSpent > 10000
)
SELECT c.Name, c.Email, h.TotalSpent, h.OrderCount
FROM HighValueCustomers h
INNER JOIN Customers c ON h.CustomerID = c.CustomerID
ORDER BY h.TotalSpent DESC;
```

### Recursive CTE

Recursive CTE သည် ၎င်းကိုယ်၎င်းပြန်ခေါ်သော CTE ဖြစ်ပြီး hierarchical data (organization chart, category tree, bill of materials) များအတွက်အသုံးပြုပါသည်။

Recursive CTE တွင် အပိုင်း ၂ ပိုင်းပါဝင်ပါသည်-
1. **Anchor Member** — ပထမဆုံး iteration (base case)
2. **Recursive Member** — နောက်ဆက်တွဲ iterations (UNION ALL ဖြင့်ချိတ်ဆက်)

```sql
-- Organization Chart (Manager Hierarchy)
WITH OrgChart AS (
    -- Anchor: အပေါ်ဆုံးအဆင့် (CEO/Manager မရှိသူ)
    SELECT 
        EmployeeID, 
        Name, 
        ManagerID, 
        0 AS Level,
        CAST(Name AS VARCHAR(500)) AS Path
    FROM Employees
    WHERE ManagerID IS NULL
    
    UNION ALL
    
    -- Recursive: အောက်အဆင့်များ
    SELECT 
        e.EmployeeID, 
        e.Name, 
        e.ManagerID, 
        o.Level + 1,
        CAST(o.Path + ' > ' + e.Name AS VARCHAR(500))
    FROM Employees e
    INNER JOIN OrgChart o ON e.ManagerID = o.EmployeeID
)
SELECT EmployeeID, Name, Level, Path
FROM OrgChart
ORDER BY Level, Name;
```

### CTE vs Subquery vs Temp Table

| Feature | CTE | Subquery | Temp Table |
|---------|-----|----------|------------|
| Readability | အကောင်းဆုံး | အတန်အသင့် | အတန်အသင့် |
| Reusability | တစ်ကြိမ်သာ | တစ်ကြိမ်သာ | Session တစ်လျှောက် |
| Recursive | ရ | မရ | မရ |
| Index | မရ | မရ | ရ |
| Performance | ကောင်း | အတန်အသင့် | အကောင်းဆုံး |

## Exercises

1. CTE သုံးပြီး 2024 ခုနှစ်တွင် order ၅ ခုထက်ပိုသော customers များကိုရှာပါ။
2. Recursive CTE သုံးပြီး category tree (Parent → Child → SubChild) ဆောက်ပါ။
3. Multiple CTEs သုံးပြီး monthly sales summary နှင့် growth rate တွက်ပါ။

## CTE အသေးစိတ် (Complete CTE Guide)

CTE (Common Table Expression) သည် query တစ်ခုအတွင်း temporary result set တစ်ခုကိုသတ်မှတ်ပေးသောနည်းလမ်းဖြစ်ပြီး WITH clause ကိုအသုံးပြုပါသည်။

### CTE ၏အားသာချက်များ

၁။ **Readability** — Complex query များကိုရှင်းလင်းစေသည် (အပိုင်းလိုက်ခွဲရေးနိုင်)
၂။ **Reusability** — CTE ကို query ထဲမှာအကြိမ်များစွာသုံးနိုင်
၃။ **Recursive** — Hierarchical data (org chart, category tree) အတွက်အကောင်းဆုံး
၄။ **Maintenance** — Query ကိုအပိုင်းပိုင်းခွဲထားသဖြင့်ပြုပြင်ရလွယ်ကူ

### Multiple CTEs သုံးပုံ

```sql
WITH 
SalesSummary AS (
    SELECT CustomerID, SUM(Amount) AS TotalSpent, COUNT(*) AS OrderCount
    FROM Orders GROUP BY CustomerID
),
VIPCustomers AS (
    SELECT CustomerID, TotalSpent
    FROM SalesSummary
    WHERE TotalSpent > 10000
)
SELECT c.Name, c.Email, v.TotalSpent
FROM VIPCustomers v
JOIN Customers c ON v.CustomerID = c.CustomerID
ORDER BY v.TotalSpent DESC;
```

### Recursive CTE အသေးစိတ်

Recursive CTE တွင် အပိုင်း ၂ ပိုင်းပါဝင်ပါသည်-
၁။ **Anchor Member** — ပထမဆုံး iteration (base case, စတင်ရန်)
၂။ **Recursive Member** — နောက်ဆက်တွဲ iterations (UNION ALL ဖြင့်ချိတ်ဆက်)

```sql
-- Employee Hierarchy (Manager → Subordinate)
WITH OrgChart AS (
    -- Anchor: CEO / Top-level managers
    SELECT EmployeeID, Name, ManagerID, 0 AS Level,
           CAST(Name AS VARCHAR(500)) AS OrgPath
    FROM Employees WHERE ManagerID IS NULL
    UNION ALL
    -- Recursive: အောက်အဆင့်များ
    SELECT e.EmployeeID, e.Name, e.ManagerID, o.Level + 1,
           CAST(o.OrgPath + ' → ' + e.Name AS VARCHAR(500))
    FROM Employees e
    INNER JOIN OrgChart o ON e.ManagerID = o.EmployeeID
)
SELECT EmployeeID, 
       REPLICATE('  ', Level) + Name AS DisplayName,
       Level, OrgPath
FROM OrgChart
ORDER BY Level, Name;
```

### CTE Best Practices

၁။ CTE ကိုရှင်းလင်းသော name ပေးပါ (ဘာ data မှန်းသိရန်)
၂။ Multiple CTEs များလွန်းပါက temp table သို့ပြောင်းပါ (performance)
၃။ Recursive CTE တွင် MAXRECURSION option သုံးပါ (infinite loop ကာကွယ်ရန်)
၄။ CTE သည် query တစ်ခုအတွက်သာသက်ရောက်ပါသည် (next query တွင်မရတော့ပါ)

### Exercises

၁။ CTE သုံးပြီး 2024 ခုနှစ်တွင် order ၅ခုထက်ပိုသော customers များကိုရှာပါ
၂။ Recursive CTE သုံးပြီး category tree (Parent → Child → SubChild) ဆောက်ပါ
၃။ Multiple CTEs သုံးပြီး monthly sales summary နှင့် growth rate တွက်ပါ



### CTE vs Temp Table vs Table Variable

| Aspect | CTE | Temp Table (#temp) | Table Variable (@var) |
|--------|-----|-------------------|----------------------|
| Scope | Single query | Session/SP | Batch/SP |
| Storage | Memory | TempDB | Memory (mostly) |
| Index | Not indexable | Indexable | PK only |
| Statistics | No stats | Full stats | No stats |
| Transaction log | None | Yes | Minimal |
| Performance | Good for small | Good for large | Good for small |

**ဘယ်အချိန်ဘယ်ဟာသုံးမလဲ?**

- **CTE** — Small-medium data, single query, recursive needs
- **Temp Table** — Large data, multiple queries, needs index
- **Table Variable** — Small data, simple queries, avoids recompilation

CTE သည် recursion လိုအပ်လျှင် (သို့) query ကိုရှင်းလင်းစေရန်အသုံးပြုပါသည်။

### CTE Practical Examples

**Example 1: Paginated Results with Row Number**
```sql
WITH NumberedProducts AS (
    SELECT ProductID, ProductName, Price,
           ROW_NUMBER() OVER (ORDER BY Price DESC) AS RowNum
    FROM Products
)
SELECT ProductID, ProductName, Price
FROM NumberedProducts
WHERE RowNum BETWEEN 21 AND 30;  -- Page 3 (10 items per page)
```

**Example 2: Hierarchical Category Tree**
```sql
WITH CategoryCTE AS (
    SELECT CategoryID, CategoryName, ParentID, 0 AS Level
    FROM Categories WHERE ParentID IS NULL
    UNION ALL
    SELECT c.CategoryID, c.CategoryName, c.ParentID, ct.Level + 1
    FROM Categories c
    INNER JOIN CategoryCTE ct ON c.ParentID = ct.CategoryID
)
SELECT CategoryID, 
       REPLICATE('--', Level) + CategoryName AS DisplayName,
       Level
FROM CategoryCTE
ORDER BY Level, CategoryName;
```

**Example 3: Running Total with CTE**
```sql
WITH Sales AS (
    SELECT OrderDate, SUM(Amount) AS DailyTotal
    FROM Orders GROUP BY OrderDate
),
RunningTotal AS (
    SELECT OrderDate, DailyTotal,
           SUM(DailyTotal) OVER (ORDER BY OrderDate) AS TotalToDate
    FROM Sales
)
SELECT OrderDate, DailyTotal, TotalToDate
FROM RunningTotal
ORDER BY OrderDate;
```

CTE များသည် complex queries များကိုရှင်းလင်းစေပြီး modular approach ဖြင့်ရေးသားနိုင်ပါသည်။



### CTE Best Practices Summary

၁။ **Meaningful Names** — CTE ၏အမည်ကို၎င်း၏အလုပ်ကိုဖော်ပြသောနာမည်ပေးပါ (SalesSummary, ActiveEmployees, CategoryTree)

၂။ **Multiple CTEs ကိုရှင်းလင်းစွာသုံးပါ** — CTE တစ်ခုစီသည် logical step တစ်ခုကိုကိုယ်စားပြုပါစေ

၃။ **Recursive CTE Limit** — SQL Server တွင် MAXRECURSION option သုံးပြီး recursion depth ကိုကန့်သတ်ပါ
```sql
WITH OrgCTE AS (...) 
SELECT * FROM OrgCTE
OPTION (MAXRECURSION 100);  -- Maximum 100 levels
```

၄။ **Performance Considerations** — Large datasets အတွက် CTE ထက် temp table သုံးပါ

၅။ **Readability** — CTE သည် query ကိုရှင်းလင်းစေသော်လည်းအလွန်အကျွံသုံးပါက nested subquery များထက်ပိုမိုရှုပ်ထွေးသွားနိုင်ပါသည်

CTE များသည် SQL query ရေးသားခြင်းကိုပိုမိုရှင်းလင်းစေပြီး modular approach ဖြင့်ရေးသားနိုင်စေပါသည်။ အထူးသဖြင့် recursive queries များအတွက် CTE သည်တစ်ခုတည်းသောရွေးချယ်မှုဖြစ်ပါသည်။
