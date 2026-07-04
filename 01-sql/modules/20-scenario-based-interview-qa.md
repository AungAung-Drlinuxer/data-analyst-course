# Module 20: Scenario-Based Interview Q&A

## ဤအခန်းတွင်

Real-world SQL interview များတွင်မေးလေ့ရှိသော scenario-based မေးခွန်းများနှင့်အဖြေများကိုလေ့လာရမည်ဖြစ်ပါသည်။

### Scenario 1: Slow Running Query

**Q:** User က 'Report တစ်ခုက မိနစ် 30 ကြာနေတယ်' လို့ပြောလာရင် ဘယ်လိုစစ်မလဲ?

**A:** အောက်ပါအဆင့်များအတိုင်းလုပ်ဆောင်ပါ-

```sql
-- Step 1: Check query execution plan
SET STATISTICS TIME ON;
SET STATISTICS IO ON;

-- Step 2: Check missing indexes
SELECT * FROM sys.dm_db_missing_index_details;

-- Step 3: Check most expensive queries
SELECT TOP 10
    qs.total_worker_time / qs.execution_count AS AvgCPU,
    qs.total_logical_reads / qs.execution_count AS AvgReads,
    qt.text AS QueryText
FROM sys.dm_exec_query_stats qs
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) qt
ORDER BY AvgCPU DESC;
```

**ဖြေရှင်းချက်:** Scan → Seek ပြောင်းရန် index ဆောက်ပါ။ SARGable query ရေးပါ။ Statistics update လုပ်ပါ။

### Scenario 2: Duplicate Data

**Q:** Table ထဲမှာ duplicate rows များကိုဘယ်လိုရှာမလဲ? ဖျက်မလဲ?

```sql
-- Duplicate ရှာခြင်း (based on Email)
SELECT Email, COUNT(*) AS DuplicateCount
FROM Users
GROUP BY Email
HAVING COUNT(*) > 1;

-- Duplicate rows အသေးစိတ်ကြည့်ရှုခြင်း
WITH DuplicateUsers AS (
    SELECT *,
           ROW_NUMBER() OVER (PARTITION BY Email ORDER BY UserID) AS RowNum
    FROM Users
)
SELECT * FROM DuplicateUsers WHERE RowNum > 1;

-- Duplicate ဖျက်ခြင်း (Keep the oldest/first record)
WITH CTE AS (
    SELECT *,
           ROW_NUMBER() OVER (PARTITION BY Email ORDER BY UserID) AS rn
    FROM Users
)
DELETE FROM CTE WHERE rn > 1;
```

### Scenario 3: Pagination

**Q:** Web app အတွက် data 1 million rows ကို page ခွဲပြချင်ရင်?

```sql
-- Method 1: Keyset Pagination (Best Performance)
SELECT * FROM Products
WHERE ProductID > @LastProductID
ORDER BY ProductID
FETCH NEXT 50 ROWS ONLY;

-- Method 2: Offset Pagination (နှေး - large offset များအတွက်မသင့်)
SELECT * FROM Products
ORDER BY ProductID
OFFSET (@PageNumber - 1) * @PageSize ROWS
FETCH NEXT @PageSize ROWS ONLY;
```

### Scenario 4: Hierarchical Data

**Q:** Organization chart တစ်ခုကို query လုပ်ချင်ရင်?

```sql
WITH OrgChart AS (
    SELECT EmployeeID, Name, ManagerID, 0 AS Level
    FROM Employees WHERE ManagerID IS NULL
    UNION ALL
    SELECT e.EmployeeID, e.Name, e.ManagerID, o.Level + 1
    FROM Employees e
    INNER JOIN OrgChart o ON e.ManagerID = o.EmployeeID
)
SELECT EmployeeID, Name, 
       REPLICATE('  ', Level) + Name AS DisplayName,
       Level
FROM OrgChart
ORDER BY Level, Name;
```

### Scenario 5: Running Total

```sql
SELECT 
    Date, 
    Amount,
    SUM(Amount) OVER (ORDER BY Date) AS RunningTotal,
    AVG(Amount) OVER (ORDER BY Date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS MovingAvg7D
FROM DailySales;
```

### မကြာခဏမေးသော Interview Questions

| Question | Short Answer |
|----------|-------------|
| PK vs UNIQUE KEY ကွာခြားချက် | PK = 1 per table, no NULL; UNIQUE = multiple, allows 1 NULL |
| Clustered vs Non-clustered Index | Clustered = data physically sorted; Non-clustered = pointer to data |
| INNER vs LEFT JOIN | INNER = matching only; LEFT = all left table rows |
| DELETE vs TRUNCATE | DELETE = row-by-row, logged; TRUNCATE = deallocates pages |
| UNION vs UNION ALL | UNION = deduplicates; UNION ALL = keeps all |
| HAVING vs WHERE | HAVING = after GROUP BY; WHERE = before GROUP BY |
| Temporary Table vs CTE | Temp = physical, indexable; CTE = in-memory, query only |
| CHAR vs VARCHAR | CHAR = fixed; VARCHAR = variable (saves space) |


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
