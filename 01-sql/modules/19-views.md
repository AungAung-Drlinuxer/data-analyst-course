# Module 19: Views

## View ဆိုတာဘာလဲ?

View ဆိုသည်မှာ virtual table တစ်ခုဖြစ်ပြီး saved SQL query ၏ result set ကို table တစ်ခုလိုအသုံးပြုနိုင်ပါသည်။ View သည် data ကိုတိုက်ရိုက်မသိမ်းဆည်းဘဲ (indexed view မှလွဲ၍) အခြေခံ table များမှ data များကိုပြသပါသည်။

### View ကောင်းကျိုးများ

1. **Security** — Sensitive columns များကိုဖုံးကွယ်နိုင်ပါသည် (ဥပမာ - salary column ကိုမပြဘဲ view ဆောက်ခြင်း)
2. **Simplicity** — Complex queries (multiple JOINs, calculations) များကို view တစ်ခုအနေဖြင့်သိမ်းဆည်းနိုင်
3. **Consistency** — တူညီသော logic ကိုနေရာတိုင်းတွင်ပြန်သုံးနိုင်
4. **Maintenance** — Query logic ကိုတစ်နေရာတည်းတွင်ပြုပြင်နိုင်

### CREATE VIEW

```sql
-- ရိုးရိုး View
CREATE VIEW ActiveCustomers AS
SELECT CustomerID, Name, Email, City, JoinDate
FROM Customers
WHERE Status = 'Active';

-- View ကိုသုံးခြင်း (Table လိုပဲ)
SELECT * FROM ActiveCustomers;
SELECT * FROM ActiveCustomers WHERE City = 'Yangon';
SELECT City, COUNT(*) FROM ActiveCustomers GROUP BY City;

-- Complex View
CREATE VIEW SalesSummary AS
SELECT 
    c.CustomerID,
    c.Name AS CustomerName,
    c.City,
    COUNT(o.OrderID) AS TotalOrders,
    ISNULL(SUM(o.TotalAmount), 0) AS TotalSpent,
    AVG(o.TotalAmount) AS AvgOrderValue,
    MAX(o.OrderDate) AS LastOrderDate,
    DATEDIFF(DAY, MAX(o.OrderDate), GETDATE()) AS DaysSinceLastOrder
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.Name, c.City;
```

### Indexed View (SQL Server)

Indexed view (materialized view) သည် view ၏ result set ကို disk ပေါ်တွင်物理သိမ်းဆည်းပြီး performance ကိုများစွာကောင်းမွန်စေပါသည်။

```sql
-- SCHEMABINDING လိုအပ်
CREATE VIEW SalesByProduct WITH SCHEMABINDING AS
SELECT 
    ProductID, 
    COUNT_BIG(*) AS TransactionCount, 
    SUM(Quantity) AS TotalQuantity
FROM dbo.OrderItems
GROUP BY ProductID;

-- Unique clustered index ဆောက်ခြင်း
CREATE UNIQUE CLUSTERED INDEX IX_SalesByProduct ON SalesByProduct(ProductID);
```

### View Options

```sql
-- WITH ENCRYPTION (view definition ကိုဝှက်ရန်)
CREATE VIEW ActiveCustomers WITH ENCRYPTION AS
SELECT * FROM Customers WHERE Status = 'Active';

-- WITH CHECK OPTION (view မှတဆင့်ထည့်သော data ကိုစစ်ရန်)
CREATE VIEW ActiveCustomers AS
SELECT * FROM Customers WHERE Status = 'Active'
WITH CHECK OPTION;
-- Status = 'Active' မဟုတ်သော row ကို view မှတဆင့်ထည့်၍မရ
```

### Alter and Drop Views

```sql
-- View ကိုပြင်ဆင်ခြင်း
ALTER VIEW ActiveCustomers AS
SELECT CustomerID, Name, Email, Phone
FROM Customers
WHERE Status = 'Active';

-- View ကိုဖျက်ခြင်း
DROP VIEW ActiveCustomers;

-- View definition ကြည့်ရှုခြင်း
EXEC sp_helptext 'ActiveCustomers';
```

### View Limitations

1. ORDER BY ကို TOP/FETCH မပါပဲတိုက်ရိုက်မသုံးရ
2. View ကို Index ထားရန် SCHEMABINDING လိုအပ်
3. Complex views များသည် performance ကိုထိခိုက်နိုင်
4. Nested views (view ပေါ်မှာ view) များကိုရှောင်ရန်

## Exercises

1. Active employees view တစ်ခုဆောက်ပါ (Status = 'Active')။
2. Monthly sales summary view ဆောက်ပါ (Year, Month, TotalSales, OrderCount)။
3. ရှိပြီးသား view ကို ALTER လုပ်ပြီး column အသစ်ထည့်ပါ။


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
