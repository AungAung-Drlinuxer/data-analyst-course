# Module 15: Text Functions (String Functions)

## Text Functions ဆိုတာဘာလဲ?

Text functions (string functions) များသည် string (စာသား) data များကိုစီမံရန်၊ ပြောင်းလဲရန်၊ ရှာဖွေရန်နှင့်ခွဲထုတ်ရန်အသုံးပြုပါသည်။ Data cleaning နှင့် transformation များတွင်အလွန်အသုံးဝင်ပါသည်။

### String Manipulation Functions

#### 1. CONCAT / CONCAT_WS
```sql
-- CONCAT (NULL ကိုအလိုအလျောက်ကိုင်တွယ်)
SELECT CONCAT(FirstName, ' ', LastName) AS FullName FROM Employees;
SELECT CONCAT(Address, ', ', City, ', ', Country) AS FullAddress FROM Customers;

-- CONCAT_WS (With Separator - SQL Server 2017+)
SELECT CONCAT_WS(', ', LastName, FirstName, Email) AS ContactInfo FROM Employees;
```

#### 2. SUBSTRING / LEFT / RIGHT
```sql
SELECT 
    Email,
    LEFT(Email, 3) AS First3Chars,
    RIGHT(Email, 4) AS Last4Chars (domain extension),
    SUBSTRING(Email, 1, CHARINDEX('@', Email) - 1) AS Username,
    SUBSTRING(Email, CHARINDEX('@', Email) + 1, LEN(Email)) AS Domain
FROM Employees;
```

#### 3. LEN / DATALENGTH
```sql
SELECT 
    Name,
    LEN(Name) AS CharCount,          -- character အရေအတွက်
    DATALENGTH(Name) AS ByteCount     -- byte အရေအတွက်
FROM Employees;
-- NVARCHAR ဆိုလျှင် DATALENGTH = LEN * 2
```

#### 4. UPPER / LOWER
```sql
SELECT 
    UPPER(Name) AS UpperCase,
    LOWER(Email) AS LowerCase
FROM Employees;
```

#### 5. TRIM / LTRIM / RTRIM
```sql
SELECT 
    TRIM('  Hello World  ') AS Trimmed,         -- နှစ်ဖက်လုံး
    LTRIM('  Hello') AS LeftTrimmed,           -- ဘယ်ဘက်
    RTRIM('Hello  ') AS RightTrimmed;          -- ညာဘက်

-- TRIM with specific characters (SQL Server 2017+)
SELECT TRIM('.' FROM '...Hello...') AS TrimmedChars;  -- 'Hello'
```

#### 6. REPLACE
```sql
SELECT 
    Description,
    REPLACE(Description, 'old', 'new') AS UpdatedDesc,
    REPLACE(Phone, '-', '') AS CleanPhone,
    REPLACE(REPLACE(Name, ' ', ''), '.', '') AS NoSpacesNoDots
FROM Products;
```

#### 7. CHARINDEX / PATINDEX
```sql
SELECT 
    Email,
    CHARINDEX('@', Email) AS AtPosition,
    CHARINDEX('.', Email, CHARINDEX('@', Email)) AS FirstDotAfterAt,
    PATINDEX('%@gmail.com', Email) AS IsGmail  -- 1 if yes, 0 if no
FROM Employees;
```

### Practical Data Cleaning Examples

```sql
-- Email username extraction
SELECT 
    Email,
    LEFT(Email, CHARINDEX('@', Email) - 1) AS Username,
    SUBSTRING(Email, CHARINDEX('@', Email) + 1, LEN(Email)) AS Domain
FROM Employees
WHERE Email IS NOT NULL;

-- Full name parsing
SELECT 
    FullName,
    LEFT(FullName, CHARINDEX(' ', FullName) - 1) AS FirstName,
    RIGHT(FullName, LEN(FullName) - CHARINDEX(' ', FullName)) AS LastName
FROM Customers;

-- Phone formatting
SELECT 
    Phone,
    '+95' + RIGHT(Phone, LEN(Phone) - 1) AS MyanmarFormat
FROM Customers;

-- Data masking
SELECT 
    Email,
    LEFT(Email, 2) + '****' + SUBSTRING(Email, CHARINDEX('@', Email), LEN(Email)) AS MaskedEmail,
    STUFF(Email, 3, CHARINDEX('@', Email) - 4, '****') AS MaskedEmail2
FROM Employees;
```

## Exercises

1. Customers table မှ full name ကိုခွဲပြီး first name နှင့် last name ထုတ်ပါ။
2. Products table မှ description ရှိ 'old' ကို 'new' ဖြင့် replace လုပ်ပါ။
3. Employees table မှ email domain ကိုခွဲထုတ်ပြီး @gmail.com အရေအတွက်ရေတွက်ပါ။


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
