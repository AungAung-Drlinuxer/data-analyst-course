# Module 3: Table ဖန်တီးခြင်း (Creating Table)

## Table ဆိုတာဘာလဲ?

Table ဆိုသည်မှာ Rows (အတန်းများ) နှင့် Columns (ဒေါင်လိုက်များ) ပုံစံဖြင့် data များကိုသိမ်းဆည်းသော database object တစ်ခုဖြစ်ပါသည်။ Spreadsheet (Excel) နှင့်ဆင်တူပြီး data တစ်ခုချင်းစီအတွက် row တစ်ခုစီနှင့် data အမျိုးအစားတစ်ခုစီအတွက် column တစ်ခုစီပါဝင်ပါသည်။

Table တစ်ခုတွင် အောက်ပါအစိတ်အပိုင်းများပါဝင်ပါသည်-

- **Columns**: Data အမျိုးအစားတစ်ခုစီအတွက် (ဥပမာ - Name, Age, Email)
- **Rows**: Record တစ်ခုချင်းစီ (ဥပမာ - လူတစ်ယောက်ချင်းစီ၏ အချက်အလက်များ)
- **Constraints**: Data validity အတွက်စည်းမျဉ်းများ
- **Indexes**: Data search မြန်ဆန်စေရန်

## Column Data Types အသေးစိတ်

Column တစ်ခုစီအတွက် သင့်တော်သော data type ကိုရွေးချယ်ရန်လိုအပ်ပါသည်-

### String Types
| Type | Description | Storage | Max Size |
|------|-------------|---------|----------|
| CHAR(n) | Fixed-length (space ဖြည့်ပေးသည်) | n bytes | 8000 |
| VARCHAR(n) | Variable-length (နေရာချွေတာသည်) | Actual + 2 bytes | 8000 |
| VARCHAR(MAX) | Very large text | 2GB | Unlimited |
| NVARCHAR(n) | Unicode (မြန်မာလိုသိမ်းရန်) | Actual*2 + 2 | 4000 |
| TEXT (deprecated) | Large text | 2GB | Legacy |

### Numeric Types
| Type | Range | Storage |
|------|-------|---------|
| TINYINT | 0 to 255 | 1 byte |
| SMALLINT | -32,768 to 32,767 | 2 bytes |
| INT | -2.1B to 2.1B | 4 bytes |
| BIGINT | -9.2Q to 9.2Q | 8 bytes |
| DECIMAL(p,s) | Precise decimal | 5-17 bytes |
| FLOAT | Approximate | 4/8 bytes |
| MONEY | Currency | 8 bytes |

### Date/Time Types
| Type | Description | Format |
|------|-------------|--------|
| DATE | Date only | YYYY-MM-DD |
| TIME | Time only | HH:MM:SS.nnnnnnn |
| DATETIME | Date + Time (3.33ms accuracy) | YYYY-MM-DD HH:MM:SS.nnn |
| DATETIME2 | More precise (100ns accuracy) | YYYY-MM-DD HH:MM:SS.nnnnnnn |
| SMALLDATETIME | Smaller range (1 min accuracy) | YYYY-MM-DD HH:MM:SS |

## CREATE TABLE Statement - အသေးစိတ်

```sql
-- Basic syntax
CREATE TABLE table_name (
    column1 data_type constraint,
    column2 data_type constraint,
    ...
    table_constraints
);
```

### လက်တွေ့နမူနာ - Customer Table

```sql
CREATE TABLE Customers (
    CustomerID INT IDENTITY(1,1) PRIMARY KEY,
    FirstName NVARCHAR(50) NOT NULL,
    LastName NVARCHAR(50) NOT NULL,
    Email VARCHAR(150) NOT NULL UNIQUE,
    Phone VARCHAR(20) NULL,
    Address NVARCHAR(200) NULL,
    City NVARCHAR(50) NULL DEFAULT 'Yangon',
    BirthDate DATE NULL,
    IsActive BIT NOT NULL DEFAULT 1,
    CreatedDate DATETIME NOT NULL DEFAULT GETDATE(),
    CONSTRAINT CK_Customer_Email CHECK (Email LIKE '%_@__%.__%')
);
```

### ရှင်းလင်းချက်
- **IDENTITY(1,1)**: Identity column (auto-increment) ဖြစ်ပြီး 1 မှစပြီး 1 တိုးတိုင်းသွားပါမည်။
- **NVARCHAR(50)**: Unicode string (မြန်မာလိုထည့်နိုင်) ။
- **NOT NULL**: ဤ column သည် empty မဖြစ်ရပါ။
- **UNIQUE**: Email တန်ဖိုးများထပ်မရပါ။
- **DEFAULT**: Default value သတ်မှတ်ခြင်း။
- **CHECK**: Email format ကိုစစ်ဆေးခြင်း။

## Temporary Tables

Temporary tables များသည် session အတွင်းသာတည်ရှိပြီး အလိုအလျောက်ဖျက်ပစ်ပါသည်။

### Local Temp Table (#)
```sql
-- Local temp table (current session အတွက်သာ)
CREATE TABLE #TempSales (
    SaleID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    SaleDate DATE,
    Amount DECIMAL(10,2)
);

-- Use it like a normal table
INSERT INTO #TempSales VALUES (1, 'Laptop', '2024-01-15', 1200.00);
SELECT * FROM #TempSales;
```

### Global Temp Table (##)
```sql
-- Global temp table (all sessions မှမြင်ရ)
CREATE TABLE ##GlobalTemp (
    ID INT,
    Info VARCHAR(100)
);
```

### Table Variable
```sql
DECLARE @ProductTable TABLE (
    ProductID INT,
    ProductName VARCHAR(100),
    Price DECIMAL(10,2)
);
```

## လက်တွေ့ကျင့်ခန်း

1. 'Products' table ကိုအောက်ပါ columns များဖြင့်ဆောက်ပါ-
   - ProductID (INT, PRIMARY KEY, IDENTITY)
   - ProductName (NVARCHAR(100), NOT NULL)
   - CategoryID (INT, NOT NULL)
   - Price (DECIMAL(10,2), CHECK Price > 0)
   - StockQuantity (INT, DEFAULT 0)
   - CreatedDate (DATETIME, DEFAULT GETDATE())

2. 'Orders' table ကိုဆောက်ပါ - OrderID, CustomerID, OrderDate, TotalAmount, Status

3. #TempOrders ဆိုသော temporary table ဆောက်ပြီး data ထည့်ကြည့်ပါ။

## Table Design အသေးစိတ် (Advanced Table Design Concepts)

Table တစ်ခုကိုကောင်းမွန်စွာဒီဇိုင်းဆွဲခြင်းသည် database ၏ performance နှင့် data integrity ကိုများစွာအကျိုးသက်ရောက်ပါသည်။

### Column Selection Guide (Column ရွေးချယ်ခြင်းလမ်းညွှန်)

သင့်တော်သော data type ကိုရွေးချယ်ခြင်းသည် storage space ကိုချွေတာရုံသာမက performance ကိုလည်းမြှင့်တင်ပေးပါသည်။

**Numeric Data:** Age, Count → TINYINT / SMALLINT။ ID, quantity → INT (အသုံးအများဆုံး)။ Price, salary → DECIMAL(10,2) (တိကျရန်)။

**Text Data:** Short fixed text → CHAR(2)। Variable text → VARCHAR(100)။ Unicode text (မြန်မာ, ဂျပန်) → NVARCHAR။ Long text → VARCHAR(MAX)။

**Date/Time Data:** Date only → DATE (3 bytes)။ Date + time → DATETIME2 (6-8 bytes)။ Timestamp → DATETIMEOFFSET။

### Column Size Estimation Guide

VARCHAR(n) — n = maximum expected length + buffer
- Name: VARCHAR(100) — မြန်မာအမည်အရှည်ဆုံး ~50 လုံး
- Email: VARCHAR(150) — အရှည်ဆုံး email ~100 လုံး
- Address: VARCHAR(200) — လိပ်စာအပြည့်အစုံ
- Phone: VARCHAR(20) — +95-9-123456789

### IDENTITY Column အသေးစိတ်

IDENTITY column သည် auto-increment column ဖြစ်ပြီး row အသစ်တစ်ခုထည့်တိုင်းတန်ဖိုးအလိုအလျောက်တိုးသွားပါသည်။

```sql
CREATE TABLE Orders (
    OrderID INT IDENTITY(1,1) PRIMARY KEY,
    OrderDate DATETIME DEFAULT GETDATE()
);
-- IDENTITY(seed=1, increment=1) — 1 မှစပြီး 1 တိုးတိုင်းသွားမည်

SELECT IDENT_CURRENT('Orders') AS CurrentIdentity;
SELECT @@IDENTITY AS LastInsertedID;
SELECT SCOPE_IDENTITY() AS LastIDInScope;
```

### Computed Columns (တွက်ချက်ထားသော Column များ)

Computed column သည် အခြား column များမှတန်ဖိုးကိုအလိုအလျောက်တွက်ချက်ပေးပါသည်။

```sql
CREATE TABLE OrderItems (
    OrderItemID INT PRIMARY KEY,
    Quantity INT NOT NULL,
    UnitPrice DECIMAL(10,2) NOT NULL,
    Discount DECIMAL(10,2) DEFAULT 0,
    LineTotal AS (Quantity * UnitPrice * (1 - Discount)) PERSISTED
);
-- PERSISTED ဆိုလျှင် disk တွင်သိမ်းပေးမည် (index ထားနိုင်)
```

### Table Constraints အသေးစိတ်

PRIMARY KEY — Table တစ်ခုလျှင်တစ်ခုသာရှိနိုင်။ Automatically creates clustered index။ Column သည် UNIQUE + NOT NULL ဖြစ်ရမည်။

FOREIGN KEY — Table နှစ်ခုကိုချိတ်ဆက်ရန်။ Referential Integrity ကိုထိန်းသိမ်းရန်။ ON DELETE CASCADE / SET NULL / SET DEFAULT သုံးနိုင်။

UNIQUE CONSTRAINT — Column values များထပ်မရ။ NULL တစ်ခုခွင့်ပြုပါသည်။ Table တစ်ခုလျှင်အများအပြားရှိနိုင်။

CHECK CONSTRAINT — Column values များကို validation လုပ်ရန်။ ဥပမာ — Price > 0, Age BETWEEN 0 AND 150။

### လက်တွေ့ဥပမာ — Full E-Commerce Table

```sql
CREATE TABLE Products (
    ProductID INT IDENTITY(1001,1) PRIMARY KEY,
    ProductName NVARCHAR(200) NOT NULL,
    CategoryID INT NOT NULL REFERENCES Categories(CategoryID),
    UnitPrice DECIMAL(10,2) NOT NULL CHECK (UnitPrice > 0),
    UnitsInStock INT NOT NULL DEFAULT 0,
    Discontinued BIT NOT NULL DEFAULT 0,
    CreatedDate DATETIME NOT NULL DEFAULT GETDATE(),
    StockValue AS (UnitsInStock * UnitPrice) PERSISTED
);
```

### Advanced Table Features

**Table Compression** — Large tables များအတွက် data compression သုံးနိုင်ပါသည်။ Row compression နှင့် Page compression ဟူ၍နှစ်မျိုးရှိပါသည်။ Page compression က storage ကိုပိုချွေတာပါသည်။

**Partitioned Tables** — Very large tables များကို partition ခွဲနိုင်ပါသည်။ ဥပမာ — sales data ကို month အလိုက် partition ခွဲပါက query performance ကောင်းပြီး management လည်းလွယ်ကူပါသည်။

**Temporal Tables** (SQL Server 2016+) — Table ၏ data change history ကိုအလိုအလျောက်သိမ်းပေးပါသည်။

```sql
CREATE TABLE Employees (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(100),
    Salary DECIMAL(10,2),
    ValidFrom DATETIME2 GENERATED ALWAYS AS ROW START,
    ValidTo DATETIME2 GENERATED ALWAYS AS ROW END,
    PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
) WITH (SYSTEM_VERSIONING = ON);
```

Temporal table သည် data ပြောင်းလဲမှုမှတ်တမ်းကိုအလိုအလျောက်သိမ်းဆည်းပေးပြီး history ကိုပြန်ကြည့်နိုင်ပါသည်။

### Data Modeling with Tables

Table တစ်ခုကိုဒီဇိုင်းဆွဲရာတွင် normalization ကိုလိုက်နာရန်အရေးကြီးပါသည်။ Normalization ဆိုသည်မှာ data redundancy ကိုလျှော့ချပြီး data integrity ကိုမြှင့်တင်ရန်အတွက်လုပ်ဆောင်ခြင်းဖြစ်ပါသည်။

**1NF (First Normal Form)** — Column တစ်ခုစီတွင် atomic value (တစ်ခုတည်း) သာရှိရမည်။ ဥပမာ — PhoneNumbers column ထဲတွင် ဖုန်းနံပါတ်များစွာထည့်မထားရပါ။

**2NF (Second Normal Form)** — 1NF ဖြစ်ရမည်။ Composite PK ၏တစ်စိတ်တစ်ပိုင်းပေါ်တွင်မူတည်သော column များကိုခွဲထုတ်ရမည်။

**3NF (Third Normal Form)** — 2NF ဖြစ်ရမည်။ Non-key column များသည် PK ပေါ်တွင်သာမူတည်ရမည် (transitive dependency မရှိရပါ)။
