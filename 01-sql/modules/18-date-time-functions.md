# Module 18: Date & Time Functions

## Date & Time Functions ဆိုတာဘာလဲ?

Date/time functions များသည် date နှင့် time data များကိုကိုင်တွယ်ရန်၊ တွက်ချက်ရန်နှင့်ပြောင်းလဲရန်အသုံးပြုပါသည်။ ရက်စွဲများကိုနုတ်ခြင်း၊ ပေါင်းခြင်း၊ နှိုင်းယှဉ်ခြင်းနှင့်ခွဲထုတ်ခြင်းများအတွက်အလွန်အသုံးဝင်ပါသည်။

### 1. Current Date/Time

```sql
SELECT 
    GETDATE() AS CurrentDateTime,                -- SQL Server
    SYSDATETIME() AS MorePrecise,               -- More precise (100ns)
    SYSDATETIMEOFFSET() AS WithTimezone,        -- With timezone offset
    CURRENT_TIMESTAMP AS ANSIStandard,           -- ANSI SQL standard
    GETUTCDATE() AS UTCTime;                    -- UTC time
```

### 2. Date Part Extraction

```sql
SELECT 
    OrderDate,
    YEAR(OrderDate) AS OrderYear,
    MONTH(OrderDate) AS OrderMonth,
    DAY(OrderDate) AS OrderDay,
    DATEPART(QUARTER, OrderDate) AS Quarter,
    DATEPART(WEEK, OrderDate) AS WeekNumber,
    DATEPART(WEEKDAY, OrderDate) AS WeekDayNum,  -- 1=Sunday (default)
    DATENAME(MONTH, OrderDate) AS MonthName,     -- January, February...
    DATENAME(WEEKDAY, OrderDate) AS WeekDayName   -- Monday, Tuesday...
FROM Orders;
```

### 3. Date Arithmetic

```sql
SELECT 
    OrderDate,
    DATEADD(DAY, 7, OrderDate) AS DueDate,              -- 7 ရက်နောက်
    DATEADD(MONTH, 1, OrderDate) AS NextMonth,         -- 1 လနောက်
    DATEADD(YEAR, -1, OrderDate) AS LastYear,           -- 1 နှစ်ရှေ့
    DATEADD(QUARTER, 2, OrderDate) AS TwoQuartersLater, -- 2 quarters နောက်
    DATEDIFF(DAY, OrderDate, GETDATE()) AS DaysSince,
    DATEDIFF(MONTH, '2020-01-01', GETDATE()) AS MonthsSince2020,
    DATEDIFF(YEAR, HireDate, GETDATE()) AS YearsEmployed
FROM Orders;

-- Age calculation
SELECT 
    Name, 
    BirthDate,
    DATEDIFF(YEAR, BirthDate, GETDATE()) - 
        CASE 
            WHEN DATEADD(YEAR, DATEDIFF(YEAR, BirthDate, GETDATE()), BirthDate) 
                 > GETDATE() 
            THEN 1 ELSE 0 
        END AS Age
FROM Employees;
```

### 4. EOMONTH (End of Month)

```sql
SELECT 
    OrderDate,
    EOMONTH(OrderDate) AS LastDayOfMonth,             -- လကုန်ရက်
    EOMONTH(OrderDate, -1) AS LastDayPrevMonth,       -- ပြီးခဲ့တဲ့လကုန်
    EOMONTH(OrderDate, 1) AS LastDayNextMonth,        -- နောက်လကုန်
    DATEADD(DAY, 1, EOMONTH(OrderDate, -1)) AS FirstDayOfMonth  -- လဆန်း ၁
FROM Orders;
```

### 5. FORMAT Function

```sql
SELECT 
    OrderDate,
    FORMAT(OrderDate, 'yyyy-MM-dd') AS ISODateFormat,
    FORMAT(OrderDate, 'dd/MM/yyyy') AS UKFormat,
    FORMAT(OrderDate, 'MM/dd/yyyy') AS USFormat,
    FORMAT(OrderDate, 'MMMM yyyy') AS MonthYear,
    FORMAT(OrderDate, 'ddd') AS ShortDayName,
    FORMAT(OrderDate, 'dddd') AS FullDayName,
    FORMAT(OrderDate, 'hh:mm:ss tt') AS Time12Hour,
    FORMAT(OrderDate, 'MMM-yyyy') AS MonthYearShort
FROM Orders;
```

### 6. Practical Examples

```sql
-- Monthly Sales Report
SELECT 
    YEAR(OrderDate) AS Year,
    MONTH(OrderDate) AS MonthNumber,
    FORMAT(OrderDate, 'MMM-yyyy') AS MonthName,
    COUNT(*) AS OrderCount,
    SUM(Amount) AS TotalSales,
    AVG(Amount) AS AvgOrderValue,
    LAG(SUM(Amount), 1) OVER (ORDER BY YEAR(OrderDate), MONTH(OrderDate)) AS PrevMonth
FROM Orders
WHERE OrderDate >= DATEADD(YEAR, -1, GETDATE())
GROUP BY YEAR(OrderDate), MONTH(OrderDate), FORMAT(OrderDate, 'MMM-yyyy')
ORDER BY Year, MonthNumber;

-- Date range filter best practice
SELECT * FROM Orders
WHERE OrderDate >= '2024-01-01' AND OrderDate < '2025-01-01';
-- SARGable: index သုံးနိုင်

-- NOT SARGable (ရှောင်ရန်)
SELECT * FROM Orders WHERE YEAR(OrderDate) = 2024;
```

## Exercises

1. 2024 ခုနှစ်အတွင်း တစ်လချင်းစီရဲ့ စုစုပေါင်းရောင်းအားကိုတွက်ပါ။
2. Employee တစ်ယောက်ချင်းစီရဲ့ အသက်ကိုတွက်ပါ (DATEDIFF + CASE)။
3. လွန်ခဲ့သော ၃၀ ရက်အတွင်းမှာရှိသော orders များကိုရှာပါ။
4. EOMONTH သုံးပြီး လကုန်ရက်များကိုထုတ်ပါ။


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
