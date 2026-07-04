# Module 22: SQL Projects

## Project 1: E-Commerce Database System

### Description
Customer, Product, Order, OrderItem များပါဝင်သော e-commerce database ကိုတည်ဆောက်ပါ။

### Tables

- **Customers**: CustomerID, Name, Email, Phone, Address, City, JoinDate, Status
- **Products**: ProductID, ProductName, Category, Price, Cost, StockQuantity, SupplierID
- **Orders**: OrderID, CustomerID, OrderDate, TotalAmount, Status, ShippingAddress
- **OrderItems**: OrderItemID, OrderID, ProductID, Quantity, UnitPrice
- **Categories**: CategoryID, CategoryName, Description, ParentCategoryID (self-reference)

### Tasks

1. Database နှင့် tables များကို PK, FK, constraints များဖြင့်ဆောက်ပါ
2. Sample data အနည်းဆုံး 50 customers, 100 products, 200 orders ထည့်ပါ
3. Joins သုံးပြီး customer order history report ထုတ်ပါ
4. Window functions သုံးပြီး customer ranking (by total spent) လုပ်ပါ
5. CTE သုံးပြီး category tree ကိုပြပါ
6. Stored procedures ရေးပါ (GetCustomerOrders, PlaceOrder)
7. View ဆောက်ပါ (MonthlySalesSummary, TopCustomers)

## Project 2: Employee Management System

### Tables

- **Departments**: DeptID, DeptName, ManagerID, Budget, Location
- **Employees**: EmpID, Name, Email, Phone, HireDate, Salary, DeptID, ManagerID, Status
- **Salaries**: SalaryID, EmpID, EffectiveDate, Amount, ChangedBy
- **Attendance**: AttendanceID, EmpID, Date, Status (Present/Absent/Leave), Hours
- **LeaveRequests**: LeaveID, EmpID, StartDate, EndDate, Type, Status

### Tasks

1. Department hierarchy ကို recursive CTE ဖြင့်ပြပါ
2. Salary analysis: avg, min, max, rank by department
3. Employee turnover rate တွက်ပါ
4. Leave balance analysis
5. Department budget vs actual spending

## Project 3: Library Management System

### Tables: Books, Members, Loans, Fines, Reservations

### Tasks
1. Overdue books query (DATEDIFF)
2. Member borrowing history with running total
3. Popular books by category and month
4. Fine calculation logic (CASE WHEN)
5. Book availability check (subquery)

## Project 4: Banking System

### Tables: Accounts, Transactions, Customers, Branches

### Tasks
1. Deposit/Withdrawal stored procedures (with transactions)
2. Daily balance report (running total with window function)
3. Fraud detection: unusual transactions (>3 std dev)
4. Interest calculation (CASE WHEN for tiered rates)
5. Monthly account statements (pivot style)

## Project 5: Hospital Management

### Tables: Patients, Doctors, Appointments, MedicalRecords, Prescriptions

### Tasks
1. Doctor schedule query (date/time functions)
2. Patient visit history (recursive CTE)
3. Revenue by department (aggregate with GROUP BY)
4. Bed availability report (CASE WHEN)
5. Patient wait time analysis (DATEDIFF)

## Suggested Approach

Project တစ်ခုစီအတွက်:
1. Database design (ER diagram) ဆွဲပါ
2. Tables များဆောက်ပြီး relationships ထားပါ
3. Sample data ထည့်ပါ (INSERT statements)
4. Business queries ရေးပါ (5-10 queries)
5. Views, stored procedures များထည့်ပါ
6. Performance optimization (indexes, query tuning)

## Resources

- Sample datasets: Kaggle, data.gov, Mockaroo (data generator)
- Tools: DBeaver, SSMS, Azure Data Studio
- Version control: Git + GitHub


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
