# ☁️ Microsoft Fabric သင်ရိုး — Modern Data Platform

> **သင်ခန်းစာ ၁၅ ခု** | **လက်တွေ့ပရောဂျက်များ** | **End-to-End Data Analytics**

---

## 📖 Microsoft Fabric ဆိုတာဘာလဲ?

**Microsoft Fabric** သည် Microsoft ၏ **All-in-One Data Analytics Platform** တစ်ခုဖြစ်ပြီး —
- **Data Lakehouse** — Data Lake + Data Warehouse ပေါင်းစပ်ထားခြင်း
- **Data Factory** — ETL/ELT Pipeline များတည်ဆောက်ခြင်း
- **Data Engineering** — Spark ဖြင့် Big Data တွက်ချက်ခြင်း
- **Data Warehouse** — Enterprise-grade SQL Analytics
- **Real-time Analytics** — Stream Data များကို ချက်ချင်းခွဲခြမ်းစိတ်ဖြာခြင်း
- **Power BI Integration** — Direct Lake Mode ဖြင့် မြန်ဆန်သော BI


---

## 📑 Fabric သင်ခန်းစာ အသေးစိတ် (Module 1-15)

### 🔰 အခြေခံပိုင်း (Foundation) — Module 1-4

| Module | ခေါင်းစဉ် | သင်ယူရမည့်အကြောင်းအရာ |
|--------|-----------|----------------------|
| **1** | Introduction to Microsoft Fabric | Fabric ဆိုတာဘာလဲ၊ OneLake, SaaS Platform, Licensing |
| **2** | Creating Azure & Fabric Account | Azure Subscription, Fabric Capacity (F2-F64), Free Trial Setup |
| **3** | Hierarchy in Fabric | Tenant → Capacity → Workspace → Item — အဆင့်ဆင့်တည်ဆောက်ပုံ |
| **4** | Fabric Interface | Portal Navigation, Settings, Monitor Hub, Admin Center |

### 🏗️ Lakehouse & Data Factory — Module 5-11

| Module | ခေါင်းစဉ် | သင်ယူရမည့်အကြောင်းအရာ |
|--------|-----------|----------------------|
| **5** | Lakehouse | OneLake Architecture, Shortcuts, Tables (Managed vs External), File Support |
| **6** | Data Factory | Pipeline Orchestration, Activities, Connectors — Ingestion အခြေခံ |
| **7** | Data Pipeline — Copy Data Activity | Source → Sink, Schema Mapping, Incremental Load, Performance Tuning |
| **8** | SQL Server Integration | On-premises SQL Server → Fabric, Gateway Setup, VPN/Direct Connect |
| **9** | Data Load Behaviour | Full Load vs Incremental Load, Append vs Upsert, Schema Drift |
| **10** | Data Pipeline — Activities | Copy, Notebook, Stored Procedure, Delete, If Condition, ForEach, Wait |
| **11** | DataFlow Gen 2 | Power Query Online, M Language, Dataflows vs Pipelines, Compute Settings |

### 🏛️ Warehouse & BI — Module 12-14

| Module | ခေါင်းစဉ် | သင်ယူရမည့်အကြောင်းအရာ |
|--------|-----------|----------------------|
| **12** | Warehouse | Dedicated SQL Warehouse, T-SQL Support, Views, Stored Procedures, Security |
| **13** | Power BI Integration | Direct Lake Mode, Semantic Models, Auto-create Reports from Lakehouse |
| **14** | Data Engineering — Spark | PySpark, Spark SQL, Notebooks, Delta Lake, Optimize/Vacuum |

### 🏁 နောက်ဆုံးပိုင်း — Module 15

| Module | ခေါင်းစဉ် | သင်ယူရမည့်အကြောင်းအရာ |
|--------|-----------|----------------------|
| **15** | Projects | End-to-End Data Pipeline Projects — Ingestion → Transformation → Analytics → Reporting |

---

## 🎯 Module 1-15 အကျဉ်းချုပ်

### Module 1: Introduction to Microsoft Fabric
```
Fabric = OneLake (Storage)
       + Data Factory (ETL)
       + Synapse Data Engineering (Spark)
       + Synapse Data Warehouse (SQL)
       + Synapse Real-Time Analytics (Streaming)
       + Power BI (Visualization)
```
- SaaS (Software as a Service) — Manage လုပ်စရာမလို
- OneLake — Single Copy of Data, Multi-cloud
- Capacity-based Pricing (F SKUs)

### Module 2: Creating Azure & Fabric Account
- Azure Portal → Microsoft Fabric → Enable Trial Capacity
- F64 Free Trial (60 days)
- Fabric Admin Portal Setup

### Module 3: Hierarchy in Fabric
```
Tenant (Azure AD)
  └── Capacity (Compute Resource)
       └── Workspace (Project Boundary)
            └── Items (Lakehouse, Notebook, Pipeline, Report)
```
- Capacity = Compute Resource
- Workspace = Project Workspace

### Module 4: Fabric Interface
- **Home** — Landing Page, Quick Actions
- **Create** — New Items (Lakehouse, Dataflow, Notebook...)
- **Monitor** — Job Runs, Pipeline Status
- **Settings** — Workspace, Security, Connections
- **Admin Portal** — Capacity Management, Tenant Settings

### Module 5: Lakehouse
```
Lakehouse = Data Lake (Parquet/CSV/JSON)
          + Delta Table (Managed)
          + SQL Endpoint (Read via T-SQL)
          + Shortcuts (External Data)
```
- OneLake Shortcuts ဖြင့် External Data ကို Copy လုပ်စရာမလို
- Delta Lake Format — ACID Transactions, Versioning
- Tables: Managed (Fabric က Manage) vs External (Source မှာပဲရှိ)

### Module 6: Data Factory
- **Pipeline** — Logical Container of Activities
- **Activity** — Copy, Notebook, Stored Procedure, Delete
- **Trigger** — Schedule, Tumbling Window, Event-based
- **Connector** — 200+ (Azure, AWS, GCP, On-premises)

### Module 7: Data Pipeline — Copy Data Activity
```
Source (SQL Server) 
  → Copy Activity 
    → Sink (Lakehouse Files/Tables)

Optional: Schema Mapping, Column Mappings
```
- Staging Mode — Large Data Transfer အတွက်
- Incremental Loading — Watermark Column သုံး၍
- Fault Tolerance — Skip error rows

### Module 8: SQL Server Integration
- **Gateway (On-premises)** — On-prem SQL Server အတွက်
- **Gateway (VNet)** — Azure VNet အတွင်းရှိ SQL Server
- **Direct Connect** — Azure SQL Database
- **Authentication** — SQL Auth, Windows Auth, AAD

### Module 9: Data Load Behaviour
| Load Type | Description | When to Use |
|-----------|------------|-------------|
| **Full Load** | Data အားလုံးကို ပြန်ဖြည့်ခြင်း | First time, Small tables, Schema change |
| **Incremental Load** | အသစ်ထည့်ထားသော Data များသာ | Large tables, Daily jobs |
| **Append** | Row အသစ်များကို ထည့်ခြင်း | Logs, Transactions |
| **Upsert** | Update + Insert (Merge) | Slowly Changing Dimensions |

### Module 10: Data Pipeline Activities
| Activity | Purpose | Description |
|----------|---------|-------------|
| Copy Data | Data Transfer | Copy data between sources |
| Notebook | Run Spark Job | Execute Spark notebook |
| Stored Procedure | Execute SQL | Database Migration Script |
| Delete | Clean Up | Remove old files |
| If Condition | Conditional Branch | Branch logic |
| ForEach | Loop | Iterate over items |
| Wait | Delay | Pause execution |

### Module 11: DataFlow Gen 2
- Power Query Online — Low-code Data Transformation
- 300+ Transformations — Merge, Append, Pivot, Unpivot, etc.
- **Compute Settings** — Serverless (Auto-scale) vs Provisioned
- **Dataflows vs Pipelines** — Dataflow = Transformation-focused, Pipeline = Orchestration-focused

### Module 12: Warehouse
```
Warehouse = Lakehouse + 
           + Full T-SQL Support
           + Stored Procedures, Views
           + Cross-database Queries
           + Table Constraints (PK, FK, Unique)
           + ACID via Delta Lake
```
- **When to use Warehouse?** — Complex SQL logic, Stored procedures, Enterprise ETL
- **When to use Lakehouse?** — File-based, Spark, Machine Learning
- **Security** — Row-level Security (RLS), Column-level Security, Dynamic Data Masking

### Module 13: Power BI Integration
- **Direct Lake Mode** — No import, no query — Direct from Delta Lake
- **Automatic Report** — One-click from Lakehouse
- **Semantic Model** — DAX Measures, Relationships, Hierarchies
- **Composite Models** — Direct Lake + Import + Direct Query

```
Traditional:           Power BI ← Import → SQL Server
Fabric Direct Lake:   Power BI ← Direct → Delta Lake (1-2 sec refresh!)
```

### Module 14: Data Engineering — Spark
```python
# PySpark Example
df = spark.read.format("delta").load("Tables/sales")
df.createOrReplaceTempView("sales")

# Spark SQL
result = spark.sql("""
    SELECT region, SUM(amount) as total_sales
    FROM sales
    GROUP BY region
""")

# Delta Operations
df.write.format("delta").mode("overwrite").saveAsTable("aggregated_sales")
```

- **Notebooks** — Interactive Development (Jupyter-style)
- **Spark Jobs** — Scheduled Batch Processing
- **Optimize** — Bin compaction (small file merging)
- **Vacuum** — Old file cleanup
- **Delta Live Tables** — Streaming + Batch Pipeline

### Module 15: Projects
Fabric Projects တွင် အောက်ပါတို့ ပါဝင်ပါမည် —
1. **End-to-End Data Pipeline** — Ingestion → Transformation → Modeling → Reporting
2. **Real-time Analytics** — Streaming Data with Event Stream
3. **Data Warehouse Migration** — On-prem to Fabric
4. **Medallion Architecture** — Bronze → Silver → Gold Layers

---

## 🔗 SQL + Power BI + Fabric — ဆက်စပ်မှု

```
SQL (Source/Layer) 
  → Power BI (Visualization/Analytics)
    → Fabric (Platform/Orchestration)

Fabric က Pipeline တစ်ခုလုံးကို Orchestrate လုပ်ပါသည်။
SQL က Data ကို Store/Transform လုပ်ပါသည်။
Power BI က Data ကို Visualize/Analyze လုပ်ပါသည်။
```

---

## 🛠️ လိုအပ်သော Setup

| Tool/Service | Link | Cost |
|-------------|------|------|
| Microsoft Fabric Trial | https://app.fabric.microsoft.com | Free for 60 days (F64) |
| Azure Subscription | https://portal.azure.com | Free $200 Credit |
| SQL Server | Docker: `docker run ... mcr.microsoft.com/mssql/server` | Free (Developer Edition) |

---

## 📂 ဖိုင်တည်ဆောက်ပုံ

```
03-microsoft-fabric/
├── README.md              ← ဤဖိုင် — Fabric သင်ရိုးအကျဉ်းချုပ်
├── modules/
│   ├── 01-introduction.md
│   ├── 02-creating-account.md
│   ├── 03-hierarchy-in-fabric.md
│   ├── 04-fabric-interface.md
│   ├── 05-lakehouse.md
│   ├── 06-data-factory.md
│   ├── 07-data-pipeline-copy-activity.md
│   ├── 08-sql-server-integration.md
│   ├── 09-data-load-behaviour.md
│   ├── 10-data-pipeline-activities.md
│   ├── 11-dataflow-gen2.md
│   ├── 12-warehouse.md
│   ├── 13-power-bi-integration.md
│   ├── 14-data-engineering-spark.md
│   └── 15-projects.md
└── projects/
    ├── 01-end-to-end-pipeline/
    ├── 02-real-time-analytics/
    └── ...
```

---

> ➡️ **စတင်လေ့လာရန်** — `modules/01-introduction.md` ကိုဖွင့်ပါ။
