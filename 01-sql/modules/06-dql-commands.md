# Module 6: DQL Commands (Data Query Language)

## DQL Commands ဆိုတာဘာလဲ?

DQL (Data Query Language) သည် database ထဲမှ data များကိုရှာဖွေထုတ်ယူရန်အသုံးပြုသော SQL command များဖြစ်ပါသည်။ အဓိက command မှာ SELECT ဖြစ်ပြီး ၎င်းသည် SQL တွင် အသုံးအများဆုံး command လည်းဖြစ်ပါသည်။

SELECT statement သည် table များမှ data များကိုရှာဖွေရန်၊ စစ်ထုတ်ရန်၊ စီရန်နှင့်အုပ်စုဖွဲ့ရန်အတွက်အသုံးပြုပါသည်။ ၎င်းသည် database မှ data ကိုပြန်လည်ရယူခြင်း (retrieve) အတွက်အဓိက tool ဖြစ်ပါသည်။

### SELECT Statement Syntax

```sql
SELECT column1, column2, ...  -- လိုချင်သော columns
FROM table_name               -- data ရှိရာ table
WHERE condition               -- row စစ်ထုတ်ရန် (optional)
GROUP BY column               -- အုပ်စုဖွဲ့ရန် (optional)
HAVING condition              -- group စစ်ထုတ်ရန် (optional)
ORDER BY column               -- စီရန် (optional);
```

SELECT statement ၏ clause များကို ဤအစီအစဉ်အတိုင်းရေးရပါမည်။ SQL engine သည် ဤ order အတိုင်း execute လုပ်ပါသည် (FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY)။

### Basic SELECT Examples

```sql
-- Column အားလုံးကိုရွေးချယ်ခြင်း
SELECT * FROM Customers;

-- Column အချို့ကိုရွေးချယ်ခြင်း
SELECT CustomerID, Name, Email FROM Customers;

-- Calculated column (expression)
SELECT ProductName, Price, Price * 1.1 AS PriceWithTax FROM Products;

-- Column alias (နာမည်ပြောင်)
SELECT 
    Name AS CustomerName, 
    Email AS ContactEmail,
    GETDATE() AS ReportDate
FROM Customers;
```

### WHERE Clause (row စစ်ထုတ်ခြင်း)

WHERE clause သည် သတ်မှတ်ချက်နှင့်ကိုက်ညီသော rows များကိုသာပြန်ပေးပါသည်။

```sql
-- တိကျသောတန်ဖိုးဖြင့်ရှာခြင်း
SELECT * FROM Products WHERE Price = 99.99;

-- နှိုင်းယှဉ်ခြင်း
SELECT * FROM Products WHERE Price > 50;
SELECT * FROM Products WHERE Price >= 50 AND Price <= 100;
SELECT * FROM Products WHERE Price BETWEEN 50 AND 100;  -- same as above

-- List ထဲမှရှာခြင်း (IN)
SELECT * FROM Customers WHERE City IN ('Yangon', 'Mandalay', 'Naypyidaw');

-- Pattern ဖြင့်ရှာခြင်း (LIKE)
SELECT * FROM Customers WHERE Name LIKE 'Aung%';     -- Aung နဲ့စသော
SELECT * FROM Customers WHERE Name LIKE '%Win';      -- Win နဲ့ဆုံးသော
SELECT * FROM Customers WHERE Name LIKE '%Myo%';     -- Myo ပါဝင်သော
SELECT * FROM Customers WHERE Email LIKE '%@gmail.com'; -- Gmail users

-- NULL တန်ဖိုးစစ်ခြင်း
SELECT * FROM Customers WHERE Email IS NULL;          -- Email မရှိသူများ
SELECT * FROM Customers WHERE Email IS NOT NULL;      -- Email ရှိသူများ

-- Multiple conditions (AND, OR, NOT)
SELECT * FROM Orders 
WHERE Status = 'Shipped' 
  AND TotalAmount > 1000 
  AND OrderDate >= '2024-01-01';
```

### DISTINCT (duplicate များကိုဖယ်ရှားခြင်း)

```sql
-- Unique city များကိုသာကြည့်ရှုခြင်း
SELECT DISTINCT City FROM Customers;

-- Column ပေါင်းများစွာအတွက် DISTINCT
SELECT DISTINCT City, Country FROM Customers;
-- City နှင့် Country ပေါင်းစပ်မှုတစ်မျိုးစီသာပြမည်

-- Count unique values
SELECT COUNT(DISTINCT City) AS UniqueCities FROM Customers;
```

### SELECT TOP / LIMIT

```sql
-- SQL Server (TOP)
SELECT TOP 10 * FROM Products ORDER BY Price DESC;
SELECT TOP 10 PERCENT * FROM Products ORDER BY Price DESC;

-- PostgreSQL / MySQL (LIMIT)
SELECT * FROM Products ORDER BY Price DESC LIMIT 10;
SELECT * FROM Products ORDER BY Price DESC LIMIT 10 OFFSET 20; -- page 3
```

### SELECT Execution Order

SQL query များကိုအောက်ပါ order အတိုင်း execute လုပ်ပါသည်-

1. **FROM** — table ကိုရွေးချယ်ခြင်း
2. **WHERE** — row များကိုစစ်ထုတ်ခြင်း
3. **GROUP BY** — rows များကိုအုပ်စုဖွဲ့ခြင်း
4. **HAVING** — groups များကိုစစ်ထုတ်ခြင်း
5. **SELECT** — columns များကိုရွေးချယ်ခြင်း
6. **ORDER BY** — result ကိုစီခြင်း
7. **LIMIT/OFFSET** — ရလဒ်ကိုကန့်သတ်ခြင်း

ဤ order ကိုနားလည်ပါက WHERE vs HAVING ကွာခြားချက်ကိုရှင်းရှင်းလင်းလင်းသိမြင်နိုင်ပါသည်။

### WHERE Clause Performance Tips

1. **Indexed columns ကိုသုံးပါ** — WHERE clause တွင် indexed column များကိုသုံးပါက query ပိုမြန်ပါသည်။
2. **SARGable expressions ရေးပါ** — WHERE YEAR(Date) = 2024 ထက် WHERE Date >= '2024-01-01' AND Date < '2025-01-01' ကပိုမြန်ပါသည်။
3. **LIKE ကိုသတိသုံးပါ** — LIKE '%keyword' နှင့် LIKE '%key%' သည် index ကိုမသုံးနိုင်ပါ။ LIKE 'keyword%' ကမူ index သုံးနိုင်ပါသည်။
4. **Functions in WHERE ကိုရှောင်ပါ** — WHERE UPPER(Name) = 'AUNG' ထက် WHERE Name = 'Aung' ကပိုမြန်ပါသည်။

## Exercises

1. Customers table မှ Yangon မြို့မှ customers အားလုံးကိုရှာပါ။
2. Products table မှ price 100 နှင့် 500 ကြားရှိသော products များကိုရှာပါ။
3. Orders table မှ 2024 ခုနှစ်အတွင်း status 'Shipped' ဖြစ်သော orders များကိုရှာပါ။
4. Customers မှ unique cities စာရင်းကိုထုတ်ပါ။
5. Products မှ ဈေးအကြီးဆုံး 5 မျိုးကိုပြပါ။

## SELECT Statement အသေးစိတ် (Advanced Query Techniques)

SELECT statement သည် SQL တွင်အသုံးအများဆုံး command ဖြစ်ပြီး data များကိုရှာဖွေရန်၊ စစ်ထုတ်ရန်၊ စီရန်နှင့်အုပ်စုဖွဲ့ရန်အတွက်အသုံးပြုပါသည်။

### SELECT ၏ Execution Order

SQL query တစ်ခုကို execute လုပ်သည့်အခါ အောက်ပါ order အတိုင်းလုပ်ဆောင်ပါသည် —
၁။ FROM — data ရှိရာ table ကိုရွေးချယ်ခြင်း
၂။ WHERE — rows များကိုစစ်ထုတ်ခြင်း
၃။ GROUP BY — rows များကိုအုပ်စုဖွဲ့ခြင်း
၄။ HAVING — groups များကိုစစ်ထုတ်ခြင်း
၅။ SELECT — columns များကိုရွေးချယ်ခြင်း
၆။ ORDER BY — result ကိုစီခြင်း
၇။ LIMIT/OFFSET — ရလဒ်ကိုကန့်သတ်ခြင်း

ဤ order ကိုနားလည်ပါက WHERE vs HAVING ကွာခြားချက်ကိုရှင်းရှင်းလင်းလင်းသိမြင်နိုင်ပါသည်။

### WHERE Clause မှာ အသုံးများသော Operators များ

```sql
-- Comparison Operators
WHERE Price = 100       -- တူညီခြင်း
WHERE Price <> 100      -- မတူညီခြင်း
WHERE Price > 100       -- ကြီးခြင်း
WHERE Price >= 100      -- ကြီးသည် သို့မဟုတ် ညီခြင်း

-- Logical Operators
WHERE A > 1 AND B < 5   -- AND: နှစ်ခုလုံးမှန်မှ
WHERE A > 1 OR B < 5    -- OR: တစ်ခုခုမှန်လျှင်
WHERE NOT A > 1         -- NOT: မဟုတ်လျှင်

-- Special Operators
WHERE Price BETWEEN 50 AND 100     -- Range
WHERE City IN ('A','B','C')         -- List
WHERE Name LIKE 'Aung%'             -- Pattern
WHERE Email IS NULL                  -- NULL check
```

### SARGable Queries (Performance အတွက်)

SARG (Search ARGumentable) ဆိုသည်မှာ index ကိုထိထိရောက်ရောက်အသုံးပြုနိုင်သော query ဖြစ်ပါသည်။

**SARGable (Index သုံးနိုင်) — ကောင်းသည်**
```sql
WHERE Date >= '2024-01-01' AND Date < '2025-01-01'
WHERE Price > 1000
WHERE Name = 'Aung'
WHERE Name LIKE 'Aung%'  -- prefix search က index သုံးနိုင်
```

**Non-SARGable (Index မသုံးနိုင်) — ရှောင်ရန်**
```sql
WHERE YEAR(Date) = 2024           -- function in WHERE
WHERE Price * 1.1 > 1000          -- expression in WHERE
WHERE Name LIKE '%Aung'           -- suffix search
WHERE Name LIKE '%Aung%'          -- contains search
WHERE CONVERT(VARCHAR, Date, 103) = '01/01/2024'  -- conversion
```

### Practical Query Examples

```sql
-- Find top 5 most expensive products
SELECT TOP 5 ProductName, Price
FROM Products
WHERE Discontinued = 0
ORDER BY Price DESC;

-- Find customers in specific cities with orders over 1000
SELECT c.CustomerID, c.Name, c.City, o.OrderID, o.TotalAmount
FROM Customers c
INNER JOIN Orders o ON c.CustomerID = o.CustomerID
WHERE c.City IN ('Yangon', 'Mandalay')
  AND o.TotalAmount > 1000
  AND o.OrderDate >= '2024-01-01'
ORDER BY o.TotalAmount DESC;
```

### Advanced SELECT Techniques

**SELECT with PIVOT** — Rows များကို columns အဖြစ်ပြောင်းရန် —

```sql
SELECT * FROM (
    SELECT YEAR(OrderDate) AS Year, Category, Amount
    FROM Orders o JOIN Products p ON o.ProductID = p.ProductID
) AS Source
PIVOT (
    SUM(Amount) FOR Category IN ([Electronics], [Clothing], [Food])
) AS PivotTable;
```

**SELECT with OFFSET-FETCH Pagination** —

```sql
DECLARE @Page INT = 3, @PageSize INT = 20;
SELECT * FROM Products
ORDER BY ProductID
OFFSET (@Page - 1) * @PageSize ROWS
FETCH NEXT @PageSize ROWS ONLY;
```

**Dynamic SELECT** — Column names များကို dynamic ပြောင်းနိုင်ရန် —

```sql
DECLARE @Columns NVARCHAR(MAX) = 'ProductID, ProductName, Price';
DECLARE @SQL NVARCHAR(MAX) = 'SELECT ' + @Columns + ' FROM Products';
EXEC sp_executesql @SQL;
```

သတိထားရန် — Dynamic SQL သည် SQL injection အတွက်အန္တရာယ်ရှိပါသည်။ User input ကိုတိုက်ရိုက် concatenate မလုပ်ပါနှင့်။

### NULL Handling in SELECT

NULL သည် unknown value ကိုကိုယ်စားပြုပြီး data မရှိခြင်းကိုဆိုလိုပါသည်။ NULL နှင့်ပတ်သက်သောအရေးကြီးအချက်များ —

- NULL = NULL သည် FALSE (သို့မဟုတ် UNKNOWN) ဖြစ်ပါသည် (IS NULL ကိုသုံးပါ)
- NULL <> NULL သည် FALSE ဖြစ်ပါသည်
- NULL + 10 သည် NULL ဖြစ်ပါသည်
- Aggregate functions (SUM, AVG) သည် NULL ကိုထည့်မတွက်ပါ
- COUNT(*) သည် NULL rows များကိုပါထည့်တွက်ပါသည်

```sql
-- NULL handling functions
SELECT ISNULL(Column, 'Default') FROM Table;  -- SQL Server
SELECT COALESCE(Col1, Col2, Col3, 'Default') FROM Table;  -- ANSI standard
SELECT NULLIF(Col1, Col2) FROM Table;  -- Equal → NULL
```
