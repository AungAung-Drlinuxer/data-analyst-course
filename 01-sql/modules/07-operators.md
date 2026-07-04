# Module 7: Operators

## Operators ဆိုတာဘာလဲ?

Operators များသည် value များကိုတွက်ချက်ရန်၊ နှိုင်းယှဉ်ရန်နှင့်စစ်ဆေးရန်အတွက်အသုံးပြုပါသည်။ SQL တွင် operator အမျိုးမျိုးရှိပြီး ၎င်းတို့ကိုကျွမ်းကျင်စွာအသုံးပြုနိုင်မှသာ complex queries များကိုရေးသားနိုင်မည်ဖြစ်ပါသည်။

### 1. Arithmetic Operators (ဂဏန်းသင်္ချာ)

ကိန်းဂဏန်းများကိုတွက်ချက်ရန်အသုံးပြုပါသည်။

| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| + | ပေါင်းခြင်း | 10 + 3 | 13 |
| - | နှုတ်ခြင်း | 10 - 3 | 7 |
| * | မြှောက်ခြင်း | 10 * 3 | 30 |
| / | စားခြင်း | 10 / 3 | 3 (integer) |
| % | Modulo (အကြွင်း) | 10 % 3 | 1 |

```sql
SELECT 
    Price,
    Price + 10 AS PricePlus10,
    Price * 1.1 AS PriceWithTax,
    Price - Discount AS DiscountedPrice,
    Quantity * Price AS TotalAmount,
    OrderID % 2 AS IsEvenOrder
FROM Orders;
```

**မှတ်ချက်**: Integer division တွင် SQL Server သည် integer ပြန်ပေးပါသည် (10/3 = 3)။ Decimal ရလိုပါက decimal ဖြင့်ရေးရန် (10.0/3 = 3.33)။

### 2. Comparison Operators (နှိုင်းယှဉ်ခြင်း)

တန်ဖိုးနှစ်ခုကိုနှိုင်းယှဉ်ရန်အသုံးပြုပါသည်။

| Operator | Description | Example |
|----------|-------------|---------|
| = | တူညီခြင်း | City = 'Yangon' |
| > | ကြီးခြင်း | Price > 100 |
| < | ငယ်ခြင်း | Price < 50 |
| >= | ကြီးသည် သို့မဟုတ် ညီခြင်း | Age >= 18 |
| <= | ငယ်သည် သို့မဟုတ် ညီခြင်း | Age <= 60 |
| <> သို့မဟုတ် != | မတူညီခြင်း | Status <> 'Cancelled' |
| !< | မငယ်ခြင်း (>=) | Amount !< 100 |
| !> | မကြီးခြင်း (<=) | Amount !> 1000 |

### 3. Logical Operators (ယုတ္တိဆိုင်ရာ)

Condition များစွာကိုပေါင်းစပ်ရန်အသုံးပြုပါသည်။

```sql
-- AND: condition အားလုံးမှန်မှ TRUE
SELECT * FROM Products 
WHERE Category = 'Electronics' 
  AND Price > 100 
  AND StockQuantity > 0;

-- OR: တစ်ခုခုမှန်လျှင် TRUE
SELECT * FROM Products 
WHERE Category = 'Electronics' 
   OR Category = 'Computers';

-- NOT: မဟုတ်လျှင် TRUE
SELECT * FROM Products 
WHERE NOT Category = 'Discontinued';
```

### 4. Special Operators

```sql
-- BETWEEN (range)
SELECT * FROM Products WHERE Price BETWEEN 50 AND 100;

-- IN (list)
SELECT * FROM Customers WHERE City IN ('Yangon', 'Mandalay', 'Naypyidaw');

-- LIKE (pattern)
SELECT * FROM Customers WHERE Name LIKE 'A%';  -- A နဲ့စသော

-- EXISTS (subquery တွင် row ရှိ/မရှိ)
SELECT * FROM Customers c
WHERE EXISTS (
    SELECT 1 FROM Orders o WHERE o.CustomerID = c.CustomerID
);
```

### 5. String Concatenation

```sql
-- SQL Server (+)
SELECT FirstName + ' ' + LastName AS FullName FROM Employees;

-- PostgreSQL / MySQL (||)
SELECT FirstName || ' ' || LastName AS FullName FROM Employees;

-- CONCAT Function (standard, handles NULL)
SELECT CONCAT(FirstName, ' ', LastName) AS FullName FROM Employees;
```

### Operator Precedence

SQL သည် အောက်ပါ precedence အတိုင်း operators များကိုအကဲဖြတ်ပါသည်-

1. Parentheses: ( )
2. Multiplication, Division: *, /
3. Addition, Subtraction: +, -
4. Comparison: =, >, <, >=, <=, <>, !=, !<, !>
5. NOT
6. AND
7. OR

```sql
-- ရှင်းရှင်းလင်းလင်းသိရန် parentheses သုံးပါ
SELECT * FROM Products 
WHERE (Category = 'Electronics' OR Category = 'Computers')
  AND Price > 500;

-- အောက်ပါအတိုင်းရေးပါက AND က OR ထက်ရှေ့အလုပ်လုပ်မည်
SELECT * FROM Products 
WHERE Category = 'Electronics' OR Category = 'Computers' AND Price > 500;
-- ဤသည်မှာ Category = 'Electronics' သို့မဟုတ် (Category = 'Computers' AND Price > 500)
```

## Exercises

1. Products မှ Category 'Electronics' သို့မဟုတ် 'Computers' ဖြစ်ပြီး Price > 1000 ကိုရှာပါ။
2. Employees မှ လစာ 30000 နှင့် 60000 ကြား (BETWEEN) ကိုရှာပါ။
3. Name တွင် 'aung' ပါဝင်သော customers ကိုရှာပါ (case-insensitive)။

## SQL Operators အသေးစိတ် (Complete Guide)

SQL တွင် operator အမျိုးမျိုးရှိပြီး ၎င်းတို့ကိုကျွမ်းကျင်စွာအသုံးပြုနိုင်မှသာ complex queries များကိုရေးသားနိုင်မည်ဖြစ်ပါသည်။

### Arithmetic Operators အသေးစိတ်

ကိန်းဂဏန်းများကိုတွက်ချက်ရန်အသုံးပြုပါသည်။

```sql
SELECT 
    Price,
    Price + 10 AS Plus10,              -- ပေါင်းခြင်း
    Price - 5 AS Minus5,               -- နှုတ်ခြင်း
    Price * 1.1 AS WithTax,            -- မြှောက်ခြင်း (10% tax)
    Price / 2 AS HalfPrice,            -- စားခြင်း
    Price % 2 AS IsEven,               -- အကြွင်း (0=even, 1=odd)
    (Price * Quantity) AS Total         -- Expression ပေါင်းစုံ
FROM Products;
```

### Integer Division ကိုသတိထားရန်

SQL Server တွင် integer နှစ်ခုကိုစားပါက integer ပြန်ပေးပါသည် —
SELECT 10/3 → 3 (3.33 မဟုတ်)
SELECT 10.0/3 → 3.33 (decimal ပြန်ရန်)
SELECT CAST(10 AS DECIMAL)/3 → 3.33

### Comparison Operators အသေးစိတ်

| Operator | Description | Example |
|----------|-------------|---------|
| = | Equal to | Salary = 50000 |
| <> or != | Not equal to | Status <> 'Cancelled' |
| > | Greater than | Price > 100 |
| < | Less than | Age < 18 |
| >= | Greater or equal | Amount >= 1000 |
| <= | Less or equal | Quantity <= 0 |

### Logical Operators အသေးစိတ်

```sql
-- AND (condition အားလုံးမှန်မှ TRUE)
SELECT * FROM Products
WHERE Category = 'Electronics'
  AND Price > 100
  AND StockQuantity > 0;

-- OR (တစ်ခုခုမှန်လျှင် TRUE)
SELECT * FROM Customers
WHERE City = 'Yangon' OR City = 'Mandalay';

-- NOT (မဟုတ်လျှင် TRUE)
SELECT * FROM Products
WHERE NOT Discontinued = 1;

-- AND/OR တွဲသုံးခြင်း (parentheses သုံးရန်)
SELECT * FROM Orders
WHERE (Status = 'Pending' OR Status = 'Processing')
  AND TotalAmount > 1000
  AND OrderDate >= '2024-01-01';
```

### Operator Precedence

SQL သည် operators များကိုအောက်ပါအစဉ်အတိုင်းအကဲဖြတ်ပါသည် —
1. () Parentheses
2. *, / Multiplication, Division
3. +, - Addition, Subtraction
4. =, >, <, >=, <=, <> Comparison
5. NOT
6. AND
7. OR

**အရေးကြီးသည်:** ရှုပ်ထွေးသော condition များတွင် parentheses ကိုအသုံးပြုပါ။

### NULL နှင့် Operators

NULL သည် unknown value ကိုကိုယ်စားပြုပါသည်။ NULL နှင့်တွက်ချက်ပါက result သည် NULL ဖြစ်ပါသည်။

```sql
SELECT NULL + 10   → NULL
SELECT NULL > 100   → NULL (not TRUE, not FALSE)
SELECT NULL = NULL  → NULL (သတိထားရန်!)
SELECT NULL IS NULL → TRUE (IS NULL ကိုသုံးပါ)
```

NULL ကိုစစ်ရန် IS NULL သို့မဟုတ် IS NOT NULL ကိုသာအသုံးပြုပါ။ = NULL သို့မဟုတ် <> NULL ကိုဘယ်တော့မှမသုံးပါနှင့်။

### Advanced Operator Usage

**Set Operators (UNION, INTERSECT, EXCEPT)** —

```sql
-- UNION: Result sets နှစ်ခုကိုပေါင်းစပ် (deduplicate)
SELECT City FROM Customers
UNION
SELECT City FROM Suppliers;

-- UNION ALL: Result sets နှစ်ခုကိုပေါင်းစပ် (keep duplicates)
SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers;

-- INTERSECT: Result sets နှစ်ခုလုံးမှာပါသော values
SELECT City FROM Customers
INTERSECT
SELECT City FROM Suppliers;

-- EXCEPT: ပထမမှာပါပြီးဒုတိယမှာမပါသော values
SELECT City FROM Customers
EXCEPT
SELECT City FROM Suppliers;
```

**ANY / ALL Operators** —

```sql
-- ANY: Subquery ထဲမှတန်ဖိုးတစ်ခုခုထက်ကြီးလျှင်
SELECT * FROM Products
WHERE Price > ANY (SELECT Price FROM Products WHERE Category = 'Electronics');

-- ALL: Subquery ထဲမှတန်ဖိုးအားလုံးထက်ကြီးလျှင်
SELECT * FROM Products
WHERE Price > ALL (SELECT Price FROM Products WHERE Category = 'Electronics');
```

**Operator Precedence Example** — AND က OR ထက်ရှေ့အလုပ်လုပ်ပါသည်-
```sql
SELECT * FROM Products
WHERE Category = 'A' OR Category = 'B' AND Price > 100
-- ဤသည် Category = 'A' OR (Category = 'B' AND Price > 100) ဖြစ်ပါသည်

-- သင်အလိုရှိသည်မှာ (Category = 'A' OR Category = 'B') AND Price > 100 ဆိုပါက
SELECT * FROM Products
WHERE (Category = 'A' OR Category = 'B') AND Price > 100
```

### String Operators

**LIKE Operator Patterns** —
- LIKE 'A%' — A နဲ့စသော string
- LIKE '%A' — A နဲ့ဆုံးသော string
- LIKE '%A%' — A ပါဝင်သော string (အနှေးဆုံး — index မသုံးနိုင်)
- LIKE 'A__' — A နဲ့စပြီး ၃ လုံးရှိသော string
- LIKE '[ABC]%' — A, B, C တစ်ခုခုနဲ့စသော string
- LIKE '[A-C]%' — A မှ C အတွင်းတစ်ခုခုနဲ့စသော string
- LIKE '[^ABC]%' — A, B, C မဟုတ်သောစာလုံးနဲ့စသော string

**Escape Characters** — LIKE တွင် special characters များကိုရှာရန် —
```sql
SELECT * FROM Products WHERE Name LIKE '30%%' ESCAPE '%';  -- 30% ပါဝင်သော
```

### Practical Operator Examples

**Example 1: Find Products in Price Range**
```sql
SELECT ProductName, Price, Category
FROM Products
WHERE (Category = 'Electronics' OR Category = 'Computers')
  AND Price BETWEEN 500 AND 2000
  AND StockQuantity > 0
ORDER BY Price DESC;
```

**Example 2: Complex Customer Search**
```sql
SELECT CustomerID, Name, City, TotalSpent
FROM Customers
WHERE (City IN ('Yangon', 'Mandalay') OR Name LIKE 'Aung%')
  AND TotalSpent > 1000
  AND NOT (Status = 'Inactive')
ORDER BY TotalSpent DESC;
```

Operator များကိုကျွမ်းကျင်စွာအသုံးပြုနိုင်ပါက complex WHERE clauses များကိုရေးသားနိုင်ပြီး data များကိုတိကျစွာစစ်ထုတ်နိုင်ပါသည်။
