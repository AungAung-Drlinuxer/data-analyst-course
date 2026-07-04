# Module 4: Data Types နှင့် Constraints

## Data Types (ဒေတာအမျိုးအစားများ)

Data Type ဆိုသည်မှာ column တစ်ခုတွင် မည်သည့်အမျိုးအစား data ကိုသိမ်းဆည်းမည်ကိုသတ်မှတ်ပေးသော attribute တစ်ခုဖြစ်ပါသည်။ သင့်တော်သော data type ကိုရွေးချယ်ခြင်းသည် database performance နှင့် storage efficiency ကိုများစွာသက်ရောက်မှုရှိပါသည်။

### String Data Types (စာသားဒေတာအမျိုးအစားများ)

String data types များသည် စာသား၊ နာမည်၊ လိပ်စာ၊ ဖော်ပြချက်စသည့် textual data များကိုသိမ်းဆည်းရန်အသုံးပြုပါသည်။

| Data Type | Description | Storage | Max Size |
|-----------|-------------|---------|----------|
| CHAR(n) | Fixed-length character string | n bytes | 8000 chars |
| VARCHAR(n) | Variable-length character string | Actual + 2 bytes | 8000 chars |
| VARCHAR(MAX) | Large variable-length string | 2GB | ~2 billion chars |
| NCHAR(n) | Fixed-length Unicode string | n * 2 bytes | 4000 chars |
| NVARCHAR(n) | Variable-length Unicode string | Actual * 2 + 2 | 4000 chars |
| NVARCHAR(MAX) | Large Unicode string | 2GB | ~1 billion chars |

**မှတ်ချက်**: Unicode (NVARCHAR/NCHAR) သည် မြန်မာ၊ ဂျပန်၊ တရုတ် စသည့် ဘာသာစကားများကိုသိမ်းဆည်းရန်အတွက်လိုအပ်ပါသည်။ အင်္ဂလိပ်စာသားများအတွက် VARCHAR ကိုသုံးပါ (NVARCHAR သည် storage နှစ်ဆယူပါသည်)။

### Numeric Data Types (ကိန်းဂဏန်းအမျိုးအစားများ)

Numeric types များသည် ကိန်းဂဏန်းများ၊ ငွေကြေးများ၊ တိုင်းတာမှုများကိုသိမ်းဆည်းရန်အသုံးပြုပါသည်။

**Exact Numeric Types**

| Data Type | Range | Storage | Use Case |
|-----------|-------|---------|----------|
| BIT | 0, 1, or NULL | 1 bit | Boolean flags (Yes/No) |
| TINYINT | 0 to 255 | 1 byte | Small numbers, age |
| SMALLINT | -32,768 to 32,767 | 2 bytes | Department codes |
| INT | -2.1B to 2.1B | 4 bytes | General purpose IDs |
| BIGINT | -9.22Q to 9.22Q | 8 bytes | Large counters |
| DECIMAL(p,s) | Variable | 5-17 bytes | Financial data |
| NUMERIC(p,s) | Same as DECIMAL | 5-17 bytes | Exact calculations |
| MONEY | -922T to 922T | 8 bytes | Currency values |
| SMALLMONEY | -214K to 214K | 4 bytes | Small currency |

**DECIMAL(p,s) ရှင်းလင်းချက်**
- p (precision): စုစုပေါင်းဂဏန်းအရေအတွက်
- s (scale): ဒဿမကိန်းနေရာအရေအတွက်
- ဥပမာ: DECIMAL(10,2) = 10 လုံးစာ၊ 2 လုံးက ဒသမနောက်
- သင့်တော်သော Use Case: ငွေကြေးတန်ဖိုးများ၊ တိကျသောတွက်ချက်မှုများ

**Approximate Numeric Types**

| Data Type | Precision | Use Case |
|-----------|-----------|----------|
| FLOAT(n) | Approximate (15 digits) | Scientific calculations |
| REAL | Approximate (7 digits) | Less precise floating point |

**သတိပြုရန်**: FLOAT/REAL သည် ငွေကြေးတွက်ချက်ရန်မသင့်တော်ပါ (rounding error ဖြစ်နိုင်သောကြောင့်)။

### Date and Time Data Types

| Data Type | Description | Accuracy | Storage |
|-----------|-------------|----------|---------|
| DATE | YYYY-MM-DD | 1 day | 3 bytes |
| TIME(n) | hh:mm:ss.nnnnnnn | 100 ns | 3-5 bytes |
| DATETIME | YYYY-MM-DD hh:mm:ss.nnn | 3.33 ms | 8 bytes |
| DATETIME2(n) | YYYY-MM-DD hh:mm:ss.nnnnnnn | 100 ns | 6-8 bytes |
| SMALLDATETIME | YYYY-MM-DD hh:mm:00 | 1 min | 4 bytes |
| DATETIMEOFFSET | With timezone | 100 ns | 10 bytes |

## Constraints (ကန့်သတ်ချက်များ)

Constraints များသည် data integrity (ဒေတာတိကျမှန်ကန်မှု) ကိုထိန်းသိမ်းရန် အသုံးပြုပါသည်။

### 1. NOT NULL Constraint
Column သည် NULL တန်ဖိုးမဖြစ်ရပါ (data ရှိရမည်)။
```sql
CREATE TABLE Employees (
    EmpID INT NOT NULL,
    FullName VARCHAR(100) NOT NULL
);
```

### 2. UNIQUE Constraint
Column ရှိတန်ဖိုးများအားလုံးထူးခြားရမည် (ထပ်မရ)။
```sql
CREATE TABLE Users (
    UserID INT PRIMARY KEY,
    Username VARCHAR(50) UNIQUE,
    Email VARCHAR(150) CONSTRAINT UQ_Email UNIQUE
);
```

### 3. PRIMARY KEY Constraint
Row တစ်ခုစီကိုသီးသန့်ခွဲခြားသတ်မှတ်ခြင်း (UNIQUE + NOT NULL)။
```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL
);
```

### 4. FOREIGN KEY Constraint
Table နှစ်ခုကိုချိတ်ဆက်ခြင်းနှင့် referential integrity ကိုထိန်းသိမ်းခြင်း။
```sql
CREATE TABLE Enrollments (
    EnrollmentID INT PRIMARY KEY,
    StudentID INT FOREIGN KEY REFERENCES Students(StudentID),
    CourseID INT FOREIGN KEY REFERENCES Courses(CourseID)
);
```

### 5. CHECK Constraint
Column တန်ဖိုးအတွက် condition စစ်ဆေးခြင်း။
```sql
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    Price DECIMAL(10,2) CHECK (Price >= 0),
    Age INT CHECK (Age >= 0 AND Age <= 150),
    Status VARCHAR(20) CHECK (Status IN ('Active', 'Inactive', 'Discontinued'))
);
```

### 6. DEFAULT Constraint
Insert လုပ်သည့်အခါတန်ဖိုးမထည့်ပါက အလိုအလျောက်ထည့်ပေးမည့် default value သတ်မှတ်ခြင်း။
```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    OrderDate DATETIME DEFAULT GETDATE(),
    Status VARCHAR(20) DEFAULT 'Pending'
);
```

## လေ့ကျင့်ခန်း

အောက်ပါ table ကိုဆောက်ပါ: Employees (EmpID INT PK, Name NVARCHAR NOT NULL, Email VARCHAR UNIQUE, Salary DECIMAL CHECK > 0, DeptID INT FK, HireDate DATE DEFAULT GETDATE())

## Data Type Selection Best Practices (အသေးစိတ်လမ်းညွှန်)

သင့်တော်သော data type ကိုရွေးချယ်ခြင်းသည် database performance အတွက်အလွန်အရေးကြီးပါသည်။

### Choosing Between CHAR and VARCHAR

CHAR(n) သည် fixed-length ဖြစ်ပြီး data ၏အရှည်တူညီသည့်အခါသုံးပါသည်။ ဥပမာ — CountryCode CHAR(2), Gender CHAR(1), YesNo CHAR(1)။ CHAR သည် faster ဖြစ်သော်လည်း space ပိုသုံးပါသည်။

VARCHAR(n) သည် variable-length ဖြစ်ပြီး data ၏အရှည်မတူညီသည့်အခါသုံးပါသည်။ ဥပမာ — Name, Email, Address။ VARCHAR သည် space ချွေတာပါသည်။

### Choosing Between Numeric Types

| Data Type | Bytes | Range | Best For |
|-----------|-------|-------|----------|
| TINYINT | 1 | 0-255 | Age, Small flags |
| SMALLINT | 2 | -32K to 32K | Department codes, Year |
| INT | 4 | -2.1B to 2.1B | IDs, Counters (most common) |
| BIGINT | 8 | -9.2Q to 9.2Q | Large IDs, Big counters |
| DECIMAL(18,2) | 9 | Large | Financial (precise) |
| FLOAT | 8 | Very large | Scientific (approximate) |

### Choosing Between Date Types

| Type | Bytes | Accuracy | Best For |
|------|-------|----------|----------|
| DATE | 3 | 1 day | Birthdays, Hire dates |
| DATETIME | 8 | 3.33 ms | Legacy applications |
| DATETIME2 | 6-8 | 100 ns | Modern apps (recommended) |
| SMALLDATETIME | 4 | 1 min | Simple date tracking |

### Constraint Design Patterns

**Pattern 1: Status with CHECK**
```sql
CREATE TABLE Orders (
    Status VARCHAR(20) 
        CHECK (Status IN ('Pending', 'Processing', 'Shipped', 'Delivered', 'Cancelled'))
);
```

**Pattern 2: Multiple Constraints**
```sql
CREATE TABLE Employees (
    Salary DECIMAL(10,2) CHECK (Salary >= 0),
    Email VARCHAR(150) NOT NULL,
    Phone VARCHAR(20) UNIQUE,
    DepartmentID INT NOT NULL DEFAULT 1,
    HireDate DATE NOT NULL,
    CONSTRAINT CK_Age CHECK (Age BETWEEN 18 AND 65),
    CONSTRAINT CK_Email CHECK (Email LIKE '%_@%_._%')
);
```

### NULL vs NOT NULL Decision Guide

NOT NULL ထားသင့်သော column များ — Primary key, Foreign key, Name, Email (if required), Status, CreatedDate

NULL ခွင့်ပြုနိုင်သော column များ — Phone (optional), MiddleName, Description, ModifiedDate, DiscontinuedDate

### Identity Column Patterns

```sql
-- Standard identity (1,1)
CREATE TABLE Customers (CustomerID INT IDENTITY(1,1) PRIMARY KEY);

-- Start from 1000, increment by 10
CREATE TABLE Products (ProductID INT IDENTITY(1000,10) PRIMARY KEY);

-- GUID as PK (for distributed systems)
CREATE TABLE Sessions (SessionID UNIQUEIDENTIFIER DEFAULT NEWID() PRIMARY KEY);
```

### Performance Impact of Data Types

သင့်တော်သော data type ကိုရွေးချယ်ခြင်းသည် query performance ကိုများစွာသက်ရောက်မှုရှိပါသည်။

**Faster Data Types** — INT, DATE, BIT, CHAR (fixed-length) တို့သည် VARCHAR, NVARCHAR, TEXT တို့ထက်မြန်ပါသည်။

**Storage Impact** — VARCHAR(100) က VARCHAR(MAX) ထက်ပိုကောင်းပါသည်။ VARCHAR(MAX) သည် data ကို normal row ထဲမသိမ်းတော့ဘဲ separate page ထဲသိမ်းပါသည်။

**Index Size** — Narrow data types (INT, DATE) များသည် index သေးငယ်စေပြီး query မြန်စေပါသည်။ Wide data types (NVARCHAR(500)) များသည် index ကြီးမားစေပါသည်။

**Best Practice** — Column size ကိုတိတိကျကျသတ်မှတ်ပါ။ Name = VARCHAR(100), Email = VARCHAR(150), Phone = VARCHAR(20) စသည်ဖြင့်။

### Constraints in Practice

**When to Use Each Constraint**
- Primary Key: Table တိုင်းတွင်ထားရန် (ခြွင်းချက်မရှိ)
- Foreign Key: Related tables များကြားတွင်ထားရန်
- Unique: Duplicate မဖြစ်စေလိုသော columns များအတွက် (Email, Username)
- Check: Validation လိုအပ်သော columns များအတွက် (Age >= 0, Price > 0)
- Default: Common default values များအတွက် (Status, CreatedDate)
- NOT NULL: မဖြစ်မနေလိုအပ်သော columns များအတွက် (Name)

**Constraint Naming Convention**
- PK: PK_TableName (PK_Customers)
- FK: FK_ChildTable_ParentTable (FK_Orders_Customers)
- UQ: UQ_TableName_Column (UQ_Customers_Email)
- CK: CK_TableName_Description (CK_Products_PricePositive)
- DF: DF_TableName_Column (DF_Orders_OrderDate)
