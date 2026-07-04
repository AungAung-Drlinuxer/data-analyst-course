# Module 7: Data Pipeline — Copy Data Activity

## Copy Activity ဆိုတာဘာလဲ?

Copy Data Activity သည် data ကို source မှ sink သို့ copy လုပ်သော activity ဖြစ်ပါသည်။ ၎င်းသည် Data Factory ၏အသုံးအများဆုံး activity ဖြစ်ပါသည်။

### Configuration

**Source Settings**:
- Source type: SQL Server, Blob, ADLS, etc.
- Query: Custom SQL or table selection
- Isolation level: Read committed, snapshot

**Sink Settings**:
- Sink type: Lakehouse files/tables
- Copy method: Bulk insert, BCP
- Table type: Managed/External

### Incremental Load Pattern

1. Get LastWatermark from control table
2. Copy WHERE Column > LastWatermark
3. Update Watermark with MAX(Column)
4. Repeat on schedule

### Performance Tips

- Staging mode for large transfers
- Parallel copy (degree of copy parallelism)
- Data compression during transfer
- Use PolyBase for large data warehouse loads


## Detailed Learning Content

### Core Concepts and Architecture

Microsoft Fabric ၏အဓိကအင်္ဂါရပ်များမှာ-

1. **OneLake** — Single, unified data lake that all Fabric workloads use. ဒေတာအားလုံးကိုတစ်နေရာတည်းတွင်သိမ်းဆည်းပြီး duplication မလိုအပ်ပါ။
2. **SaaS Platform** — Microsoft က infrastructure အားလုံးကိုစီမံပေးပါသည် (no servers to manage)
3. **Integrated Experiences** — Data Factory, Synapse, Power BI တို့သည်တစ်ခုတည်းသော platform တွင်အလုပ်လုပ်ပါသည်
4. **AI-Powered** — Copilot နှင့်အခြား AI features များပါဝင်ပါသည်

### Practical Workshop

**Lab 1: Create Your First Fabric Workspace**
1. Sign in to app.fabric.microsoft.com
2. Create a new workspace (MyFirstWorkspace)
3. Create a Lakehouse item
4. Upload sample data (CSV file)
5. Create a table from the CSV
6. Query the data using SQL endpoint

**Lab 2: Build a Pipeline**
1. Create a new pipeline
2. Add Copy Data activity
3. Configure source (SQL Server or sample)
4. Configure sink (Lakehouse)
5. Run the pipeline
6. Monitor the run

### Best Practices

| Area | Best Practice | Rationale |
|------|---------------|----------|
| Security | Use Azure AD authentication | Better than SQL auth |
| Performance | Use Medallion Architecture | Bronze → Silver → Gold |
| Cost | Monitor CU usage | Avoid unexpected bills |
| Development | Use Git integration | Version control |
| Testing | Separate Dev/Test/Prod workspaces | Safe deployments |

### Common Errors and Solutions

| Error | Cause | Resolution |
|-------|-------|------------|
| Capacity not found | Capacity paused or deleted | Check capacity status |
| Pipeline failed | Source not accessible | Check gateway and credentials |
| SQL timeout | Query too complex | Optimize query or increase timeout |
| Insufficient permissions | Wrong workspace role | Assign contributor role |
| Data mismatch | Schema mismatch | Review schema mapping |

### Step-by-Step Configuration

**Setting up Data Pipeline:**
1. Navigate to your workspace
2. Click New → Pipeline
3. Give pipeline a meaningful name
4. Add Copy Data activity from Activities pane
5. Configure Source tab:
   - Connection: Create new connection
   - Connection type: SQL Server
   - Server/Database: Enter details
   - Authentication: Windows/SQL/AAD
6. Configure Destination tab:
   - Connection: Your Lakehouse
   - Table: New table name
7. Configure Mapping tab:
   - Auto-map or manual mapping
8. Validate and Save
9. Run pipeline
10. Monitor run in Monitor hub

### Integration with Other Services

Fabric သည် Azure services အများအပြားနှင့်ပေါင်းစပ်အလုပ်လုပ်နိုင်ပါသည်-
- Azure Data Lake Storage Gen2 (shortcuts)
- Azure SQL Database (direct query)
- Azure Event Hubs (streaming)
- Azure Databricks (interoperability)
- Azure DevOps (CI/CD pipelines)
- Microsoft 365 (Copilot integration)

### Performance Optimization

1. **Use Delta Lake format** — Best performance for large-scale analytics
2. **Optimize Spark jobs** — Proper partitioning, caching
3. **Use Direct Lake** — Avoid import overhead for Power BI
4. **Schedule runs during off-peak** — Better resource availability
5. **Monitor CU consumption** — Identify expensive operations
6. **Use shortcuts instead of copying** — Save storage and time
7. **Vacuum old files** — Clean up unnecessary Delta versions

### Learning Path

1. ဤ module ၏ concept များကိုနားလည်အောင်လေ့လာပါ
2. Sample data ဖြင့်စမ်းသပ်ပါ
3. တကယ့် use case တစ်ခုအတွက်အသုံးချပါ
4. Performance testing လုပ်ပါ
5. Documentation ရေးပါ
6. Team နှင့် share လုပ်ပါ
## Detailed Learning Content

### Core Concepts and Architecture

Microsoft Fabric ၏အဓိကအင်္ဂါရပ်များမှာ-

1. **OneLake** — Single, unified data lake that all Fabric workloads use. ဒေတာအားလုံးကိုတစ်နေရာတည်းတွင်သိမ်းဆည်းပြီး duplication မလိုအပ်ပါ။
2. **SaaS Platform** — Microsoft က infrastructure အားလုံးကိုစီမံပေးပါသည် (no servers to manage)
3. **Integrated Experiences** — Data Factory, Synapse, Power BI တို့သည်တစ်ခုတည်းသော platform တွင်အလုပ်လုပ်ပါသည်
4. **AI-Powered** — Copilot နှင့်အခြား AI features များပါဝင်ပါသည်

### Practical Workshop

**Lab 1: Create Your First Fabric Workspace**
1. Sign in to app.fabric.microsoft.com
2. Create a new workspace (MyFirstWorkspace)
3. Create a Lakehouse item
4. Upload sample data (CSV file)
5. Create a table from the CSV
6. Query the data using SQL endpoint

**Lab 2: Build a Pipeline**
1. Create a new pipeline
2. Add Copy Data activity
3. Configure source (SQL Server or sample)
4. Configure sink (Lakehouse)
5. Run the pipeline
6. Monitor the run

### Best Practices

| Area | Best Practice | Rationale |
|------|---------------|----------|
| Security | Use Azure AD authentication | Better than SQL auth |
| Performance | Use Medallion Architecture | Bronze → Silver → Gold |
| Cost | Monitor CU usage | Avoid unexpected bills |
| Development | Use Git integration | Version control |
| Testing | Separate Dev/Test/Prod workspaces | Safe deployments |

### Common Errors and Solutions

| Error | Cause | Resolution |
|-------|-------|------------|
| Capacity not found | Capacity paused or deleted | Check capacity status |
| Pipeline failed | Source not accessible | Check gateway and credentials |
| SQL timeout | Query too complex | Optimize query or increase timeout |
| Insufficient permissions | Wrong workspace role | Assign contributor role |
| Data mismatch | Schema mismatch | Review schema mapping |

### Step-by-Step Configuration

**Setting up Data Pipeline:**
1. Navigate to your workspace
2. Click New → Pipeline
3. Give pipeline a meaningful name
4. Add Copy Data activity from Activities pane
5. Configure Source tab:
   - Connection: Create new connection
   - Connection type: SQL Server
   - Server/Database: Enter details
   - Authentication: Windows/SQL/AAD
6. Configure Destination tab:
   - Connection: Your Lakehouse
   - Table: New table name
7. Configure Mapping tab:
   - Auto-map or manual mapping
8. Validate and Save
9. Run pipeline
10. Monitor run in Monitor hub

### Integration with Other Services

Fabric သည် Azure services အများအပြားနှင့်ပေါင်းစပ်အလုပ်လုပ်နိုင်ပါသည်-
- Azure Data Lake Storage Gen2 (shortcuts)
- Azure SQL Database (direct query)
- Azure Event Hubs (streaming)
- Azure Databricks (interoperability)
- Azure DevOps (CI/CD pipelines)
- Microsoft 365 (Copilot integration)

### Performance Optimization

1. **Use Delta Lake format** — Best performance for large-scale analytics
2. **Optimize Spark jobs** — Proper partitioning, caching
3. **Use Direct Lake** — Avoid import overhead for Power BI
4. **Schedule runs during off-peak** — Better resource availability
5. **Monitor CU consumption** — Identify expensive operations
6. **Use shortcuts instead of copying** — Save storage and time
7. **Vacuum old files** — Clean up unnecessary Delta versions

### Learning Path

1. ဤ module ၏ concept များကိုနားလည်အောင်လေ့လာပါ
2. Sample data ဖြင့်စမ်းသပ်ပါ
3. တကယ့် use case တစ်ခုအတွက်အသုံးချပါ
4. Performance testing လုပ်ပါ
5. Documentation ရေးပါ
6. Team နှင့် share လုပ်ပါ
## Detailed Learning Content

### Core Concepts and Architecture

Microsoft Fabric ၏အဓိကအင်္ဂါရပ်များမှာ-

1. **OneLake** — Single, unified data lake that all Fabric workloads use. ဒေတာအားလုံးကိုတစ်နေရာတည်းတွင်သိမ်းဆည်းပြီး duplication မလိုအပ်ပါ။
2. **SaaS Platform** — Microsoft က infrastructure အားလုံးကိုစီမံပေးပါသည် (no servers to manage)
3. **Integrated Experiences** — Data Factory, Synapse, Power BI တို့သည်တစ်ခုတည်းသော platform တွင်အလုပ်လုပ်ပါသည်
4. **AI-Powered** — Copilot နှင့်အခြား AI features များပါဝင်ပါသည်

### Practical Workshop

**Lab 1: Create Your First Fabric Workspace**
1. Sign in to app.fabric.microsoft.com
2. Create a new workspace (MyFirstWorkspace)
3. Create a Lakehouse item
4. Upload sample data (CSV file)
5. Create a table from the CSV
6. Query the data using SQL endpoint

**Lab 2: Build a Pipeline**
1. Create a new pipeline
2. Add Copy Data activity
3. Configure source (SQL Server or sample)
4. Configure sink (Lakehouse)
5. Run the pipeline
6. Monitor the run

### Best Practices

| Area | Best Practice | Rationale |
|------|---------------|----------|
| Security | Use Azure AD authentication | Better than SQL auth |
| Performance | Use Medallion Architecture | Bronze → Silver → Gold |
| Cost | Monitor CU usage | Avoid unexpected bills |
| Development | Use Git integration | Version control |
| Testing | Separate Dev/Test/Prod workspaces | Safe deployments |

### Common Errors and Solutions

| Error | Cause | Resolution |
|-------|-------|------------|
| Capacity not found | Capacity paused or deleted | Check capacity status |
| Pipeline failed | Source not accessible | Check gateway and credentials |
| SQL timeout | Query too complex | Optimize query or increase timeout |
| Insufficient permissions | Wrong workspace role | Assign contributor role |
| Data mismatch | Schema mismatch | Review schema mapping |

### Step-by-Step Configuration

**Setting up Data Pipeline:**
1. Navigate to your workspace
2. Click New → Pipeline
3. Give pipeline a meaningful name
4. Add Copy Data activity from Activities pane
5. Configure Source tab:
   - Connection: Create new connection
   - Connection type: SQL Server
   - Server/Database: Enter details
   - Authentication: Windows/SQL/AAD
6. Configure Destination tab:
   - Connection: Your Lakehouse
   - Table: New table name
7. Configure Mapping tab:
   - Auto-map or manual mapping
8. Validate and Save
9. Run pipeline
10. Monitor run in Monitor hub

### Integration with Other Services

Fabric သည် Azure services အများအပြားနှင့်ပေါင်းစပ်အလုပ်လုပ်နိုင်ပါသည်-
- Azure Data Lake Storage Gen2 (shortcuts)
- Azure SQL Database (direct query)
- Azure Event Hubs (streaming)
- Azure Databricks (interoperability)
- Azure DevOps (CI/CD pipelines)
- Microsoft 365 (Copilot integration)

### Performance Optimization

1. **Use Delta Lake format** — Best performance for large-scale analytics
2. **Optimize Spark jobs** — Proper partitioning, caching
3. **Use Direct Lake** — Avoid import overhead for Power BI
4. **Schedule runs during off-peak** — Better resource availability
5. **Monitor CU consumption** — Identify expensive operations
6. **Use shortcuts instead of copying** — Save storage and time
7. **Vacuum old files** — Clean up unnecessary Delta versions

### Learning Path

1. ဤ module ၏ concept များကိုနားလည်အောင်လေ့လာပါ
2. Sample data ဖြင့်စမ်းသပ်ပါ
3. တကယ့် use case တစ်ခုအတွက်အသုံးချပါ
4. Performance testing လုပ်ပါ
5. Documentation ရေးပါ
6. Team နှင့် share လုပ်ပါ
## Detailed Learning Content

### Core Concepts and Architecture

Microsoft Fabric ၏အဓိကအင်္ဂါရပ်များမှာ-

1. **OneLake** — Single, unified data lake that all Fabric workloads use. ဒေတာအားလုံးကိုတစ်နေရာတည်းတွင်သိမ်းဆည်းပြီး duplication မလိုအပ်ပါ။
2. **SaaS Platform** — Microsoft က infrastructure အားလုံးကိုစီမံပေးပါသည် (no servers to manage)
3. **Integrated Experiences** — Data Factory, Synapse, Power BI တို့သည်တစ်ခုတည်းသော platform တွင်အလုပ်လုပ်ပါသည်
4. **AI-Powered** — Copilot နှင့်အခြား AI features များပါဝင်ပါသည်

### Practical Workshop

**Lab 1: Create Your First Fabric Workspace**
1. Sign in to app.fabric.microsoft.com
2. Create a new workspace (MyFirstWorkspace)
3. Create a Lakehouse item
4. Upload sample data (CSV file)
5. Create a table from the CSV
6. Query the data using SQL endpoint

**Lab 2: Build a Pipeline**
1. Create a new pipeline
2. Add Copy Data activity
3. Configure source (SQL Server or sample)
4. Configure sink (Lakehouse)
5. Run the pipeline
6. Monitor the run

### Best Practices

| Area | Best Practice | Rationale |
|------|---------------|----------|
| Security | Use Azure AD authentication | Better than SQL auth |
| Performance | Use Medallion Architecture | Bronze → Silver → Gold |
| Cost | Monitor CU usage | Avoid unexpected bills |
| Development | Use Git integration | Version control |
| Testing | Separate Dev/Test/Prod workspaces | Safe deployments |

### Common Errors and Solutions

| Error | Cause | Resolution |
|-------|-------|------------|
| Capacity not found | Capacity paused or deleted | Check capacity status |
| Pipeline failed | Source not accessible | Check gateway and credentials |
| SQL timeout | Query too complex | Optimize query or increase timeout |
| Insufficient permissions | Wrong workspace role | Assign contributor role |
| Data mismatch | Schema mismatch | Review schema mapping |

### Step-by-Step Configuration

**Setting up Data Pipeline:**
1. Navigate to your workspace
2. Click New → Pipeline
3. Give pipeline a meaningful name
4. Add Copy Data activity from Activities pane
5. Configure Source tab:
   - Connection: Create new connection
   - Connection type: SQL Server
   - Server/Database: Enter details
   - Authentication: Windows/SQL/AAD
6. Configure Destination tab:
   - Connection: Your Lakehouse
   - Table: New table name
7. Configure Mapping tab:
   - Auto-map or manual mapping
8. Validate and Save
9. Run pipeline
10. Monitor run in Monitor hub

### Integration with Other Services

Fabric သည် Azure services အများအပြားနှင့်ပေါင်းစပ်အလုပ်လုပ်နိုင်ပါသည်-
- Azure Data Lake Storage Gen2 (shortcuts)
- Azure SQL Database (direct query)
- Azure Event Hubs (streaming)
- Azure Databricks (interoperability)
- Azure DevOps (CI/CD pipelines)
- Microsoft 365 (Copilot integration)

### Performance Optimization

1. **Use Delta Lake format** — Best performance for large-scale analytics
2. **Optimize Spark jobs** — Proper partitioning, caching
3. **Use Direct Lake** — Avoid import overhead for Power BI
4. **Schedule runs during off-peak** — Better resource availability
5. **Monitor CU consumption** — Identify expensive operations
6. **Use shortcuts instead of copying** — Save storage and time
7. **Vacuum old files** — Clean up unnecessary Delta versions

### Learning Path

1. ဤ module ၏ concept များကိုနားလည်အောင်လေ့လာပါ
2. Sample data ဖြင့်စမ်းသပ်ပါ
3. တကယ့် use case တစ်ခုအတွက်အသုံးချပါ
4. Performance testing လုပ်ပါ
5. Documentation ရေးပါ
6. Team နှင့် share လုပ်ပါ
## Detailed Learning Content

### Core Concepts and Architecture

Microsoft Fabric ၏အဓိကအင်္ဂါရပ်များမှာ-

1. **OneLake** — Single, unified data lake that all Fabric workloads use. ဒေတာအားလုံးကိုတစ်နေရာတည်းတွင်သိမ်းဆည်းပြီး duplication မလိုအပ်ပါ။
2. **SaaS Platform** — Microsoft က infrastructure အားလုံးကိုစီမံပေးပါသည် (no servers to manage)
3. **Integrated Experiences** — Data Factory, Synapse, Power BI တို့သည်တစ်ခုတည်းသော platform တွင်အလုပ်လုပ်ပါသည်
4. **AI-Powered** — Copilot နှင့်အခြား AI features များပါဝင်ပါသည်

### Practical Workshop

**Lab 1: Create Your First Fabric Workspace**
1. Sign in to app.fabric.microsoft.com
2. Create a new workspace (MyFirstWorkspace)
3. Create a Lakehouse item
4. Upload sample data (CSV file)
5. Create a table from the CSV
6. Query the data using SQL endpoint

**Lab 2: Build a Pipeline**
1. Create a new pipeline
2. Add Copy Data activity
3. Configure source (SQL Server or sample)
4. Configure sink (Lakehouse)
5. Run the pipeline
6. Monitor the run

### Best Practices

| Area | Best Practice | Rationale |
|------|---------------|----------|
| Security | Use Azure AD authentication | Better than SQL auth |
| Performance | Use Medallion Architecture | Bronze → Silver → Gold |
| Cost | Monitor CU usage | Avoid unexpected bills |
| Development | Use Git integration | Version control |
| Testing | Separate Dev/Test/Prod workspaces | Safe deployments |

### Common Errors and Solutions

| Error | Cause | Resolution |
|-------|-------|------------|
| Capacity not found | Capacity paused or deleted | Check capacity status |
| Pipeline failed | Source not accessible | Check gateway and credentials |
| SQL timeout | Query too complex | Optimize query or increase timeout |
| Insufficient permissions | Wrong workspace role | Assign contributor role |
| Data mismatch | Schema mismatch | Review schema mapping |

### Step-by-Step Configuration

**Setting up Data Pipeline:**
1. Navigate to your workspace
2. Click New → Pipeline
3. Give pipeline a meaningful name
4. Add Copy Data activity from Activities pane
5. Configure Source tab:
   - Connection: Create new connection
   - Connection type: SQL Server
   - Server/Database: Enter details
   - Authentication: Windows/SQL/AAD
6. Configure Destination tab:
   - Connection: Your Lakehouse
   - Table: New table name
7. Configure Mapping tab:
   - Auto-map or manual mapping
8. Validate and Save
9. Run pipeline
10. Monitor run in Monitor hub

### Integration with Other Services

Fabric သည် Azure services အများအပြားနှင့်ပေါင်းစပ်အလုပ်လုပ်နိုင်ပါသည်-
- Azure Data Lake Storage Gen2 (shortcuts)
- Azure SQL Database (direct query)
- Azure Event Hubs (streaming)
- Azure Databricks (interoperability)
- Azure DevOps (CI/CD pipelines)
- Microsoft 365 (Copilot integration)

### Performance Optimization

1. **Use Delta Lake format** — Best performance for large-scale analytics
2. **Optimize Spark jobs** — Proper partitioning, caching
3. **Use Direct Lake** — Avoid import overhead for Power BI
4. **Schedule runs during off-peak** — Better resource availability
5. **Monitor CU consumption** — Identify expensive operations
6. **Use shortcuts instead of copying** — Save storage and time
7. **Vacuum old files** — Clean up unnecessary Delta versions

### Learning Path

1. ဤ module ၏ concept များကိုနားလည်အောင်လေ့လာပါ
2. Sample data ဖြင့်စမ်းသပ်ပါ
3. တကယ့် use case တစ်ခုအတွက်အသုံးချပါ
4. Performance testing လုပ်ပါ
5. Documentation ရေးပါ
6. Team နှင့် share လုပ်ပါ
