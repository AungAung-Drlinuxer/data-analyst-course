# Module 16: Numeric Functions (ကိန်းဂဏန်း Functions)

## Numeric Functions များ

Numeric functions များသည် ကိန်းဂဏန်းများကိုတွက်ချက်ရန်၊ ဝိုင်းရန်နှင့်ပြောင်းလဲရန်အသုံးပြုပါသည်။

### 1. ROUND / CEILING / FLOOR
```sql
SELECT 
    Amount,
    ROUND(Amount, 2) AS Rounded2Dec,      -- 2 decimal ထိဝိုင်း
    ROUND(Amount, 0) AS RoundedInt,       -- ကိန်းပြည့်ဝိုင်း
    ROUND(Amount, -1) AS Rounded10s,       -- 10 လုံးထိဝိုင်း (e.g., 123 → 120)
    ROUND(Amount, -2) AS Rounded100s,      -- 100 လုံးထိဝိုင်း (e.g., 123 → 100)
    CEILING(Amount) AS CeilingValue,        -- အပေါ်သို့ဝိုင်း
    FLOOR(Amount) AS FloorValue             -- အောက်သို့ဝိုင်း
FROM Transactions;

-- Result: Amount=123.4567, Rounded2Dec=123.46, Ceiling=124, Floor=123
```

### 2. ABS / SIGN
```sql
SELECT 
    Difference,
    ABS(Difference) AS AbsoluteValue,      -- Negative ကို positive ပြောင်း
    SIGN(Difference) AS SignValue           -- 1=positive, -1=negative, 0=zero
FROM Variance;
```

### 3. POWER / SQRT / SQUARE
```sql
SELECT 
    POWER(10, 3) AS TenCubed,              -- 1000 (10^3)
    POWER(2, 10) AS TwoToThe10th,          -- 1024 (2^10)
    SQRT(144) AS SquareRoot,               -- 12
    SQUARE(12) AS Squared;                  -- 144
```

### 4. RANDOM Numbers
```sql
-- Random float 0-1
SELECT RAND() AS RandomValue;

-- Random integer 1-100
SELECT CAST(RAND() * 100 AS INT) + 1 AS RandomInt;

-- Random ID selection
SELECT TOP 1 * FROM Customers ORDER BY NEWID();

-- Random sample 10%
SELECT * FROM Products
WHERE ABS(CAST(CAST(BINARY_CHECKSUM(*) AS BIGINT) AS DECIMAL)) % 100 < 10;
```

### 5. Mathematical Functions
```sql
SELECT 
    PI() AS PiValue,                       -- 3.14159265358979
    EXP(1) AS EulerNumber,                 -- 2.71828182845905
    LOG(100) AS LogBaseE,                  -- Natural log
    LOG10(100) AS LogBase10,                -- 2
    SIN(30 * PI() / 180) AS Sin30,         -- 0.5
    COS(0) AS Cos0,                        -- 1
    DEGREES(PI()) AS RadToDeg,             -- 180
    RADIANS(180) AS DegToRad;              -- 3.14159
```

### လက်တွေ့အသုံးချမှုများ

```sql
-- Order Summary တွက်ချက်ခြင်း
SELECT 
    OrderID,
    SUM(Quantity * UnitPrice) AS SubTotal,
    ROUND(SUM(Quantity * UnitPrice) * 0.9, 2) AS After10PctDiscount,
    ROUND(SUM(Quantity * UnitPrice) * 0.05, 2) AS Tax5Pct,
    CEILING(SUM(Quantity * UnitPrice) * 1.05) AS RoundUpTotal
FROM OrderItems
GROUP BY OrderID;

-- Statistical Summary
SELECT 
    COUNT(*) AS N,
    AVG(Price) AS Mean,
    STDEV(Price) AS StdDev,               -- Standard deviation
    VAR(Price) AS Variance,                 -- Variance
    MAX(Price) - MIN(Price) AS Range
FROM Products;
```

## Best Practices

1. **Financial data အတွက် DECIMAL သုံးပါ** — FLOAT/REAL သည် rounding error ဖြစ်နိုင်ပါသည်
2. **ROUND ကိုလိုအပ်မှသာသုံးပါ** — တွက်ချက်မှုတိုင်းတွင် ROUND သုံးရန် မလိုအပ်ပါ
3. **CEILING/FLOOR ကိုသင့်တော်ရာသုံးပါ** — CEILING က အပေါ်သို့ဝိုင်း (e.g., tax calculation)

## Exercises

1. Products table မှ price များကို 10% တိုးပြီး 2 decimal ထိဝိုင်းပါ။
2. CEILING အသုံးပြု၍ shipping cost ကိုတွက်ပါ (1kg = $5, အပေါ်သို့ဝိုင်း)။
3. RAND သုံးပြီး customer တစ်ယောက်ကိုကျပန်းရွေးပါ။


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
