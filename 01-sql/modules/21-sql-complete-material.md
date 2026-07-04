# Module 21: SQL Complete Material

## SQL Cheat Sheet

### DDL Commands (Data Definition Language)

```sql
-- Database
CREATE DATABASE DBName;
ALTER DATABASE DBName MODIFY NAME = NewName;
DROP DATABASE DBName;

-- Table
CREATE TABLE TableName (Col1 INT PRIMARY KEY, Col2 VARCHAR(50));
ALTER TABLE TableName ADD ColumnName DataType;
ALTER TABLE TableName DROP COLUMN ColumnName;
DROP TABLE TableName;
TRUNCATE TABLE TableName;
```

### DML Commands (Data Manipulation Language)

```sql
INSERT INTO TableName VALUES (val1, val2);
INSERT INTO TableName (Col1, Col2) VALUES (val1, val2);
UPDATE TableName SET Column1 = Value1 WHERE Condition;
DELETE FROM TableName WHERE Condition;
```

### DQL (SELECT) ရေးနည်း

```sql
SELECT [DISTINCT] Col1, Col2, Aggregate()
FROM Table1
JOIN Table2 ON Table1.Key = Table2.Key
WHERE Condition
GROUP BY Col1
HAVING Aggregate Condition
ORDER BY Col1 [ASC|DESC]
OFFSET n ROWS FETCH NEXT m ROWS ONLY;
```

### JOIN Types

```sql
INNER JOIN  -- Matching rows only
LEFT JOIN   -- All rows from left table
RIGHT JOIN  -- All rows from right table
FULL OUTER JOIN -- All rows from both tables
CROSS JOIN  -- Cartesian product
```

### Index Best Practices

| Rule | Description |
|------|-------------|
| **Clustered Index** | PK တွင်သုံးပါ၊ unique ဖြစ်ရန်၊ narrow column (INT) |
| **Non-clustered Index** | WHERE, JOIN, ORDER BY သုံးသော columns များ |
| **Covering Index** | Query အတွက်လိုအပ်သော columns အားလုံးပါဝင်သော index |
| **Filtered Index** | WHERE clause နှင့်တွဲသုံးရန် (partial data) |
| **Index Maintenance** | Fragmentation check, rebuild/reorganize |

### Query Performance Tips

1. **SELECT * ကိုရှောင်ပါ** — လိုအပ်သော columns များကိုသာရွေးပါ
2. **WHERE clause ကိုသေချာရေးပါ** — SARGable ဖြစ်စေရန်
3. **JOIN columns များတွင် index ထားပါ**
4. **Subquery ထက် JOIN ကိုပိုသုံးပါ**
5. **Large dataset အတွက် batch processing လုပ်ပါ**
6. **Execution plan ကိုကြည့်ပါ** — Scan vs Seek
7. **Statistics ကို update လုပ်ပါ**

### Common Mistakes and Fixes

```sql
-- ❌ Mistakes
WHERE Name = NULL;              -- Wrong: NULL ကို = နဲ့မစစ်ရ
WHERE YEAR(Date) = 2024;       -- Wrong: SARGable မဟုတ်
SELECT DISTINCT *;             -- Wrong: unnecessary

-- ✅ Correct
WHERE Name IS NULL;
WHERE Date >= '2024-01-01' AND Date < '2025-01-01';
SELECT DISTINCT Col1, Col2;
```

### Naming Conventions

| Object | Convention | Example |
|--------|-----------|---------|
| Table | PascalCase / plural | Customers, Products |
| Column | PascalCase | CustomerID, FirstName |
| Index | IX_TableName_Column | IX_Customers_Email |
| Primary Key | PK_TableName | PK_Customers |
| Foreign Key | FK_ChildTable_ParentTable | FK_Orders_Customers |
| View | vw_ prefix | vw_ActiveCustomers |

### Useful System Queries

```sql
-- Table size
SELECT t.NAME AS TableName, p.rows AS RowCounts,
       SUM(a.total_pages) * 8 / 1024 AS TotalSpaceMB
FROM sys.tables t
INNER JOIN sys.indexes i ON t.object_id = i.object_id
INNER JOIN sys.partitions p ON i.object_id = p.object_id
INNER JOIN sys.allocation_units a ON p.partition_id = a.container_id
GROUP BY t.Name, p.rows
ORDER BY TotalSpaceMB DESC;

-- Running queries
SELECT r.session_id, r.status, r.command, 
       t.text, r.start_time
FROM sys.dm_exec_requests r
CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) t;

-- Index usage stats
SELECT OBJECT_NAME(i.object_id) AS TableName,
       i.name AS IndexName,
       s.user_seeks, s.user_scans, s.user_lookups
FROM sys.indexes i
LEFT JOIN sys.dm_db_index_usage_stats s
ON i.object_id = s.object_id AND i.index_id = s.index_id;
```


## Practical Applications and Examples

### Real-World Scenario

**Use Case:** Data Analysis Dashboard တစ်ခုတည်ဆောက်ခြင်း

**Requirements:**
- Data integration from multiple sources
- Real-time data refresh
- Interactive visualizations with drill-through
- Mobile-friendly layout
- Row-level security for different user groups

**Implementation Steps:**
1. Connect to data sources (SQL Server, Excel, API)
2. Transform and clean data with Power Query
3. Design Star Schema data model
4. Create calculated columns and measures
5. Build visualizations and arrange dashboard
6. Add interactivity (slicers, bookmarks, drill-through)
7. Test performance and optimize
8. Deploy to service and set up refresh
9. Configure row-level security
10. Share with stakeholders

### Best Practices

1. **Data Quality First** — Clean data သည်ကောင်းမွန်သော analysis ၏အခြေခံဖြစ်ပါသည်
2. **Model Design** — Star Schema ကိုသုံးပါ (fact + dimensions)
3. **DAX Optimization** — Measures များကို efficient ဖြစ်အောင်ရေးပါ
4. **Visual Design** — Clean, simple, focused dashboard များဆောက်ပါ
5. **Performance** — Regular performance testing လုပ်ပါ
6. **Documentation** — Technical documentation ရေးထားပါ
7. **Version Control** — Git သုံးပြီး code များကိုစီမံပါ

### Common Pitfalls

| Problem | Cause | Solution |
|---------|-------|----------|
| Data mismatch | Wrong relationship direction | Check cardinality |
| Slow report | Too many visuals/complex measures | Optimize with Performance Analyzer |
| Wrong totals | Measure context issue | Use CALCULATE properly |
| Refresh failure | Gateway not configured | Check gateway status |
| Security breach | RLS not configured | Implement row-level security |

### Performance Tips

1. **Reduce columns** — Only load columns you need
2. **Filter early** — Apply filters at source (query folding)
3. **Use aggregations** — Pre-aggregate large datasets
4. **Avoid calculated columns** — Use measures instead when possible
5. **Disable cross-filtering** — Only enable when needed
6. **Use numeric keys** — String keys degrade performance
7. **Limit card visuals** — Each card runs a separate query

### Exercise Questions

1. ဤ feature ကိုအသုံးပြုပြီး report တစ်ခုဆောက်ပါ
2. Sample data ဖြင့်စမ်းသပ်ပါ
3. Performance ကိုစစ်ဆေးပါ (Performance Analyzer)
4. Documentation ရေးပါ
## Practical Applications and Examples

### Real-World Scenario

**Use Case:** Data Analysis Dashboard တစ်ခုတည်ဆောက်ခြင်း

**Requirements:**
- Data integration from multiple sources
- Real-time data refresh
- Interactive visualizations with drill-through
- Mobile-friendly layout
- Row-level security for different user groups

**Implementation Steps:**
1. Connect to data sources (SQL Server, Excel, API)
2. Transform and clean data with Power Query
3. Design Star Schema data model
4. Create calculated columns and measures
5. Build visualizations and arrange dashboard
6. Add interactivity (slicers, bookmarks, drill-through)
7. Test performance and optimize
8. Deploy to service and set up refresh
9. Configure row-level security
10. Share with stakeholders

### Best Practices

1. **Data Quality First** — Clean data သည်ကောင်းမွန်သော analysis ၏အခြေခံဖြစ်ပါသည်
2. **Model Design** — Star Schema ကိုသုံးပါ (fact + dimensions)
3. **DAX Optimization** — Measures များကို efficient ဖြစ်အောင်ရေးပါ
4. **Visual Design** — Clean, simple, focused dashboard များဆောက်ပါ
5. **Performance** — Regular performance testing လုပ်ပါ
6. **Documentation** — Technical documentation ရေးထားပါ
7. **Version Control** — Git သုံးပြီး code များကိုစီမံပါ

### Common Pitfalls

| Problem | Cause | Solution |
|---------|-------|----------|
| Data mismatch | Wrong relationship direction | Check cardinality |
| Slow report | Too many visuals/complex measures | Optimize with Performance Analyzer |
| Wrong totals | Measure context issue | Use CALCULATE properly |
| Refresh failure | Gateway not configured | Check gateway status |
| Security breach | RLS not configured | Implement row-level security |

### Performance Tips

1. **Reduce columns** — Only load columns you need
2. **Filter early** — Apply filters at source (query folding)
3. **Use aggregations** — Pre-aggregate large datasets
4. **Avoid calculated columns** — Use measures instead when possible
5. **Disable cross-filtering** — Only enable when needed
6. **Use numeric keys** — String keys degrade performance
7. **Limit card visuals** — Each card runs a separate query

### Exercise Questions

1. ဤ feature ကိုအသုံးပြုပြီး report တစ်ခုဆောက်ပါ
2. Sample data ဖြင့်စမ်းသပ်ပါ
3. Performance ကိုစစ်ဆေးပါ (Performance Analyzer)
4. Documentation ရေးပါ
## Practical Applications and Examples

### Real-World Scenario

**Use Case:** Data Analysis Dashboard တစ်ခုတည်ဆောက်ခြင်း

**Requirements:**
- Data integration from multiple sources
- Real-time data refresh
- Interactive visualizations with drill-through
- Mobile-friendly layout
- Row-level security for different user groups

**Implementation Steps:**
1. Connect to data sources (SQL Server, Excel, API)
2. Transform and clean data with Power Query
3. Design Star Schema data model
4. Create calculated columns and measures
5. Build visualizations and arrange dashboard
6. Add interactivity (slicers, bookmarks, drill-through)
7. Test performance and optimize
8. Deploy to service and set up refresh
9. Configure row-level security
10. Share with stakeholders

### Best Practices

1. **Data Quality First** — Clean data သည်ကောင်းမွန်သော analysis ၏အခြေခံဖြစ်ပါသည်
2. **Model Design** — Star Schema ကိုသုံးပါ (fact + dimensions)
3. **DAX Optimization** — Measures များကို efficient ဖြစ်အောင်ရေးပါ
4. **Visual Design** — Clean, simple, focused dashboard များဆောက်ပါ
5. **Performance** — Regular performance testing လုပ်ပါ
6. **Documentation** — Technical documentation ရေးထားပါ
7. **Version Control** — Git သုံးပြီး code များကိုစီမံပါ

### Common Pitfalls

| Problem | Cause | Solution |
|---------|-------|----------|
| Data mismatch | Wrong relationship direction | Check cardinality |
| Slow report | Too many visuals/complex measures | Optimize with Performance Analyzer |
| Wrong totals | Measure context issue | Use CALCULATE properly |
| Refresh failure | Gateway not configured | Check gateway status |
| Security breach | RLS not configured | Implement row-level security |

### Performance Tips

1. **Reduce columns** — Only load columns you need
2. **Filter early** — Apply filters at source (query folding)
3. **Use aggregations** — Pre-aggregate large datasets
4. **Avoid calculated columns** — Use measures instead when possible
5. **Disable cross-filtering** — Only enable when needed
6. **Use numeric keys** — String keys degrade performance
7. **Limit card visuals** — Each card runs a separate query

### Exercise Questions

1. ဤ feature ကိုအသုံးပြုပြီး report တစ်ခုဆောက်ပါ
2. Sample data ဖြင့်စမ်းသပ်ပါ
3. Performance ကိုစစ်ဆေးပါ (Performance Analyzer)
4. Documentation ရေးပါ
