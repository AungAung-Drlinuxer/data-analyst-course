# 🗄️ SQL သင်ရိုး — အခြေခံမှ ကျွမ်းကျင်အဆင့်အထိ

> **သင်ခန်းစာ ၂၂ ခု** | **လက်တွေ့ပရောဂျက်များ** | **အင်တာဗျူးမေးခွန်းများ**

---

## 📖 SQL ဆိုတာဘာလဲ?

**SQL (Structured Query Language)** ဆိုသည်မှာ Database (ဒေတာဘေ့စ်) ထဲမှ ဒေတာများကို-
- ဖန်တီးခြင်း (Create)
- ပြင်ဆင်ခြင်း (Alter/Update)
- ရှာဖွေခြင်း (Select/Read)
- ဖျက်ခြင်း (Delete/Drop)

ပြုလုပ်နိုင်သော **Standard Programming Language** တစ်ခုဖြစ်သည်။

---

## 📑 SQL သင်ခန်းစာ အသေးစိတ် (Module 1-22)

### 🔰 အခြေခံပိုင်း (Foundation) — Module 1-5

| Module | ခေါင်းစဉ် | သင်ယူရမည့်အကြောင်းအရာ |
|--------|-----------|----------------------|
| **1** | Introduction to SQL | SQL သမိုင်း၊ Database အမျိုးအစားများ (RDBMS, NoSQL), SQL Tools (SSMS, DBeaver) |
| **2** | Creating Database | Database ဆိုတာဘာလဲ၊ CREATE DATABASE command၊ Database Options |
| **3** | Creating Table | Table တည်ဆောက်ပုံ၊ CREATE TABLE Syntax၊ Temporary Tables |
| **4** | Data Types & Constraints | INT, VARCHAR, DATE, DECIMAL — Data Types များနှင့် NOT NULL, UNIQUE, DEFAULT, CHECK Constraints |
| **5** | DDL Commands | CREATE, ALTER, DROP, TRUNCATE, RENAME, COMMENT |

### 📊 ဒေတာရှာဖွေခြင်းပိုင်း (Querying) — Module 6-9

| Module | ခေါင်းစဉ် | သင်ယူရမည့်အကြောင်းအရာ |
|--------|-----------|----------------------|
| **6** | DQL Commands | SELECT, WHERE, DISTINCT, BETWEEN, IN, LIKE, IS NULL |
| **7** | Operators | Arithmetic (+, -, *, /), Comparison (=, >, <, <>), Logical (AND, OR, NOT), String Concatenation |
| **8** | LIMIT, ORDER BY, OFFSET, GROUP BY, HAVING | ဒေတာစီခြင်း၊ အုပ်စုခွဲခြင်း၊ စစ်ထုတ်ခြင်း |
| **9** | Aggregate Functions | COUNT, SUM, AVG, MIN, MAX |

### 🔗 Table များချိတ်ဆက်ခြင်းပိုင်း — Module 10-14

| Module | ခေါင်းစဉ် | သင်ယူရမည့်အကြောင်းအရာ |
|--------|-----------|----------------------|
| **10** | Primary & Foreign Key | Table ချိတ်ဆက်ခြင်း အခြေခံ — Primary Key, Foreign Key, Composite Key |
| **11** | JOINS | INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL JOIN, CROSS JOIN, SELF JOIN |
| **12** | Subquery | Nested Queries — WHERE ထဲက Subquery, FROM ထဲက Subquery, EXISTS / NOT EXISTS |
| **13** | Window Functions | ROW_NUMBER, RANK, DENSE_RANK, NTILE, LEAD, LAG, FIRST_VALUE, LAST_VALUE |
| **14** | CTEs (Common Table Expressions) | WITH Clause — Recursive CTE, Multiple CTEs, CTE ကောင်းကျိုးများ |

### 🛠️ Function များပိုင်း — Module 15-18

| Module | ခေါင်းစဉ် | သင်ယူရမည့်အကြောင်းအရာ |
|--------|-----------|----------------------|
| **15** | Text Functions | CONCAT, SUBSTRING, REPLACE, LEN, UPPER/LOWER, TRIM, CHARINDEX, PATINDEX |
| **16** | Numeric Functions | ROUND, CEILING, FLOOR, ABS, POWER, SQRT, RAND |
| **17** | Control Flow Functions | CASE WHEN, IIF, COALESCE, NULLIF, ISNULL |
| **18** | Date & Time Functions | GETDATE, DATEADD, DATEDIFF, DATEPART, FORMAT, EOMONTH, YEAR/MONTH/DAY |

### 🏗️ အဆင့်မြင့်ပိုင်း — Module 19-22

| Module | ခေါင်းစဉ် | သင်ယူရမည့်အကြောင်းအရာ |
|--------|-----------|----------------------|
| **19** | Views | CREATE VIEW, Indexed Views, Schema Binding, View ကောင်းကျိုး/ဆိုးကျိုး |
| **20** | Scenario-Based Interview Q&A | Real-world Interview Questions များ |
| **21** | SQL Complete Material | SQL Cheat Sheet, Best Practices, Performance Tips |
| **22** | SQL Projects | လက်တွေ့ပရောဂျက်များ |

---

## 🎯 SQL သင်ယူရခြင်း ရည်ရွယ်ချက်

Platform Engineer များအတွက် SQL သည် မရှိမဖြစ် အရေးကြီးပါသည် —
- **Database Migration** — ဒေတာဘေ့စ်များ ပြောင်းရွှေ့စဉ် SQL ကို အသုံးပြုရပါသည်
- **Backend Services** — API Services များသည် SQL Database နှင့် ချိတ်ဆက်အလုပ်လုပ်ပါသည်
- **Observability** — ELK Stack, Prometheus အချက်အလက်များကို SQL-like Query များဖြင့် ရှာဖွေနိုင်ပါသည်
- **Data Analysis** — Power BI, Fabric အတွက် SQL Data Source လိုအပ်ပါသည်

---

## ⚡ သင်ယူနည်း အကြံပြုချက်များ

1. **Module တစ်ခုစီအတွက် ကိုယ်တိုင် Query ရေးပါ** — အလွတ်မှတ်စရာမလို၊ နားလည်ရန်သာလိုပါသည်
2. **Sample Database တစ်ခုတည်ဆောက်ပါ** — ကိုယ်တိုင် Database ဆောက်ပြီး လေ့ကျင့်ပါ
3. **Joins & Window Functions** — ၎င်းတို့သည် အရေးကြီးဆုံး Topics များဖြစ်ပါသည်
4. **DBeaver GUI သုံးပါ** — Query Visual Plan ကိုကြည့်ပြီး Execution Plan နားလည်အောင်လုပ်ပါ

---

## 🔧 လိုအပ်သော Setup

| Tool | Download Link | မှတ်ချက် |
|------|--------------|---------|
| PostgreSQL 16 | https://www.postgresql.org/download/ | Local Database Server |
| DBeaver Community | https://dbeaver.io/download/ | SQL GUI Tool **အကြံပြုသည်** |
| SSMS (Windows only) | https://aka.ms/ssmsfullsetup | SQL Server Management Studio |
| SQL Server | Docker: `docker run ... mcr.microsoft.com/mssql/server` | Container |

---

## 📂 ဖိုင်တည်ဆောက်ပုံ

```
01-sql/
├── README.md              ← ဤဖိုင် — SQL သင်ရိုးအကျဉ်းချုပ်
├── modules/
│   ├── 01-introduction-to-sql.md
│   ├── 02-creating-database.md
│   ├── 03-creating-table.md
│   ├── 04-data-types-and-constraints.md
│   ├── 05-ddl-commands.md
│   ├── 06-dql-commands.md
│   ├── 07-operators.md
│   ├── 08-limit-order-by-group-by-having.md
│   ├── 09-aggregate-functions.md
│   ├── 10-primary-foreign-key.md
│   ├── 11-joins.md
│   ├── 12-subquery.md
│   ├── 13-window-functions.md
│   ├── 14-ctes.md
│   ├── 15-text-functions.md
│   ├── 16-numeric-functions.md
│   ├── 17-control-flow-functions.md
│   ├── 18-date-time-functions.md
│   ├── 19-views.md
│   ├── 20-scenario-based-interview-qa.md
│   ├── 21-sql-complete-material.md
│   └── 22-sql-projects.md
├── projects/              → SQL Projects ဖိုင်များ
└── materials/             → Cheat Sheet & Reference
```

---

## 📝 SQL လေ့လာရန် နမူနာ (Sample Query)

```sql
-- Database ဆောက်ခြင်း
CREATE DATABASE ShopDB;
USE ShopDB;

-- Table ဆောက်ခြင်း
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Email VARCHAR(150) UNIQUE,
    JoinDate DATE DEFAULT GETDATE()
);

-- ဒေတာထည့်ခြင်း
INSERT INTO Customers VALUES (1, 'Aung Aung', 'aung@example.com', '2025-01-01');

-- ဒေတာရှာဖွေခြင်း
SELECT * FROM Customers WHERE Name LIKE '%Aung%';
```

---

> ➡️ **စတင်လေ့လာရန်** — `modules/01-introduction-to-sql.md` ကိုဖွင့်ပါ။


## SQL Learning Guide

### How SQL Works

SQL (Structured Query Language) သည် relational database management systems (RDBMS) များတွင် data များကိုစီမံရန်အတွက်အသုံးပြုသော standard language ဖြစ်ပါသည်။

### Database Concepts

Database ဆိုသည်မှာ data များကိုစနစ်တကျသိမ်းဆည်းနိုင်သော container တစ်ခုဖြစ်ပါသည်။ ၎င်းတွင် tables, views, stored procedures စသည့် objects များပါဝင်ပါသည်။

### Why SQL is Important

1. **Universal Language** — Database အားလုံးနီးပါးက SQL ကိုအသုံးပြုပါသည်
2. **Data Analysis Foundation** — Data analyst များအတွက်မရှိမဖြစ်
3. **Backend Development** — Web/mobile app တိုင်းတွင် database ပါဝင်ပါသည်
4. **Cloud & Big Data** — Cloud databases (Snowflake, Redshift) များလည်း SQL သုံးပါသည်
5. **BI Tools Integration** — Power BI, Tableau များက SQL databases များကိုချိတ်ဆက်ပါသည်

### Learning Approach

SQL ကိုလေ့လာရန် အကောင်းဆုံးနည်းလမ်းမှာ-

1. **Theory** — Concept များကိုနားလည်အောင်လေ့လာပါ
2. **Practice** — Code များကိုကိုယ်တိုင်ရေးပါ
3. **Debug** — Error များကိုဖြေရှင်းတတ်အောင်လုပ်ပါ
4. **Optimize** — Query performance ကိုစဉ်းစားပါ
5. **Apply** — Real-world problems များကိုဖြေရှင်းပါ

### Sample Database Setup

```sql
-- Create sample database for practice
CREATE DATABASE PracticeDB;
USE PracticeDB;

-- Create sample tables
CREATE TABLE Employees (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10,2),
    HireDate DATE
);

-- Insert sample data
INSERT INTO Employees VALUES
(1, 'Aung Aung', 'IT', 80000, '2020-01-15'),
(2, 'Mya Mya', 'HR', 55000, '2021-03-20'),
(3, 'Hla Hla', 'Sales', 65000, '2022-06-10');
```

### Module-by-Module Summary

| Module | Topic | What You'll Learn |
|--------|-------|-------------------|
| 1 | SQL Introduction | History, RDBMS, Tools |
| 2 | Create Database | Database creation, options |
| 3 | Create Table | Tables, data types, columns |
| 4-5 | DDL | Create, Alter, Drop, Truncate |
| 6-9 | DQL | Select, Where, Group By, Aggregates |
| 10-11 | Keys & Joins | PK, FK, INNER, LEFT, RIGHT |
| 12-14 | Advanced Query | Subquery, Window, CTE |
| 15-18 | Functions | Text, Numeric, Date, Control Flow |
| 19 | Views | Virtual tables |
| 20-22 | Interview & Projects | Real-world practice |
