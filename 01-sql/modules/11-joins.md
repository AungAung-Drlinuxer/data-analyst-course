# Module 11: JOINS (Table များချိတ်ဆက်ခြင်း)

## JOIN ဆိုတာဘာလဲ?

JOIN သည် table နှစ်ခု (သို့မဟုတ်) ထို့ထက်ပိုသော table များကို ၎င်းတို့၏ related column (များသောအားဖြင့် FK-PK) ဖြင့်ချိတ်ဆက်ပေးပါသည်။ JOIN များသည် relational database ၏အဓိကအင်္ဂါရပ်ဖြစ်ပြီး normalized tables များမှဒေတာများကိုပြန်လည်ပေါင်းစပ်ရန်အသုံးပြုပါသည်။

JOIN အမျိုးအစား ၆ မျိုးရှိပါသည်-

| JOIN Type | Description |
|-----------|-------------|
| INNER JOIN | Table နှစ်ခုလုံးတွင်တူညီသော data များသာ |
| LEFT JOIN | Left table အားလုံး + right table မှတူညီသော data |
| RIGHT JOIN | Right table အားလုံး + left table မှတူညီသော data |
| FULL OUTER JOIN | Table နှစ်ခုလုံးမှ data အားလုံး |
| CROSS JOIN | Cartesian product (combination အားလုံး) |
| SELF JOIN | Table ကိုယ်နှိုက်နှင့်ကိုယ် JOIN |

### Sample Tables များ

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(100),
    City VARCHAR(50)
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT FOREIGN KEY REFERENCES Customers(CustomerID),
    OrderDate DATE,
    Amount DECIMAL(10,2)
);

INSERT INTO Customers VALUES (1, 'Aung', 'Yangon'), (2, 'Mya', 'Mandalay'), (3, 'Hla', 'Naypyidaw');
INSERT INTO Orders VALUES (101, 1, '2024-01-15', 500), (102, 2, '2024-02-20', 300), (103, 5, '2024-03-10', 200);
```

### 1. INNER JOIN

Table နှစ်ခုလုံးတွင် matching rows ရှိမှသာ result ထဲပါဝင်ပါသည်။

```sql
SELECT c.Name, o.OrderID, o.Amount
FROM Customers c
INNER JOIN Orders o ON c.CustomerID = o.CustomerID;

-- Result: Aung (101, 500), Mya (102, 300)
-- Hla (CustomerID 3) နှင့် CustomerID 5 (Order 103) တို့မပါ
```

### 2. LEFT JOIN

Left table (FROM ထဲကပထမ table) မှ rows အားလုံးပါဝင်ပြီး right table မှ matching rows များသာပါဝင်ပါသည်။

```sql
SELECT c.Name, o.OrderID, o.Amount
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID;

-- Result: Aung (101, 500), Mya (102, 300), Hla (NULL, NULL)
-- Hla တွင် order မရှိသော်လည်း left join ကြောင့်ပါဝင်ပါသည်
```

### 3. RIGHT JOIN

Right table မှ rows အားလုံးပါဝင်ပြီး left table မှ matching rows များသာပါဝင်ပါသည်။

```sql
SELECT c.Name, o.OrderID, o.Amount
FROM Customers c
RIGHT JOIN Orders o ON c.CustomerID = o.CustomerID;

-- Result: Aung (101, 500), Mya (102, 300), NULL (103, 200)
-- CustomerID 5 (orders တွင်ပါသော်လည်း customers တွင်မရှိ) အတွက် NULL ပြမည်
```

### 4. FULL OUTER JOIN

Table နှစ်ခုလုံးမှ rows အားလုံးပါဝင်ပါသည်။ မတူညီသော sides များအတွက် NULL များဖြည့်ပေးပါသည်။

```sql
SELECT c.Name, o.OrderID, o.Amount
FROM Customers c
FULL OUTER JOIN Orders o ON c.CustomerID = o.CustomerID;

-- Result: Aung (101, 500), Mya (102, 300), Hla (NULL, NULL), NULL (103, 200)
```

### 5. CROSS JOIN

Table နှစ်ခုမှ rows အားလုံးကို combination လုပ်ပါသည် (Cartesian product)။

```sql
SELECT c.Name, p.ProductName
FROM Customers c
CROSS JOIN Products p;
-- Row အရေအတွက် = Customers အရေအတွက် x Products အရေအတွက်
```

### 6. SELF JOIN

Table တစ်ခုကိုယ်၎င်းနှင့် JOIN လုပ်ခြင်း (alias များသုံးရန်)။

```sql
-- Employee-Manager hierarchy
SELECT 
    e.Name AS Employee,
    m.Name AS Manager
FROM Employees e
LEFT JOIN Employees m ON e.ManagerID = m.EmployeeID;
```

### Multiple JOINs

```sql
SELECT 
    o.OrderID,
    c.Name AS Customer,
    p.ProductName,
    oi.Quantity,
    oi.UnitPrice,
    oi.Quantity * oi.UnitPrice AS LineTotal
FROM Orders o
INNER JOIN Customers c ON o.CustomerID = c.CustomerID
INNER JOIN OrderItems oi ON o.OrderID = oi.OrderID
INNER JOIN Products p ON oi.ProductID = p.ProductID
WHERE o.OrderDate >= '2024-01-01'
ORDER BY o.OrderID;
```

### JOIN Performance Tips

1. **Index FK columns များတွင် Index ထားပါ** — JOIN performance အတွက်အရေးကြီးဆုံး
2. **Small table ကိုရှေ့ထားပါ** — Query optimizer ကစီမံပေးသော်လည်းအလေ့အကျင့်ကောင်း
3. **WHERE clause ဖြင့်အရင်စစ်ပါ** — JOIN မလုပ်မီ rows များကိုလျှော့ချနိုင်
4. **SELECT * ကိုရှောင်ပါ** — လိုအပ်သော columns များကိုသာရွေးပါ

## Exercises

1. Customers နှင့် Orders table များကို INNER JOIN လုပ်ပြီး customer အမည်နှင့် order ပမာဏကိုထုတ်ပါ။
2. LEFT JOIN သုံးပြီး order မရှိသော customers များကိုရှာပါ။
3. Orders, OrderItems, Products ၃ ခုကို JOIN လုပ်ပြီး order detail report ထုတ်ပါ။

## JOIN Types အသေးစိတ် (Complete JOIN Reference)

JOIN သည် relational database ၏အဓိကအင်္ဂါရပ်ဖြစ်ပြီး normalized tables များမှ data များကိုပြန်လည်ပေါင်းစပ်ရန်အသုံးပြုပါသည်။

### JOIN အမျိုးအစားတစ်ခုချင်းစီ၏အသေးစိတ်ရှင်းလင်းချက်

**INNER JOIN** — Table နှစ်ခုလုံးတွင် matching rows ရှိမှသာ result ထဲပါဝင်ပါသည်။ အသုံးအများဆုံး JOIN type ဖြစ်ပါသည်။

**LEFT JOIN** — Left table (FROM ထဲကပထမ table) မှ rows အားလုံးပါဝင်ပြီး right table မှ matching rows များသာပါဝင်ပါသည်။ Right table တွင် match မရှိပါက NULL များဖြည့်ပေးပါသည်။

**RIGHT JOIN** — Right table မှ rows အားလုံးပါဝင်ပြီး left table မှ matching rows များသာပါဝင်ပါသည်။ LEFT JOIN ၏ပြောင်းပြန်ဖြစ်ပါသည်။

**FULL OUTER JOIN** — Table နှစ်ခုလုံးမှ rows အားလုံးပါဝင်ပါသည်။ မတူညီသော sides များအတွက် NULL များဖြည့်ပေးပါသည်။

**CROSS JOIN** — Table နှစ်ခုမှ rows အားလုံးကို combination လုပ်ပါသည် (Cartesian product)။ Row အရေအတွက် = Table A rows x Table B rows။

**SELF JOIN** — Table တစ်ခုကိုယ်၎င်းနှင့် JOIN လုပ်ခြင်း။ Alias များသုံးရန် လိုအပ်ပါသည်။

### JOIN နားလည်ရန် Venn Diagram ရှင်းလင်းချက်

INNER JOIN = Circle နှစ်ခု၏ထပ်နေသောအပိုင်း
LEFT JOIN = Left circle တစ်ခုလုံး + ထပ်နေသောအပိုင်း
RIGHT JOIN = Right circle တစ်ခုလုံး + ထပ်နေသောအပိုင်း
FULL JOIN = Circle နှစ်ခုလုံး၏အပြင်ဘက်အစွန်းအထိ (ထပ်သည်မထပ်သည်အားလုံး)
CROSS JOIN = Circle နှစ်ခုလုံးမှ point အားလုံးကိုတွဲခြင်း

### Multiple JOINs သုံးပုံ

```sql
SELECT 
    o.OrderID,
    c.Name AS CustomerName,
    p.ProductName,
    oi.Quantity,
    oi.UnitPrice,
    oi.Quantity * oi.UnitPrice AS LineTotal
FROM Orders o
INNER JOIN Customers c ON o.CustomerID = c.CustomerID
INNER JOIN OrderItems oi ON o.OrderID = oi.OrderID
INNER JOIN Products p ON oi.ProductID = p.ProductID
WHERE o.OrderDate >= '2024-01-01'
ORDER BY o.OrderID, p.ProductName;
```

ဤ query သည် order တစ်ခုချင်းစီအတွက် customer အမည်၊ product အမည်၊ ပမာဏနှင့်စုစုပေါင်းတန်ဖိုးကိုပြသပေးပါသည်။

### JOIN Performance Optimization

၁။ **Index FK columns** — JOIN column များတွင် index ရှိရန် အလွန်အရေးကြီးပါသည်
၂။ **Join order** — Small table ကိုရှေ့ထားပါ (သို့သော် query optimizer ကစီမံပေးပါသည်)
၃။ **Filter early** — JOIN မလုပ်မီ WHERE ဖြင့် data ကိုလျှော့ချပါ
၄။ **Select columns** — SELECT * အစားလိုအပ်သော columns များကိုသာရွေးပါ
၅။ **Avoid functions in JOIN** — JOIN ON Column = Column (function မပါ) ဖြစ်ရန်

### JOIN vs Subquery Performance

များသောအားဖြင့် JOIN သည် subquery ထက်ပိုမြန်ပါသည် (query optimizer က JOIN ကိုပိုကောင်းအောင် optimize လုပ်နိုင်သောကြောင့်)။ သို့သော် correlated subquery (EXISTS) သည် JOIN နှင့်တူညီသော performance ရှိတတ်ပါသည်။

### Exercises

၁။ Customers နှင့် Orders table များကို LEFT JOIN လုပ်ပြီး order မရှိသော customers များကိုရှာပါ
၂။ Orders, OrderItems, Products ၃ခုကို JOIN လုပ်ပြီး order detail report ထုတ်ပါ
၃။ SELF JOIN သုံးပြီး employee-manager hierarchy ကိုပြပါ
၄။ FULL OUTER JOIN သုံးပြီး customers နှင့် orders နှစ်ခုလုံးမှ data အားလုံးကိုပြပါ



### JOIN Optimization Tips

**Index Strategy for JOINs** — JOIN column များတွင် index ရှိရန်အလွန်အရေးကြီးပါသည်။ FK columns များတွင်အလိုအလျောက် index မတက်ပါ။

**Query Plan Analysis** — JOIN query ၏ execution plan ကိုကြည့်ရန် SET SHOWPLAN_XML ON သုံးပါ။ Nested Loop, Hash Match, Merge Join စသည့် join types များကိုလေ့လာပါ။

**Join Types Performance** — INNER JOIN သည် fastest ဖြစ်ပြီး FULL OUTER JOIN သည် slowest ဖြစ်ပါသည်။ LEFT JOIN ကို INNER JOIN ဖြင့်အစားထိုးနိုင်လျှင်ပိုကောင်းပါသည်။

**Practical Tip** — Large tables များကို JOIN မလုပ်မီ WHERE clause ဖြင့် data ကိုလျှော့ချပါ။

### JOINs with Multiple Tables

**4-Table JOIN Example** — Customer, Order, OrderItem, Product

```sql
SELECT 
    c.Name AS Customer,
    o.OrderID,
    o.OrderDate,
    p.ProductName,
    oi.Quantity,
    oi.UnitPrice,
    oi.Quantity * oi.UnitPrice AS LineTotal
FROM Customers c
INNER JOIN Orders o ON c.CustomerID = o.CustomerID
INNER JOIN OrderItems oi ON o.OrderID = oi.OrderID
INNER JOIN Products p ON oi.ProductID = p.ProductID
WHERE o.OrderDate >= '2024-01-01'
ORDER BY o.OrderDate, c.Name;
```

**LEFT JOIN to Find Missing Data** — Customer တွင် order မရှိသူများကိုရှာရန်

```sql
SELECT c.Name, c.Email
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
WHERE o.OrderID IS NULL
-- Customers without any orders
```

**SELF JOIN for Hierarchical Data** — Employee-Manager relationship

```sql
SELECT 
    e.Name AS Employee,
    m.Name AS Manager
FROM Employees e
LEFT JOIN Employees m ON e.ManagerID = m.EmployeeID
ORDER BY m.Name, e.Name;
```

SELF JOIN ကို organizational chart, category tree, bill of materials စသည့် hierarchical data များအတွက်အသုံးပြုပါသည်။
