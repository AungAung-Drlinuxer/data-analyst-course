# Module 10: Primary & Foreign Key

## Primary Key ဆိုတာဘာလဲ?

Primary Key (PK) သည် table တစ်ခုရှိ row တစ်ခုစီကိုသီးသန့်ခွဲခြားသတ်မှတ်ပေးသော column (သို့မဟုတ် column အုပ်စု) ဖြစ်ပါသည်။ PK သည် UNIQUE နှင့် NOT NULL ဖြစ်ရမည်။ Table တစ်ခုလျှင် PK တစ်ခုသာရှိနိုင်ပါသည်။

### Primary Key ၏အရေးပါပုံ

1. **Unique Identification** — Row တစ်ခုချင်းစီကိုသီးသန့်ခွဲခြားသတ်မှတ်နိုင်ခြင်း
2. **Indexing** — PK တွင် clustered index အလိုအလျောက်တည်ဆောက်ပေးပြီး query performance ကိုကောင်းမွန်စေပါသည်
3. **Referential Integrity** — Foreign keys များက PK ကိုရည်ညွှန်းပြီး table များကိုချိတ်ဆက်ပါသည်
4. **Data Integrity** — Duplicate rows များမဖြစ်စေရန်တားဆီးပေးပါသည်

### Primary Key Syntax များ

```sql
-- Single column PK (Column level)
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL
);

-- Single column PK (Table level - နာမည်ပေးနိုင်)
CREATE TABLE Students (
    StudentID INT,
    Name VARCHAR(100),
    CONSTRAINT PK_Students PRIMARY KEY (StudentID)
);

-- Composite Primary Key (column များစွာ)
CREATE TABLE Enrollments (
    StudentID INT,
    CourseID INT,
    EnrollmentDate DATE,
    Grade CHAR(2),
    CONSTRAINT PK_Enrollments PRIMARY KEY (StudentID, CourseID)
);
-- StudentID နှင့် CourseID တွဲဆက်မှုတစ်ခုစီသည် unique ဖြစ်ရမည်

-- ALTER table ဖြင့် PK ထည့်ခြင်း
ALTER TABLE Students ADD CONSTRAINT PK_Students PRIMARY KEY (StudentID);
```

### Primary Key Selection Tips

PK အတွက် column ရွေးချယ်ရာတွင် အောက်ပါအချက်များကိုဆင်ခြင်ပါ-

1. **Surrogate Key vs Natural Key**:
   - Surrogate Key (Identity, GUID): စက်မှအလိုအလျောက်ထုတ်ပေးသောတန်ဖိုး — ပိုလုံခြုံသည်၊ ပြောင်းလဲမှုမရှိ
   - Natural Key (SSN, Email): လက်တွေ့ကမ္ဘာမှတန်ဖိုး — ပြောင်းလဲနိုင်သည်၊ duplicate ဖြစ်နိုင်သည်

2. **INT vs GUID**:
   - INT (4 bytes): ပိုမြန်သည်၊ နေရာချွေတာသည်၊ sequential
   - GUID/UNIQUEIDENTIFIER (16 bytes): ဖြန့်ဝေစနစ်များအတွက်သင့်တော်၊ random

## Foreign Key ဆိုတာဘာလဲ?

Foreign Key (FK) သည် table နှစ်ခုကိုချိတ်ဆက်ပေးပြီး referential integrity ကိုထိန်းသိမ်းပေးပါသည်။ FK ရှိသော table ကို child table ဟုခေါ်ပြီး PK ရှိသော table ကို parent table ဟုခေါ်ပါသည်။

### Foreign Key Syntax

```sql
-- Column level
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT REFERENCES Customers(CustomerID),
    OrderDate DATE,
    Amount DECIMAL(10,2)
);

-- Table level (constraint name ပေးနိုင်)
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT NOT NULL,
    OrderDate DATE DEFAULT GETDATE(),
    Amount DECIMAL(10,2),
    CONSTRAINT FK_Orders_Customers 
        FOREIGN KEY (CustomerID) 
        REFERENCES Customers(CustomerID)
);
```

### Referential Actions (ON DELETE / ON UPDATE)

| Action | Description | Example |
|--------|-------------|---------|
| NO ACTION (default) | Parent row ကိုဖျက်၍မရ (error) | Safe option |
| CASCADE | Parent ပါ child ကိုပါဖျက်မည် | Order → OrderItems |
| SET NULL | Parent ဖျက်ပါက child FK ကို NULL ထားမည် | Optional relationship |
| SET DEFAULT | Parent ဖျက်ပါက child FK ကို default ထားမည် | Rarely used |

```sql
CREATE TABLE OrderItems (
    OrderItemID INT PRIMARY KEY,
    OrderID INT NOT NULL,
    ProductID INT NOT NULL,
    Quantity INT,
    CONSTRAINT FK_OrderItems_Orders 
        FOREIGN KEY (OrderID) 
        REFERENCES Orders(OrderID)
        ON DELETE CASCADE,
    CONSTRAINT FK_OrderItems_Products 
        FOREIGN KEY (ProductID) 
        REFERENCES Products(ProductID)
);
```

### Relationship Types

1. **One-to-One (1:1)**: PK and FK တူညီ — User ↔ UserProfile
2. **One-to-Many (1:N)**: အသုံးအများဆုံး — Customer → Orders
3. **Many-to-Many (N:M)**: Junction table လိုအပ် — Students ↔ Courses via Enrollments

### Foreign Key Best Practices

- FK column များကို NOT NULL ထားပါ (ဖြစ်နိုင်လျှင်)
- FK column name ကို parent table name + ID ပုံစံပေးပါ (CustomerID, ProductID)
- ON DELETE CASCADE ကိုသတိသုံးပါ (data loss ဖြစ်နိုင်)
- Index FK columns များတွင် index ထားပါ (JOIN performance)

## Exercises

1. Departments (DeptID PK, DeptName) နှင့် Employees (EmpID PK, Name, DeptID FK) table များဆောက်ပါ။
2. FK ပါသော child table ထဲသို့ parent တွင်မရှိသော DeptID ဖြင့် insert လုပ်ကြည့်ပါ (error ရမည်)။
3. Parent row ကိုဖျက်ကြည့်ပြီး referential action များကိုစမ်းသပ်ပါ။

## Keys များအကြောင်းအသေးစိတ် (In-Depth Key Concepts)

### Super Key, Candidate Key, Primary Key ကွာခြားချက်

**Super Key** — Row တစ်ခုစီကိုသီးသန့်ခွဲခြားသတ်မှတ်နိုင်သော column တစ်ခု (သို့မဟုတ်) column အုပ်စုဖြစ်ပါသည်
**Candidate Key** — Super Key များထဲမှ minimal super key (အနည်းဆုံး columns ပါဝင်သော)
**Primary Key** — Candidate Key များထဲမှတစ်ခုကို PK အဖြစ်ရွေးချယ်ခြင်း

ဥပမာ — Employees table တွင်-
- Super Key: {EmployeeID}, {SSN}, {EmployeeID, Name}, {SSN, Name}
- Candidate Key: {EmployeeID}, {SSN} (minimal)
- Primary Key: {EmployeeID} (ရွေးချယ်ထားသော candidate key)

### Surrogate Key vs Natural Key

| Aspect | Surrogate Key | Natural Key |
|--------|--------------|-------------|
| Source | System-generated (IDENTITY, GUID) | Real-world value (SSN, Email) |
| Uniqueness | Always unique | May change |
| Stability | Never changes | Can change |
| Performance | INT is fast | VARCHAR is slower |
| Readability | No meaning | Has meaning |
| Recommendation | **Use this** | Avoid if possible |

### Foreign Key Actions အသေးစိတ်

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    CONSTRAINT FK_Orders_Customers 
        FOREIGN KEY (CustomerID) 
        REFERENCES Customers(CustomerID)
        ON DELETE CASCADE      -- Customer ဖျက်ပါက Order များပါဖျက်
        ON UPDATE CASCADE      -- CustomerID ပြောင်းပါက Order များပါပြောင်း
);
```

### Foreign Key နှင့် Performance

FK များသည် data integrity ကိုထိန်းသိမ်းပေးသော်လည်း performance ကိုအနည်းငယ်ထိခိုက်စေနိုင်ပါသည်-
- INSERT/UPDATE/DELETE တိုင်းတွင် FK validation လုပ်ရပါသည်
- FK columns များတွင် index ထားပါက JOIN performance ကောင်းပါသည်
- Large tables များတွင် FK များသည် performance overhead ဖြစ်စေနိုင်ပါသည်

### Practical Scenario: E-Commerce Database Keys

```sql
-- Customers table (parent)
CREATE TABLE Customers (
    CustomerID INT IDENTITY(1,1) PRIMARY KEY,  -- Surrogate PK
    Email VARCHAR(150) NOT NULL UNIQUE,          -- Natural key (alternative)
    Name NVARCHAR(100) NOT NULL
);

-- Orders table (child)
CREATE TABLE Orders (
    OrderID INT IDENTITY(1000,1) PRIMARY KEY,
    CustomerID INT NOT NULL,
    OrderDate DATETIME DEFAULT GETDATE(),
    CONSTRAINT FK_Orders_Customers 
        FOREIGN KEY (CustomerID) 
        REFERENCES Customers(CustomerID)
);
-- CustomerID တွင် index ထားရန် (JOIN performance)
CREATE INDEX IX_Orders_CustomerID ON Orders(CustomerID);
```



### Referential Integrity Best Practices

Referential integrity သည် database ၏အရေးကြီးဆုံး concept များထဲမှတစ်ခုဖြစ်ပါသည်။ ၎င်းသည် data များကြားဆက်စပ်မှုကိုတိတိကျကျထိန်းသိမ်းပေးပါသည်။

**ON DELETE CASCADE ကိုသတိသုံးရန်** — Parent row ဖျက်ပါက child rows များပါအလိုအလျောက်ဖျက်ပစ်မည်။ ဥပမာ — Customer ဖျက်ပါ� Orders နှင့် OrderItems များပါပါဖျက်ပစ်မည်။

**ON DELETE SET NULL** — Parent ဖျက်ပါက child ၏ FK ကို NULL ထားပေးမည်။ ဥပမာ — Product ဖျက်ပါက OrderItems.ProductID ကို NULL ထားမည်။

**ON DELETE SET DEFAULT** — Parent ဖျက်ပါက child ၏ FK ကို default value ထားပေးမည်။

### Performance Considerations

Foreign keys များသည် data integrity ကိုထိန်းသိမ်းပေးသော်လည်း performance ကိုအနည်းငယ်ထိခိုက်စေနိုင်ပါသည်။
- INSERT: FK validation လုပ်ရန် parent table ကိုစစ်ဆေးပါသည်
- DELETE: Child table တွင် reference ရှိမရှိစစ်ဆေးပါသည်
- UPDATE: Cascade operations များလုပ်ဆောင်ရပါသည်

ဤ overhead ကိုလျှော့ချရန် FK columns များတွင် index ထားရှိရန်အကြံပြုပါသည်။

### Real-World Database Design Example

**E-Commerce Database Schema**

```sql
-- Customers (parent)
CREATE TABLE Customers (
    CustomerID INT IDENTITY(1,1) PRIMARY KEY,
    Email VARCHAR(150) NOT NULL UNIQUE,
    Name NVARCHAR(100) NOT NULL,
    Phone VARCHAR(20),
    CreatedDate DATETIME DEFAULT GETDATE()
);

-- Orders (child of Customers)
CREATE TABLE Orders (
    OrderID INT IDENTITY(1000,1) PRIMARY KEY,
    CustomerID INT NOT NULL,
    OrderDate DATETIME DEFAULT GETDATE(),
    Status VARCHAR(20) DEFAULT 'Pending',
    TotalAmount DECIMAL(10,2),
    CONSTRAINT FK_Orders_Customers FOREIGN KEY (CustomerID)
        REFERENCES Customers(CustomerID)
);
CREATE INDEX IX_Orders_CustomerID ON Orders(CustomerID);

-- OrderItems (child of Orders and Products)
CREATE TABLE OrderItems (
    OrderItemID INT IDENTITY(1,1) PRIMARY KEY,
    OrderID INT NOT NULL,
    ProductID INT NOT NULL,
    Quantity INT CHECK (Quantity > 0),
    UnitPrice DECIMAL(10,2),
    CONSTRAINT FK_OrderItems_Orders FOREIGN KEY (OrderID)
        REFERENCES Orders(OrderID) ON DELETE CASCADE,
    CONSTRAINT FK_OrderItems_Products FOREIGN KEY (ProductID)
        REFERENCES Products(ProductID)
);
CREATE INDEX IX_OrderItems_OrderID ON OrderItems(OrderID);
CREATE INDEX IX_OrderItems_ProductID ON OrderItems(ProductID);
```

ဤဒီဇိုင်းသည် —
- Customer တစ်ယောက်တွင် Order များစွာရှိနိုင် (1:N)
- Order တစ်ခုတွင် Item များစွာရှိနိုင် (1:N)
- Product တစ်ခုသည် Order များစွာတွင်ပါဝင်နိုင် (N:N)
- ON DELETE CASCADE: Order ဖျက်ပါက ၎င်း၏ Items များပါဖျက်ပစ်မည်
