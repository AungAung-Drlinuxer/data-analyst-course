# Module 2: Database ဖန်တီးခြင်း (Creating Database)

## Database ဆိုတာဘာလဲ?

Database ဆိုသည်မှာ ဒေတာများကို စနစ်တကျ သိမ်းဆည်းနိုင်သော container (သိုလှောင်ခန်း) တစ်ခုဖြစ်ပါသည်။ Database တစ်ခုတွင် tables, views, stored procedures, functions, indexes စသည့် database objects များပါဝင်ပါသည်။ Database သည် data များကိုဗဟိုချုပ်ကိုင်မှုရှိရှိ စီမံနိုင်ရန်၊ လုံခြုံစေရန်နှင့် ပြန်လည်ရယူရလွယ်ကူစေရန်အတွက် အသုံးပြုပါသည်။

## Database vs Schema vs Table

ဤအခေါ်အဝေါ်သုံးခုကိုခွဲခြားနားလည်ထားရန် လိုအပ်ပါသည်-

- **Database**: Server ပေါ်ရှိ အကြီးဆုံး container ။ ၎င်းတွင် schema များနှင့် ၎င်းတို့၏ objects များအားလုံးပါဝင်ပါသည်။
- **Schema**: Database အတွင်းရှိ logical grouping unit တစ်ခုဖြစ်သည်။ Tables များကို schema အလိုက်စုဖွဲ့နိုင်ပါသည်။ Default schema မှာ dbo (SQL Server) သို့မဟုတ် public (PostgreSQL) ဖြစ်ပါသည်။
- **Table**: အချက်အလက်များကိုတကယ်သိမ်းဆည်းသော rows နှင့် columns ပုံစံရှိသည့် object ဖြစ်ပါသည်။

## CREATE DATABASE Command

### Basic Syntax (SQL Server)
```sql
-- ရိုးရိုး database ဆောက်ခြင်း
CREATE DATABASE ShopDB;

-- Parameters များဖြင့် database ဆောက်ခြင်း
CREATE DATABASE ShopDB
ON PRIMARY (
    NAME = 'ShopDB_Data',
    FILENAME = 'C:\\Program Files\\Microsoft SQL Server\\MSSQL16.MSSQLSERVER\\MSSQL\\DATA\\ShopDB.mdf',
    SIZE = 100MB,
    MAXSIZE = 1GB,
    FILEGROWTH = 100MB
)
LOG ON (
    NAME = 'ShopDB_Log',
    FILENAME = 'C:\\Program Files\\Microsoft SQL Server\\MSSQL16.MSSQLSERVER\\MSSQL\\DATA\\ShopDB_log.ldf',
    SIZE = 50MB,
    MAXSIZE = 500MB,
    FILEGROWTH = 50MB
);
```

### ရှင်းလင်းချက်
အထက်ပါ create database statement တွင်-
- **ON PRIMARY**: Data file (.mdf) အတွက် configuration ဖြစ်ပါသည်။
- **NAME**: File ၏ logical name (SQL Server အတွင်းသုံးမည့် name)။
- **FILENAME**: Disk ပေါ်တွင် file တည်ရှိမည့် physical path။
- **SIZE**: File ၏ initial size (စတင်သတ်မှတ်မည့်အရွယ်အစား)။
- **MAXSIZE**: File ၏ maximum size (အများဆုံးကြီးထွားနိုင်သောအရွယ်အစား)။
- **FILEGROWTH**: File အလိုအလျောက်ကြီးထွားနှုန်း (auto-growth setting)။
- **LOG ON**: Transaction log file (.ldf) အတွက် configuration။

### PostgreSQL တွင် Database ဆောက်ခြင်း
```sql
-- PostgreSQL
CREATE DATABASE shopdb
    WITH ENCODING 'UTF8'
    OWNER postgres
    CONNECTION LIMIT 100;
```

### MySQL တွင် Database ဆောက်ခြင်း
```sql
-- MySQL
CREATE DATABASE shopdb
    CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci;
```

## System Databases (SQL Server)

SQL Server တွင် system databases ၄ ခုပါဝင်ပြီး server ၏လည်ပတ်မှုအတွက် မရှိမဖြစ်လိုအပ်ပါသည်-

1. **master Database**: Server-level system information အားလုံးကိုသိမ်းဆည်းပါသည်။ Login များ, linked servers, endpoints, system configuration settings များပါဝင်ပါသည်။ master database ပျက်စီးပါက server လုံးဝအလုပ်မလုပ်တော့ပါ။

2. **model Database**: New database များအတွက် template အဖြစ်ဆောင်ရွက်ပါသည်။ model database ကိုပြင်ဆင်ပါက ၎င်းနောက်ဆောက်သမျှ database အားလုံးတွင် ပါဝင်သွားပါသည်။

3. **msdb Database**: SQL Server Agent (scheduling jobs, alerts), backup/restore history, SSIS package storage များအတွက်သုံးပါသည်။

4. **tempdb Database**: Temporary objects များအတွက်သုံးပါသည်။ Temporary tables, table variables, cursor work tables, row versioning များပါဝင်ပါသည်။ SQL Server restart ချတိုင်း tempdb ကိုအသစ်ပြန်ဆောက်ပါသည်။

## Database Options များ

```sql
-- Database စာရင်းကြည့်ရှုခြင်း
EXEC sp_databases;

-- Database ကိုပြောင်းလဲအသုံးပြုခြင်း
USE ShopDB;

-- Database properties ကြည့်ရှုခြင်း
SELECT * FROM sys.databases WHERE name = 'ShopDB';

-- Database size ကြည့်ရှုခြင်း
EXEC sp_spaceused;
```

## Database အမျိုးအစားများ

### 1. Relational Database (RDBMS)
Table-based, ACID compliant, structured data — SQL Server, PostgreSQL, MySQL, Oracle

### 2. NoSQL Database
Document-based (MongoDB), Key-value (Redis), Column-family (Cassandra), Graph (Neo4j)

### 3. In-Memory Database
Data အားလုံးကို RAM ထဲမှာသိမ်းပြီး အလွန်မြန်ဆန်သည် — Redis, SAP HANA

### 4. Cloud Database
Cloud provider မှ manage လုပ်ပေးသည် — Azure SQL Database, Amazon RDS, Google Cloud SQL

## Database Design အခြေခံမူများ

1. **Naming Convention**: Database name များသည် meaningful ဖြစ်ရမည်။ Clear, descriptive name ကိုသုံးပါ။

2. **Normalization**: Data redundancy ကိုလျှော့ချရန် normalization (1NF, 2NF, 3NF) ကိုလိုက်နာပါ။

3. **Collation Setting**: Language/character set sorting အတွက်သင့်တော်သော collation ကိုရွေးချယ်ပါ။

4. **Recovery Model**: Full, Simple, Bulk-Logged recovery models များမှသင့်တော်ရာရွေးပါ။

## လေ့ကျင့်ခန်း

1. 'LibraryDB' ဆိုသော database တစ်ခုဆောက်ပါ (သင့်တော်သော file paths များဖြင့်)။
2. System databases များ၏ list ကိုကြည့်ရှုပါ။
3. သင်ဆောက်ထားသော database ၏ properties များကိုစစ်ဆေးပါ။
4. Database ကို alter လုပ်၍ size ကိုချဲ့ပါ (ALTER DATABASE)။

## Database Design နှင့် Planning (အသေးစိတ်ရှင်းလင်းချက်)

Database တစ်ခုကိုမဆောက်မီ အောက်ပါအချက်များကိုကြိုတင်စဉ်းစားရန်လိုအပ်ပါသည်-

### Database Design Process (ဒေတာဘေ့စ်ဒီဇိုင်းလုပ်ငန်းစဉ်)

၁။ Requirements Analysis — မည်သည့် data များကိုသိမ်းဆည်းမည်၊ မည်သို့အသုံးပြုမည်ကိုဆန်းစစ်ပါ
၂။ Conceptual Design — Entity-Relationship Diagram (ERD) ဆွဲပါ
၃။ Logical Design — Tables, columns, relationships များကိုသတ်မှတ်ပါ
၄။ Normalization — Data redundancy ကိုလျှော့ချရန် normalization လုပ်ပါ
၅။ Physical Design — Data types, indexes, constraints များကိုသတ်မှတ်ပါ

### Database Naming Conventions (အမည်ပေးနည်းစနစ်များ)

ကောင်းမွန်သော naming convention သည် database ၏ readability နှင့် maintainability ကိုများစွာအထောက်အကူပြုပါသည်။

**Database Name:** CamelCase သို့မဟုတ် Snake Case သုံးပါ။ ဥပမာ — ShopDB, shop_db

**Table Name:** Plural သုံးလေ့ရှိသည် — Customers, Products, Orders

**Column Name:** Descriptive ဖြစ်ရမည်။ ဥပမာ — CustomerID, FirstName, OrderDate

### SQL Server File Architecture (ဖိုင်တည်ဆောက်ပုံ)

SQL Server သည် database တစ်ခုအတွက် file သုံးမျိုးကိုအသုံးပြုပါသည်-

**1. Primary Data File (.mdf)** — Database ၏အဓိက data file ဖြစ်ပြီး system tables များနှင့် user objects များကိုသိမ်းဆည်းပါသည်

**2. Secondary Data File (.ndf)** — Optional data file ဖြစ်ပါသည်။ Database ကြီးမားပါက data များကို disk များစွာပေါ်ခွဲသိမ်းရန်သုံးပါသည်

**3. Transaction Log File (.ldf)** — All transactions များကိုမှတ်တမ်းတင်ပါသည်။ Recovery နှင့် rollback အတွက်အရေးကြီးပါသည်

### Database Recovery Models (ပြန်လည်ရယူနိုင်မှုပုံစံများ)

SQL Server တွင် recovery model သုံးမျိုးရှိပါသည်-

**1. Full Recovery Model** — All transactions များကို log file တွင်အပြည့်အဝမှတ်တမ်းတင်ပါသည်။ Point-in-time recovery လုပ်နိုင်ပါသည်။ Production databases များအတွက်သင့်တော်ပါသည်။

**2. Simple Recovery Model** — Log ကို automatically truncate လုပ်ပါသည်။ Point-in-time recovery မလုပ်နိုင်ပါ။ Development/test databases များအတွက်သင့်တော်ပါသည်။

**3. Bulk-Logged Recovery Model** — Bulk operations များကို minimal log လုပ်ပါသည်။ Large data import လုပ်ချိန်တွင်ယာယီသုံးနိုင်ပါသည်။

### Database Size Planning

Database တစ်ခု၏အရွယ်အစားကိုခန့်မှန်းရန် — Row Size x Row Count x 1.5 (overhead) ကိုတွက်ပါ။

ဥပမာ — Customers table တွင် CustomerID (INT, 4 bytes), Name (VARCHAR(100), avg 50), Email (VARCHAR(150), avg 30), overhead 12 bytes — total ~106 bytes per row, 1 million rows = ~106 MB

### Database ဆိုင်ရာအရေးကြီးသော System Functions များ

```sql
-- Database size ကြည့်ရန်
EXEC sp_spaceused;

-- All database sizes
SELECT d.name, SUM(CAST(m.size AS BIGINT)) * 8 / 1024 AS SizeMB
FROM sys.databases d
JOIN sys.master_files m ON d.database_id = m.database_id
GROUP BY d.name ORDER BY SizeMB DESC;
```

### လက်တွေ့လေ့ကျင့်ခန်း

၁။ 'ECommerceDB' database ကိုဆောက်ပါ (data file 500MB, max 2GB, growth 100MB)
၂။ Log file ကို 100MB, max 500MB, growth 50MB ထားပါ
၃။ Recovery model ကို Full ထားပါ
၄။ Database properties များကိုစစ်ဆေးပါ
၅။ Tables များစတင်ဆောက်ပါ

### Database Management Best Practices

**1. Regular Backups** — Database ကိုပုံမှန် backup လုပ်ပါ။ Full backup (weekly), Differential backup (daily), Transaction log backup (hourly) စသည်ဖြင့်စီစဉ်ပါ။

**2. Performance Monitoring** — Query performance, disk space, CPU usage များကိုပုံမှန်စောင့်ကြည့်ပါ။ SQL Server Management Studio ၏ Activity Monitor ကိုသုံးနိုင်ပါသည်။

**3. Index Maintenance** — Index fragmentation ကိုစစ်ဆေးပြီး rebuild/reorganize လုပ်ပါ။

**4. Security Hardening** — Least privilege principle ကိုလိုက်နာပါ။ Users များကိုလိုအပ်သော permission အနည်းဆုံးသာပေးပါ။

**5. Documentation** — Database schema, stored procedures, security settings များကို document လုပ်ထားပါ။
