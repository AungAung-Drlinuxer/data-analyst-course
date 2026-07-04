# Module 1: SQL အခြေခံသဘောတရား (Introduction to SQL)

## SQL ဆိုတာဘာလဲ?

SQL (Structured Query Language) ဆိုသည်မှာ Relational Database Management System (RDBMS) များတွင် data များကို စီမံခန့်ခွဲရန်အတွက် အသုံးပြုသော Standard Programming Language တစ်ခုဖြစ်ပါသည်။ SQL ကို ၁၉၇၀ ပြည့်နှစ်များတွင် IBM မှ တီထွင်ခဲ့ပြီး ယနေ့အချိန်အထိ Database Management ၏ အဓိကဘာသာစကားအဖြစ် တည်ရှိနေပါသည်။

SQL သည် အောက်ပါ command များကို အသုံးပြု၍ data များကို စီမံခန့်ခွဲနိုင်ပါသည်-

| Operation | Description | SQL Command |
|-----------|-------------|-------------|
| **Create** | Database/Table အသစ်ဆောက်ခြင်း | CREATE |
| **Read (Retrieve)** | ဒေတာများကိုရှာဖွေခြင်း | SELECT |
| **Update** | ဒေတာဟောင်းများကိုပြင်ဆင်ခြင်း | UPDATE |
| **Delete** | ဒေတာများကိုဖျက်ခြင်း | DELETE / DROP |

SQL ကို CRUD Operations (Create, Read, Update, Delete) ဟုလည်း ခေါ်ဆိုပါသည်။ ဤလုပ်ငန်းလေးမျိုးသည် database application အားလုံး၏ အခြေခံဖြစ်ပါသည်။

## RDBMS (Relational Database Management System)

RDBMS ဆိုသည်မှာ Table များဖြင့် ဒေတာကိုသိမ်းဆည်းပြီး Table များအကြား Relationship (ဆက်သွယ်ချက်) များထားရှိနိုင်သော Database System ဖြစ်ပါသည်။ RDBMS ၏ အဓိကအားသာချက်မှာ data integrity ကိုထိန်းသိမ်းနိုင်ပြီး redundant data များကိုလျှော့ချနိုင်ခြင်းဖြစ်ပါသည်။

### လူသုံးများသော RDBMS များ

1. **Microsoft SQL Server** — Enterprise-grade database, Windows ecosystem တွင်အသုံးများသည်။ လုပ်ငန်းကြီးများအတွက် သင့်တော်ပြီး rich feature set ရှိပါသည်။
2. **PostgreSQL** — Open-source database, Advanced features များစွာပါဝင်သည်။ JSON, Array, Geographic data များကိုပါ support လုပ်ပါသည်။
3. **MySQL** — Open-source, Web applications များတွင်အသုံးများသည်။ Facebook, YouTube, Twitter တို့ကအသုံးပြုပါသည်။
4. **Oracle Database** — Enterprise-level, High performance, Large corporations များအတွက်သင့်တော်ပါသည်။
5. **SQLite** — Lightweight, File-based, Mobile apps နှင့် embedded systems များအတွက်သုံးပါသည်။

## SQL Command အမျိုးအစားများ

SQL Command များကို အဓိကအုပ်စုကြီး ၅ စုခွဲခြားနိုင်ပါသည်-

### 1. DDL (Data Definition Language)
Database object များ၏ structure ကိုသတ်မှတ်ရန်အသုံးပြုပါသည်။
- CREATE: Database, table, view, index စသည့် object များဆောက်ရန်
- ALTER: Object များ၏ structure ကိုပြင်ဆင်ရန်
- DROP: Object များကိုဖျက်ရန်
- TRUNCATE: Table ထဲမှ data အားလုံးကိုဖျက်ရန် (structure ကျန်ခဲ့)
- RENAME: Object အမည်ပြောင်းရန်

### 2. DML (Data Manipulation Language)
Table ထဲရှိ data များကိုစီမံရန်အသုံးပြုပါသည်။
- INSERT: Row အသစ်ထည့်ရန်
- UPDATE: Row များကိုပြင်ဆင်ရန်
- DELETE: Row များကိုဖျက်ရန်

### 3. DQL (Data Query Language)
Table ထဲမှ data များကိုရှာဖွေထုတ်ယူရန်။
- SELECT: Data များကိုရှာဖွေရန် (အသုံးအများဆုံး SQL command)

### 4. DCL (Data Control Language)
Database security အတွက်အသုံးပြုပါသည်။
- GRANT: User များကို permission ပေးရန်
- REVOKE: User များ၏ permission ကိုပြန်ရုပ်သိမ်းရန်

### 5. TCL (Transaction Control Language)
Transaction များကိုစီမံရန်အသုံးပြုပါသည်။
- BEGIN TRANSACTION: Transaction စတင်ရန်
- COMMIT: Transaction ကို save လုပ်ရန်
- ROLLBACK: Transaction ကို undo လုပ်ရန်
- SAVEPOINT: Transaction အတွင်း checkpoint သတ်မှတ်ရန်

## SQL Tools များ

SQL ကိုရေးသားရန်နှင့် execute လုပ်ရန်အတွက် tool အမျိုးမျိုးရှိပါသည်-

| Tool | Database Support | Platform | Free/Paid |
|------|-----------------|----------|-----------|
| SSMS (SQL Server Management Studio) | SQL Server | Windows | Free |
| DBeaver | All major databases | Cross-platform | Free/Paid |
| Azure Data Studio | SQL Server, PostgreSQL | Cross-platform | Free |
| pgAdmin | PostgreSQL | Cross-platform | Free |
| MySQL Workbench | MySQL | Cross-platform | Free |
| DataGrip | All major databases | Cross-platform | Paid |

DBeaver သည် cross-platform အသုံးပြုနိုင်ပြီး database အမျိုးမျိုးကို GUI ဖြင့်အလွယ်တကူကြည့်ရှုနိုင်သောကြောင့် စတင်လေ့လာသူများအတွက် အထူးအကြံပြုလိုပါသည်။

## နမူနာ SQL Query များ

```sql
-- Hello World SQL
SELECT 'Hello, World!' AS Greeting;
/* Result: Hello, World! */

-- Database စာရင်းကြည့်ရှုခြင်း (SQL Server)
SELECT name, database_id, create_date FROM sys.databases;

-- Server version ကြည့်ရှုခြင်း
SELECT @@VERSION AS [SQL Server Version];

-- Current date/time ကြည့်ရှုခြင်း
SELECT GETDATE() AS CurrentDateTime;
```

## SQL Syntax အခြေခံစည်းမျဉ်းများ

1. **Case-Insensitive** — SQL keywords များသည် case-sensitive မဟုတ်ပါ။ SELECT, select, Select အားလုံးအလုပ်လုပ်ပါသည်။ သို့သော် SQL keywords များကို UPPERCASE ဖြင့်ရေးသားခြင်းသည် standard convention ဖြစ်ပါသည်။

2. **Semicolon (;)** — SQL statement တစ်ခုစီကိ် semicolon ဖြင့်အဆုံးသတ်ရပါသည်။ ၎င်းသည် statement များကိုရှင်းရှင်းလင်းလင်းခွဲခြားပေးပါသည်။

3. **Comments** — SQL တွင် comment ရေးရန်နည်းလမ်းနှစ်မျိုးရှိပါသည်-
   - Single line comment: -- (double dash)
   - Multi-line comment: /* ... */

4. **Whitespace** — SQL သည် whitespace (space, tab, newline) များကို ignore လုပ်ပါသည်။ Query များကိုရှင်းရှင်းလင်းလင်းဖတ်ရန် indentation နှင့် line breaks များသုံးနိုင်ပါသည်။

5. **String Literals** — String တန်ဖိုးများကို single quotes ('') ဖြင့်ရေးရပါသည်။

## SQL လေ့လာရန်အကြံပြုချက်များ

SQL ကိုလေ့လာရာတွင် အောက်ပါအချက်များကိုလိုက်နာပါက ပိုမိုမြန်ဆန်စွာတတ်မြောက်နိုင်ပါသည်-

1. **ကိုယ်တိုင် Query ရေးပါ** — နမူနာများကို copy/paste လုပ်မည့်အစား ကိုယ်တိုင်ရေးပါ။
2. **Sample Database ဆောက်ပါ** — တကယ့် database ဆောက်ပြီး data ထည့်ကာလေ့ကျင့်ပါ။
3. **Error များမှသင်ယူပါ** — Error message များကိုဖတ်တတ်အောင်လုပ်ပါ။
4. **Execution Plan ကိုလေ့လာပါ** — Query ဘယ်လိုအလုပ်လုပ်သည်ကိုနားလည်ပါ။
5. **Online Resources သုံးပါ** — Stack Overflow, W3Schools, MSSQLTips များမှအကူအညီယူပါ။

## အမေးများသောမေးခွန်းများ

**မေး: SQL နှင့် NoSQL ကွာခြားချက်ကဘာလဲ?**
ဖြေ: SQL database များသည် table-based, structured data, ACID compliant ဖြစ်ပြီး NoSQL database များသည် document/key-value/graph based, schema-less, flexible, horizontal scaling ပိုကောင်းပါသည်။

**မေး: SQL ကိုဘယ်သူတွေသုံးလဲ?**
ဖြေ: Data Analyst, Data Scientist, Backend Developer, DBA, Business Analyst, Platform Engineer စသည့် data နှင့်ဆက်စပ်သောသူအားလုံးနီးပါးသုံးပါသည်။

**မေး: SQL အခြေခံတတ်ရန်ဘယ်လောက်ကြာမလဲ?**
ဖြေ: အခြေခံ (SELECT, WHERE, JOIN) ကို ၁-၂ ပတ်၊ အဆင့်မြင့် (Window Functions, CTEs) ကို ၃-၄ ပတ်၊ လက်တွေ့ကျွမ်းကျင်ရန် ၂-၃ လခန့်ကြာတတ်ပါသည်။

## လေ့ကျင့်ခန်း

1. SQL Server (သို့) PostgreSQL တစ်ခုခုကို install လုပ်ပါ။
2. DBeaver ကို install လုပ်ပြီး database ကိုချိတ်ဆက်ပါ။
3. အောက်ပါ query ကို run ကြည့်ပါ- SELECT 'My First SQL Query' AS Message;
4. Server/Database version ကိုကြည့်ရန် query ရေးပါ။
5. သင်လေ့လာခဲ့သော SQL commands အမျိုးအစား ၅ မျိုးကိုစာရင်းပြုစုပါ။




## SQL ၏အရေးပါပုံနှင့်အသုံးချမှုများ (အသေးစိတ်)

SQL သည်ယနေ့ခေတ် Data-driven world တွင် မရှိမဖြစ်လိုအပ်သောကျွမ်းကျင်မှုတစ်ခုဖြစ်ပါသည်။ အောက်ပါနယ်ပယ်များတွင် SQL ကိုကျယ်ကျယ်ပြန့်ပြန့်အသုံးပြုပါသည်-

### Web Application များတွင် SQL ၏အခန်းကဏ္ဍ

Website နှင့် mobile application တိုင်းနီးပါးတွင် database ရှိပါသည်။ ဥပမာ-
- Facebook သည် users, posts, likes, comments များကို SQL database တွင်သိမ်းဆည်းပါသည်
- E-commerce site များ (Shopee, Lazada) သည် products, orders, payments များကို SQL database တွင်သိမ်းဆည်းပါသည်
- Banking applications များသည် accounts, transactions, balances များကို SQL database တွင်သိမ်းဆည်းပါသည်

### Data Analysis တွင် SQL ၏အရေးပါမှု

Data Analyst များသည် SQL ကို၎င်းတို့၏အဓိက tool တစ်ခုအနေဖြင့်အသုံးပြုပါသည်-
- ရောင်းအားဒေတာများကိုခွဲခြမ်းစိတ်ဖြာရန်
- Customer behavior ကိုလေ့လာရန်
- Business trends များကိုရှာဖွေရန်
- Reports များထုတ်ရန်အတွက်

### Database Administrator (DBA) ၏အခန်းကဏ္ဍ

DBA များသည် database server များကိုစီမံခန့်ခွဲရန် SQL ကိုအသုံးပြုပါသည်-
- Database performance ကိုစောင့်ကြည့်ရန်
- Backup နှင့် recovery လုပ်ရန်
- Security နှင့် user permissions များစီမံရန်
- Database maintenance လုပ်ရန်

### SQL ၏အားသာချက်များ

၁။ **Standard Language** — SQL သည် ANSI နှင့် ISO standard ဖြစ်ပြီး database အားလုံးနီးပါးတွင် အလုပ်လုပ်ပါသည်
၂။ **Declarative Language** — ဘယ်လိုရယူမည်ကိုမဟုတ်ဘဲ ဘာကိုရယူမည်ကိုသာရေးရန်လိုပါသည်
၃။ **Easy to Learn** — အခြား programming languages များနှင့်ယှဉ်ပါက SQL သည်သင်ယူရလွယ်ကူပါသည်
၄။ **Powerful** — Complex queries များဖြင့် data အမြောက်အမြားကိုလွယ်ကူစွာရှာဖွေနိုင်ပါသည်
၅။ **Portable** — တစ်ကြိမ်ရေးထားသော SQL query ကို database အမျိုးမျိုးတွင်အသုံးပြုနိုင်ပါသည်

### SQL အသုံးပြုသောအလုပ်အကိုင်များ

| အလုပ်အကိုင် | SQL အသုံးပြုပုံ | ပျမ်းမျှလစာ |
|-------------|-----------------|--------------|
| Data Analyst | Data ထုတ်ယူခြင်း၊ report ဆွဲခြင်း | မြင့် |
| Data Scientist | Data exploration, feature engineering | အလွန်မြင့် |
| Backend Developer | API data access, CRUD operations | မြင့် |
| Database Administrator (DBA) | Server management, tuning | အလွန်မြင့် |
| BI Developer | Data warehouse, ETL, reporting | မြင့် |
| QA Engineer | Test data setup, data validation | အလယ် |

### SQL Tools များအကြောင်းအသေးစိတ်

**1. DBeaver** — Cross-platform tool ဖြစ်ပြီး database အမျိုးမျိုး (MySQL, PostgreSQL, SQL Server, Oracle) ကိုချိတ်ဆက်နိုင်ပါသည်။ Free community version ရှိပါသည်။ GUI ဖြင့် database structure ကိုကြည့်ရှုနိုင်ပြီး query များကိုရေးသား run နိုင်ပါသည်။

**2. SQL Server Management Studio (SSMS)** — SQL Server အတွက် Microsoft ၏ official tool ဖြစ်ပါသည်။ Windows တွင်သာ run နိုင်ပါသည်။ Enterprise-level features များစွာပါဝင်ပါသည်။

**3. Azure Data Studio** — Cross-platform tool ဖြစ်ပြီး SQL Server နှင့် PostgreSQL ကိုအဓိကထားပါသည်။ Lightweight ဖြစ်ပြီး notebook support ပါရှိပါသည်။

**4. pgAdmin** — PostgreSQL အတွက် open-source tool ဖြစ်ပါသည်။ Web-based interface ဖြစ်ပြီး Linux/Windows/Mac အားလုံးတွင်သုံးနိုင််ပါသည်။

**5. MySQL Workbench** — MySQL အတွက် official GUI tool ဖြစ်ပါသည်။ Database design, development, administration အားလုံးလုပ်ဆောင်နိုင်ပါသည်။

### SQL လေ့လာရန်နည်းလမ်းကောင်းများ

၁။ **Practice Daily** — SQL သည်လက်တွေ့လေ့ကျင့်မှုများမှတစ်ဆင့်အကောင်းဆုံးသင်ယူနိုင်ပါသည်
၂။ **Sample Database ဆောက်ပါ** — ကိုယ်ပိုင် database ဆောက်ပြီး data ထည့်ကာ query များရေးပါ
၃။ **Online Platforms သုံးပါ** — LeetCode, HackerRank, SQLZoo စသည့် platform များတွင်လေ့ကျင့်ပါ
၄။ **Real Problems ကိုဖြေရှင်းပါ** — ကိုယ့် work ထဲမှာ SQL ကိုအသုံးပြုပြီး real problems များကိုဖြေရှင်းပါ
၅။ **Documentation ကိုဖတ်ပါ** — Official documentation များမှ အသေးစိတ်လေ့လာပါ
၆။ **Community များတွင်ပါဝင်ပါ** — Stack Overflow, Reddit, Telegram groups များတွင်မေးမြန်းလေ့လာပါ

### သာမန်အမှားများနှင့်ရှောင်ရှားနည်း

| အမှား | ရှင်းလင်းချက် | ဖြေရှင်းနည်း |
|-------|-------------|-------------|
| SELECT * သုံးခြင်း | Column အားလုံးကိုဆွဲထုတ်ပါသည် | လိုအပ်သော column များကိုသာရွေးပါ |
| NULL ကို = ဖြင့်နှိုင်းယှဉ်ခြင်း | NULL = NULL သည် false ဖြစ်ပါသည် | IS NULL ကိုသုံးပါ |
| String ကို quote မေ့ခြင်း | Syntax error ဖြစ်ပါသည် | 'single quotes' ကိုသုံးပါ |
| JOIN မေ့ခြင်း | Cartesian product ဖြစ်ပါသည် | ON clause ကိုသေချာရေးပါ |
| Semicolon မေ့ခြင်း | Statement မပြီးဆုံးပါ | ; ကိုအဆုံးမှာထည့်ပါ |
