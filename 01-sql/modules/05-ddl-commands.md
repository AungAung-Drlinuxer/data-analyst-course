# Module 5: DDL Commands (Data Definition Language)

## DDL Commands ဆိုတာဘာလဲ?

DDL (Data Definition Language) commands များသည် database objects များ၏ structure ကိုသတ်မှတ်ရန်၊ ပြောင်းလဲရန်နှင့်ဖျက်ရန်အသုံးပြုပါသည်။ ၎င်းတို့သည် database schema ကိုသတ်မှတ်ပေးသော commands များဖြစ်ပါသည်။

DDL commands များသည် auto-commit ဖြစ်ပြီး transaction အတွင်းမှ rollback လုပ်၍မရပါ (အချို့ RDBMS များတွင် ရနိုင်သည်)။

## DDL Commands အသေးစိတ်

### CREATE Command

Object အသစ်များဖန်တီးရန် အသုံးပြုပါသည်။

```sql
-- Database ဆောက်ခြင်း
CREATE DATABASE SchoolDB;

-- Table ဆောက်ခြင်း
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Email VARCHAR(150) UNIQUE
);

-- View ဆောက်ခြင်း (virtual table)
CREATE VIEW ActiveStudents AS
SELECT * FROM Students WHERE Status = 'Active';

-- Index ဆောက်ခြင်း (performance အတွက်)
CREATE NONCLUSTERED INDEX IX_Students_Name 
ON Students(Name);

-- Stored Procedure ဆောက်ခြင်း
CREATE PROCEDURE GetStudentByID
    @StudentID INT
AS
BEGIN
    SELECT * FROM Students WHERE StudentID = @StudentID;
END;
```

### ALTER Command

Existing object များ၏ structure ကိုပြောင်းလဲရန်။

#### Column Operations
```sql
-- Column အသစ်ထည့်ခြင်း
ALTER TABLE Students ADD Phone VARCHAR(20) NULL;
ALTER TABLE Students ADD Age INT NOT NULL DEFAULT 0;

-- Column data type ပြောင်းခြင်း
ALTER TABLE Students ALTER COLUMN Name VARCHAR(200);
ALTER TABLE Students ALTER COLUMN Age SMALLINT;

-- Column ဖျက်ခြင်း
ALTER TABLE Students DROP COLUMN Phone;
```

#### Constraint Operations
```sql
-- Primary key ထည့်ခြင်း
ALTER TABLE Students ADD CONSTRAINT PK_Student PRIMARY KEY (StudentID);

-- Foreign key ထည့်ခြင်း
ALTER TABLE Enrollments ADD CONSTRAINT FK_Enrollments_Students
FOREIGN KEY (StudentID) REFERENCES Students(StudentID);

-- Default constraint ထည့်ခြင်း
ALTER TABLE Students ADD CONSTRAINT DF_Status DEFAULT 'Active' FOR Status;

-- Check constraint ထည့်ခြင်း
ALTER TABLE Students ADD CONSTRAINT CK_Age CHECK (Age >= 0 AND Age <= 150);

-- Constraint ဖျက်ခြင်း
ALTER TABLE Students DROP CONSTRAINT CK_Age;
```

#### Database Operations
```sql
-- Database name ပြောင်းခြင်း
ALTER DATABASE SchoolDB MODIFY NAME = SchoolDB_2024;

-- Database size ပြောင်းခြင်း
ALTER DATABASE SchoolDB MODIFY FILE (
    NAME = SchoolDB_Data,
    SIZE = 200MB
);
```

### DROP Command

Object များကိုလုံးဝဖျက်ရန်အသုံးပြုပါသည် (structure နှင့် data နှစ်ခုလုံးပါပျက်မည်)။

```sql
-- Table ဖျက်ခြင်း
DROP TABLE Students;

-- Database ဖျက်ခြင်း
DROP DATABASE SchoolDB;

-- View ဖျက်ခြင်း
DROP VIEW ActiveStudents;

-- Index ဖျက်ခြင်း
DROP INDEX IX_Students_Name ON Students;

-- Stored procedure ဖျက်ခြင်း
DROP PROCEDURE GetStudentByID;
```

### TRUNCATE Command

Table ထဲမှ data အားလုံးကိုဖျက်ပစ်ပြီး table structure ကိုကျန်ခဲ့စေပါသည်။

```sql
TRUNCATE TABLE Students;
-- Students table ထဲက row အားလုံးပျက်မည်။ structure ကျန်မည်။
```

#### TRUNCATE vs DELETE

| Feature | TRUNCATE | DELETE |
|---------|----------|--------|
| Speed | Very fast | Slower |
| WHERE clause | မရ | ရ |
| Transaction log | Minimal (page deallocation) | Full (row-by-row) |
| Triggers | မဖြစ် | ဖြစ် |
| Identity reset | Yes (ပြန် 1 ဖြစ်) | No (ဆက်တိုး) |
| Rollback | မရ | ရ (transaction အတွင်းဆိုလျှင်) |

### RENAME Command

Object အမည်ပြောင်းလဲရန်။

```sql
-- SQL Server
EXEC sp_rename 'OldTableName', 'NewTableName';
EXEC sp_rename 'Students.Phone', 'MobilePhone', 'COLUMN';

-- PostgreSQL
ALTER TABLE old_name RENAME TO new_name;
ALTER TABLE students RENAME COLUMN phone TO mobile_phone;

-- MySQL
RENAME TABLE old_name TO new_name;
ALTER TABLE students RENAME COLUMN phone TO mobile_phone;
```

## DDL Best Practices

1. **Production တွင် DDL မလုပ်မီ Backup ယူပါ** — DROP/ALTER သည် irreversible ဖြစ်နိုင်ပါသည်။
2. **Development environment တွင်အရင်စမ်းပါ** — Production တွင်တိုက်ရိုက်မလုပ်ရ။
3. **Naming convention ကိုလိုက်နာပါ** — Tables: PascalCase, Indexes: IX_TableName, Constraints: PK_/FK_/CK_
4. **Peak hours ကိုရှောင်ပါ** — DDL commands သည် locking ဖြစ်စေနိုင်ပါသည်။
5. **Script များကို version control ထားပါ** — Database changes များကို Git တွင်သိမ်းပါ။
6. **Foreign keys များကိုသတိထားပါ** — DROP table မလုပ်မီ dependencies များကိုစစ်ဆေးပါ။

## DDL Exercises

1. Database အသစ်ဆောက်ပါ — 'CompanyDB'
2. Departments table ဆောက်ပါ (DeptID, DeptName, Location)
3. Employees table ဆောက်ပါ (EmpID, Name, Salary, DeptID FK)
4. Employees table တွင် Email column အသစ်ထည့်ပါ
5. Salary column ၏ data type ကို DECIMAL(12,2) သို့ပြောင်းပါ
6. Employees table ကို TRUNCATE လုပ်ပြီး DELETE နှင့်ကွာခြားချက်ကိုလေ့လာပါ
7. Departments table ကို DROP မလုပ်မီ error ရအောင်ကြည့်ပါ (FK ကြောင့်)

## DDL Commands Detailed Examples (အသေးစိတ်နမူနာများ)

### CREATE Command များစွာ

```sql
-- Database with multiple filegroups
CREATE DATABASE SalesDB
ON PRIMARY (
    NAME = 'SalesDB_Data',
    FILENAME = 'D:\Data\SalesDB.mdf',
    SIZE = 1GB, MAXSIZE = 10GB, FILEGROWTH = 500MB
),
FILEGROUP SalesData (
    NAME = 'SalesDB_Data2',
    FILENAME = 'E:\Data\SalesDB2.ndf',
    SIZE = 1GB, MAXSIZE = 10GB, FILEGROWTH = 500MB
)
LOG ON (
    NAME = 'SalesDB_Log',
    FILENAME = 'F:\Logs\SalesDB.ldf',
    SIZE = 500MB, MAXSIZE = 5GB, FILEGROWTH = 200MB
);
```

### ALTER Command များစွာ

```sql
-- Multiple column changes
ALTER TABLE Employees
    ADD DateOfBirth DATE NULL,
    ALTER COLUMN Phone VARCHAR(20) NULL,
    DROP COLUMN OldColumn;

-- Enable/disable constraint
ALTER TABLE Orders NOCHECK CONSTRAINT FK_Orders_Customers;
ALTER TABLE Orders CHECK CONSTRAINT FK_Orders_Customers;

-- Rebuild index
ALTER INDEX ALL ON Orders REBUILD;
```

### DROP vs TRUNCATE vs DELETE Performance

| Operation | Speed | Logged | Can Rollback | Resets Identity |
|-----------|-------|--------|--------------|-----------------|
| DROP | Fastest | Minimal | No | N/A (table gone) |
| TRUNCATE | Very Fast | Minimal | No (in some DBs) | Yes |
| DELETE | Slow | Full | Yes | No |

### DDL in Transactions

```sql
BEGIN TRANSACTION;
ALTER TABLE Orders ADD NewColumn INT NULL;
ALTER TABLE Orders ADD CONSTRAINT DF_NewCol DEFAULT 0 FOR NewColumn;
-- If something goes wrong
ROLLBACK TRANSACTION;  -- Reverts both ALTER commands
-- Or COMMIT TRANSACTION; to save changes
```

### Schema Management

Schema ဆိုသည်မှာ database objects များကိုစုဖွဲ့ထားခြင်းဖြစ်ပါသည်။

```sql
-- Create schema
CREATE SCHEMA Sales;
CREATE SCHEMA HR;
CREATE SCHEMA Inventory;

-- Create table in specific schema
CREATE TABLE Sales.Orders (OrderID INT PRIMARY KEY);
CREATE TABLE HR.Employees (EmpID INT PRIMARY KEY);
CREATE TABLE Inventory.Products (ProductID INT PRIMARY KEY);

-- Move table to different schema
ALTER SCHEMA Sales TRANSFER dbo.Orders;
```

### Viewing Object Information

```sql
-- All tables with schema
SELECT TABLE_SCHEMA, TABLE_NAME, TABLE_TYPE
FROM INFORMATION_SCHEMA.TABLES
ORDER BY TABLE_SCHEMA, TABLE_NAME;

-- All columns of a table
SELECT COLUMN_NAME, DATA_TYPE, CHARACTER_MAXIMUM_LENGTH, IS_NULLABLE
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'Employees';

-- All constraints
SELECT * FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS;
```

### DDL Script Management

Production database တွင် DDL scripts များကိုစနစ်တကျစီမံရန် —

**Version Control** — DDL scripts များကို Git တွင်သိမ်းဆည်းပါ။ Migration scripts များကို folder အလိုက်စုစည်းပါ (V1__Initial.sql, V2__AddCustomers.sql, V3__AddOrders.sql)

**Migration Tools** — Flyway, Liquibase, Entity Framework Migrations စသည့် tools များသည် database schema changes များကိုစနစ်တကျ manage လုပ်ပေးပါသည်။

**Testing** — DDL scripts များကို development environment တွင်အရင်စမ်းသပ်ပါ။ Production တွင်တိုက်ရိုက်မလုပ်ဆောင်ပါနှင့်။

**Rollback Plan** — DDL change တစ်ခုစီအတွက် rollback script ကိုပါပြင်ဆင်ထားပါ။

```sql
-- Example migration structure
-- V1__CreateTables.sql
-- V2__AddEmailColumn.sql
-- V2__AddEmailColumn_rollback.sql
-- V3__CreateOrdersTable.sql
-- V3__CreateOrdersTable_rollback.sql
```

### Working with Database Schemas

Schema ဆိုသည်မှာ database objects များကိုယုတ္တိကျကျစုဖွဲ့ထားခြင်းဖြစ်ပါသည်။ ၎င်းသည်-
- Objects များကိုစနစ်တကျစုစည်းပေးပါသည်
- Security ကိုပိုမိုကောင်းမွန်စေပါသည် (schema အလိုက် permission ပေးနိုင်)
- Naming conflicts များကိုရှောင်ရှားနိုင်ပါသည်

Default schema မှာ dbo (SQL Server) ဖြစ်ပါသည်။ Schema သုံးရန် — CREATE TABLE SchemaName.TableName (...) ဟုရေးပါ။

```sql
CREATE SCHEMA Sales;
CREATE SCHEMA HR;
CREATE TABLE Sales.Orders (...);
CREATE TABLE HR.Employees (...);
```
