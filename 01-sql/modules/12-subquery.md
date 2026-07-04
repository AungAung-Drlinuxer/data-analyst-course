# Module 12: Subquery (အသိုက်လိုက် Query များ)

## Subquery ဆိုတာဘာလဲ?

Subquery ဆိုသည်မှာ အခြား query တစ်ခုအတွင်းတွင်ရှိသော query ဖြစ်ပါသည်။ Inner query (အတွင်း query) သည် outer query (အပြင် query) မလုပ်ဆောင်မီအရင် execute လုပ်ပြီး ၎င်း၏ result ကို outer query မှအသုံးပြုပါသည်။ Subquery များသည် parentheses () အတွင်းတွင်ရှိရမည်ဖြစ်ပြီး SELECT, FROM, WHERE, HAVING clauses များတွင်သုံးနိုင်ပါသည်။

## Subquery အမျိုးအစားများ

Subquery ကို ၎င်းပြန်ပေးသော result အမျိုးအစားပေါ်မူတည်ပြီး အုပ်စု ၄ မျိုးခွဲခြားနိုင်ပါသည်-

### ၁။ Scalar Subquery (တန်ဖိုးတစ်ခုတည်းပြန်)

Scalar subquery သည် တန်ဖိုးတစ်ခုတည်း (single value) ကိုပြန်ပေးပါသည်။ ၎င်းကို WHERE, SELECT, HAVING clauses များတွင်သုံးနိုင်ပါသည်။

```sql
-- ပျမ်းမျှလစာထက်များသော employees များကိုရှာခြင်း
SELECT EmployeeID, Name, Salary
FROM Employees
WHERE Salary > (SELECT AVG(Salary) FROM Employees);

-- SELECT clause တွင် scalar subquery သုံးခြင်း
SELECT 
    ProductName,
    Price,
    (SELECT AVG(Price) FROM Products) AS AveragePrice,
    Price - (SELECT AVG(Price) FROM Products) AS PriceDifference
FROM Products;
```

### ၂။ Table Subquery (FROM clause တွင်သုံး)

Table subquery သည် table တစ်ခုလုံးကိုပြန်ပေးပြီး FROM clause တွင် derived table (virtual table) အဖြစ်သုံးပါသည်။ Alias ပေးရန်လိုအပ်ပါသည်။

```sql
SELECT Department, AvgSalary
FROM (
    SELECT Department, AVG(Salary) AS AvgSalary
    FROM Employees
    GROUP BY Department
) AS DeptAvg  -- Alias ပေးရန်လိုအပ်
WHERE AvgSalary > 50000
ORDER BY AvgSalary DESC;
```

### ၃။ Correlated Subquery (ဆက်စပ် Subquery)

Correlated subquery သည် outer query ၏ column ကို inner query မှ reference လုပ်ပါသည်။ Outer row တစ်ခုချင်းစီအတွက် inner query ကိုပြန် run ရပါသည်။

```sql
-- ဌာနတစ်ခုစီတွင် လစာအများဆုံး employee ကိုရှာခြင်း
SELECT e.Name, e.Department, e.Salary
FROM Employees e
WHERE e.Salary = (
    SELECT MAX(Salary)
    FROM Employees
    WHERE Department = e.Department  -- Outer column ကို reference
);
```

Correlated subquery သည် row-by-row execute လုပ်ရသောကြောင့် large dataset များအတွက်နှေးတတ်ပါသည်။ JOIN ဖြင့်ပြောင်းရေးနိုင်လျှင်ပိုကောင်းပါသည်။

### ၄။ EXISTS / NOT EXISTS Subquery

EXISTS သည် subquery ထဲတွင် row တစ်ခုရှိမရှိကိုသာစစ်ပြီး TRUE/FALSE ပြန်ပေးပါသည်။

```sql
-- Order ရှိသော customers များ
SELECT c.CustomerID, c.Name
FROM Customers c
WHERE EXISTS (
    SELECT 1 FROM Orders o 
    WHERE o.CustomerID = c.CustomerID
);

-- Order မရှိသော customers များ
SELECT c.CustomerID, c.Name
FROM Customers c
WHERE NOT EXISTS (
    SELECT 1 FROM Orders o 
    WHERE o.CustomerID = c.CustomerID
);
```

## Subquery vs JOIN

| Aspect | Subquery | JOIN |
|--------|----------|------|
| Readability | ရိုးရှင်းသော subquery များအတွက်ကောင်း | Complex queries အတွက်ပိုကောင်း |
| Performance | နှေးနိုင် (အထူးသဖြင့် correlated) | များသောအားဖြင့်ပိုမြန် |
| Multiple columns | ခက်ခဲ (correlated မှလွဲ၍) | လွယ်ကူ |
| NULL handling | IN သည် NULL ရှိလျှင်ပြဿနာ | ပြဿနာမရှိ |
| Recommendation | လိုအပ်မှသာသုံးပါ | JOIN ကိုပိုသုံးပါ |

## Subquery နေရာမျိုးစုံတွင်သုံးခြင်း

```sql
-- WHERE clause တွင် IN subquery
SELECT * FROM Products
WHERE CategoryID IN (
    SELECT CategoryID FROM Categories WHERE CategoryName = 'Electronics'
);

-- HAVING clause တွင် subquery
SELECT Department, AVG(Salary) AS AvgSal
FROM Employees
GROUP BY Department
HAVING AVG(Salary) > (SELECT AVG(Salary) FROM Employees);
```

## Subquery Performance Tips

၁။ Subquery ထက် JOIN ကိုပိုသုံးပါ (optimizer ကပိုကောင်းအောင်လုပ်နိုင်)
၂။ IN ထက် EXISTS ကိုသုံးပါ (large dataset အတွက်)
၃။ Correlated subquery ကိုရှောင်ပါ (နှေးသည်)
၄။ Subquery ထဲတွင် WHERE clause ဖြင့်အရင်စစ်ပါ (data လျှော့ချရန်)
၅။ Scalar subquery ကို SELECT clause တွင်သုံးပါက N+1 problem သတိထားရန်

## လေ့ကျင့်ခန်း

၁။ Scalar subquery သုံးပြီး ပျမ်းမျှ product ဈေးထက်များသော products များကိုရှာပါ
၂။ EXISTS သုံးပြီး 2024 ခုနှစ်အတွင်း order ရှိသော customers များကိုရှာပါ
၃။ Correlated subquery သုံးပြီး ဌာနတစ်ခုစီတွင် လစာအနည်းဆုံး employee ကိုရှာပါ
၄။ Subquery ကို FROM clause တွင်သုံးပြီး monthly sales summary ဆောက်ပါ
၅။ Subquery ကို JOIN ဖြင့်ပြန်ရေးပြီး performance ကိုနှိုင်းယှဉ်ပါ

## Subquery သုံးပုံများအသေးစိတ် (Practical Usage Examples)

### လက်တွေ့အသုံးချနမူနာများ

**Example 1: Top 5 Products by Sales Amount**

```sql
SELECT ProductID, ProductName, TotalSales
FROM (
    SELECT 
        p.ProductID, 
        p.ProductName, 
        SUM(oi.Quantity * oi.UnitPrice) AS TotalSales
    FROM Products p
    JOIN OrderItems oi ON p.ProductID = oi.ProductID
    GROUP BY p.ProductID, p.ProductName
) AS ProductSales
ORDER BY TotalSales DESC
LIMIT 5;
```

ဤ query သည် subquery ကို FROM clause တွင် derived table အဖြစ်သုံးပြီး product sales များကိုတွက်ချက်ကာ ထိပ်ဆုံး ၅ ခုကိုပြသပေးပါသည်။

**Example 2: Customers with Above-Average Spend**

```sql
SELECT c.CustomerID, c.Name, c.Email,
       (SELECT SUM(Amount) FROM Orders o WHERE o.CustomerID = c.CustomerID) AS TotalSpent
FROM Customers c
WHERE (
    SELECT SUM(Amount) FROM Orders o WHERE o.CustomerID = c.CustomerID
) > (
    SELECT AVG(CustomerTotal) FROM (
        SELECT SUM(Amount) AS CustomerTotal
        FROM Orders GROUP BY CustomerID
    ) AS AllCustomers
);
```

ဤတွင် subquery ၃ ခုကိုအဆင့်ဆင့်အသုံးပြုထားပါသည် —
- SELECT clause: customer တစ်ယောက်ချင်းစီ၏စုစုပေါင်းအသုံးစရိတ်
- WHERE clause first: customer ၏စုစုပေါင်းကိုစစ်ဆေး
- WHERE clause second: ပျမ်းမျှအသုံးစရိတ်ကိုတွက်ချက်

**Example 3: Using EXISTS for Efficient Filtering**

```sql
-- Active customers who placed orders in the last 30 days
SELECT c.CustomerID, c.Name, c.LastOrderDate
FROM Customers c
WHERE c.Status = 'Active'
  AND EXISTS (
    SELECT 1 FROM Orders o
    WHERE o.CustomerID = c.CustomerID
      AND o.OrderDate >= DATEADD(DAY, -30, GETDATE())
);
```

EXISTS သည် IN ထက်မြန်ပါသည် — subquery ထဲမှာ matching row တစ်ခုတွေ့သည်နှင့် scan ရပ်လိုက်ပါသည်။

### Subquery vs JOIN ဘယ်အချိန်သုံးမလဲ?

**Subquery သုံးသင့်သောအချက်များ**
- Aggregate value (AVG, SUM, MAX) ကိုနှိုင်းယှဉ်ရန်
- EXISTS/NOT EXISTS ဖြင့် data ရှိ/မရှိစစ်ရန်
- SELECT clause တွင် additional calculated field ထည့်ရန်
- IN ဖြင့် list ထဲမှရှာရန် (list သေးလျှင်)

**JOIN သုံးသင့်သောအချက်များ**
- Table များစွာမှ columns များကိုတစ်ပြိုင်နက်ယူရန်
- Large dataset များအတွက် (JOIN ကပိုမြန်)
- Multiple tables မှ data များကိုပေါင်းစပ်ရန်
- Query ရှင်းလင်းစေရန် (JOIN ကိုဖတ်ရလွယ်သည်)

### Nested Subquery များ (အဆင့်ဆင့်)

```sql
-- ပျမ်းမျှထက်ပိုသော ဌာနများမှ လစာအများဆုံး employee
SELECT Name, Department, Salary
FROM Employees
WHERE Salary > (
    SELECT MAX(Salary) FROM Employees WHERE Department IN (
        SELECT Department FROM Employees
        GROUP BY Department
        HAVING AVG(Salary) > (SELECT AVG(Salary) FROM Employees)
    )
);
```

Nested subquery များသည် performance ကိုထိခိုက်နိုင်သောကြောင့် အလွန်အကျွံမသုံးရန်အကြံပြုလိုပါသည်။

### Subquery သုံးရာတွင် သတိထားရမည့်အချက်များ

၁။ Subquery သည် single value ပြန်မည်ဆိုပါက scalar subquery ဖြစ်ရမည် (WHERE col = (subquery) တွင်)
၂။ Subquery သည် multiple values ပြန်ပါက IN, ANY, ALL ကိုသုံးရမည်
၃။ Subquery သည် NULL ပြန်ပါက IN သည် empty result ပြန်ပါသည်
၄။ Correlated subquery သည် row တိုင်းအတွက် execute လုပ်ရသောကြောင့် large table အတွက်နှေးပါသည်
၅။ Subquery ကို ORDER BY သုံးရန် LIMIT/OFFSET နှင့်တွဲသုံးရန် (သို့) window function သုံးရန်

### Subquery Variations by RDBMS

| RDBMS | LIMIT in Subquery | Recursive CTE | LATERAL JOIN |
|-------|------------------|---------------|--------------|
| SQL Server | OFFSET-FETCH | WITH CTE | CROSS/OUTER APPLY |
| PostgreSQL | LIMIT-OFFSET | WITH RECURSIVE | LATERAL |
| MySQL | LIMIT-OFFSET | WITH RECURSIVE | LATERAL (8.0+) |
| Oracle | ROWNUM / OFFSET | CONNECT BY / WITH | LATERAL |



### Subquery vs CTE

CTE သည် subquery ၏ပိုမိုကောင်းမွန်သော alternative တစ်ခုဖြစ်ပါသည်။

**Subquery** — အခြား query အတွင်း၌တန်းထည့်ရေးသားခြင်း
**CTE** — Query ၏အပေါ်ဆုံးတွင် WITH clause ဖြင့်သတ်မှတ်ပြီး အောက်တွင်ပြန်သုံးခြင်း

CTE ၏အားသာချက်များ —
- ပိုမိုရှင်းလင်းသော syntax
- တစ်ကြိမ်သတ်မှတ်ပြီးအကြိမ်များစွာပြန်သုံးနိုင်
- Recursive queries များရေးသားနိုင်

Subquery ၏အားသာချက်များ —
- Inline ရေးသားနိုင် (CTE လောက်ရှည်မနေ)
- Scalar context တွင်သုံးနိုင် (SELECT clause)
- Simple queries များအတွက်ပိုမိုလွယ်ကူ
