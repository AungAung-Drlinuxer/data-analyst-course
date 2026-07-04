# Module 27: Important Power BI Handy Notes

## DAX Quick Reference

### Common Measures
```dax
Total Sales = SUM(Sales[Amount])
Total Quantity = SUM(Sales[Quantity])
Distinct Customers = DISTINCTCOUNT(Sales[CustomerID])
Avg Order Value = DIVIDE([Total Sales], [Order Count])
```

### Time Intelligence
```dax
Sales YTD = TOTALYTD([Total Sales], 'Date'[Date])
Sales LY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date]))
Sales YoY % = DIVIDE([Total Sales] - [Sales LY], [Sales LY])
```

### Filter Context Examples
```dax
CALCULATE([Measure], Table[Column] = "Value")
CALCULATE([Measure], FILTER(Table, Condition))
CALCULATE([Measure], ALL(Table))
```

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| F2 | Rename field/visual |
| Ctrl+D | Duplicate visual |
| Ctrl+Shift+Enter | New measure |
| Alt+F1 | New visual |
| Ctrl+E | Export data |

## Best Practices Checklist

- [ ] Star Schema သုံးထားရန်
- [ ] Calendar table ထည့်ထားရန်
- [ ] Measures များကို proper naming convention လိုက်နာရန်
- [ ] Performance Analyzer ဖြင့်စစ်ဆေးရန်
- [ ] Report ကို mobile-friendly ဖြစ်စေရန်
- [ ] RLS ထားရှိရန် (multi-user)


## Comprehensive Guide and Examples

### Module Overview

ဤ module တွင် Power BI ၏အရေးကြီးသော concepts များနှင့်လက်တွေ့အသုံးချမှုများကိုလေ့လာရမည်ဖြစ်ပါသည်။

### Key Learning Objectives

1. Understand Core Concepts — Power BI ၏အခြေခံသဘောတရားများကိုနားလည်ရန်
2. Hands-on Practice — ကိုယ်တိုင်လက်တွေ့ဆောက်လုပ်နိုင်ရန်
3. Best Practices — အကောင်းဆုံးနည်းလမ်းများကိုလေ့လာရန်
4. Real-world Application — တကယ့်လုပ်ငန်းခွင်တွင်အသုံးချနိုင်ရန်

### Step-by-Step Learning Path

1. Concept Understanding — အခြေခံသဘောတရားများကိုလေ့လာပါ
2. Tool Setup — Power BI Desktop ကို install လုပ်ပြီး configure လုပ်ပါ
3. Sample Project — Sample data ဖြင့်လက်တွေ့ဆောက်လုပ်ပါ
4. Advanced Features — DAX, Power Query, AI features များကိုလေ့လာပါ
5. Deployment — Service သို့ publish လုပ်ပြီး share လုပ်ပါ
6. Optimization — Performance ကိုစစ်ဆေးပြီး optimize လုပ်ပါ

### Practical Workshop

Exercise 1: Basic Report Creation
1. Open Power BI Desktop
2. Load sample data (Excel or CSV)
3. Create 3 visualizations (bar, line, table)
4. Add a slicer for filtering
5. Format and arrange on canvas
6. Save and publish

Exercise 2: Advanced Analysis
1. Create a calculated column
2. Write 2 DAX measures
3. Create a hierarchy
4. Add drill-through page
5. Configure row-level security
6. Test with different user roles

### Common Interview Questions

1. Power BI ၏အဓိက components များကိုဖော်ပြပါ။
2. Measure နှင့် Calculated Column ကွာခြားချက်ကိုရှင်းပြပါ။
3. Star Schema ဆိုတာဘာလဲ? ဘာကြောင့်အသုံးပြုရသလဲ။
4. CALCULATE function ရဲ့အလုပ်လုပ်ပုံကိုရှင်းပြပါ။
5. Import vs DirectQuery ဘယ်အချိန်မှာသုံးမလဲ?
6. Row-Level Security ကိုဘယ်လို implement လုပ်မလဲ?
7. Performance optimization techniques များကိုဖော်ပြပါ။
8. Power BI Service နဲ့ Power BI Desktop ကွာခြားချက်ကဘာလဲ?

### Troubleshooting Guide

| Issue | Check | Solution |
|-------|-------|----------|
| Data not loading | Connection settings | Check credentials and gateway |
| Wrong values | Measure formula | Review DAX context |
| Slow report | Performance Analyzer | Optimize measures and model |
| Refresh failure | Gateway status | Restart gateway service |
| Missing data | Relationship direction | Check cardinality |

### Resources

- Microsoft Learn: Power BI documentation
- DAX Guide: dax.guide (all DAX functions with examples)
- SQLBI: DAX patterns and best practices
- Power BI Community: forum for questions and answers
- GitHub: Sample datasets and report templates

### Best Practices Summary

1. Design with Star Schema — Fact + Dimensions
2. Use Measures over Calculated Columns — Better performance
3. Optimize Power Query — Filter early, remove unused columns
4. Implement RLS — Secure data by user role
5. Document Everything — Measures, model, data sources
6. Regular Performance Testing — Use Performance Analyzer
7. Version Control — Use Git for .pbip files
8. User Training — Train end users on report usage


## Comprehensive Guide and Examples

### Module Overview

ဤ module တွင် Power BI ၏အရေးကြီးသော concepts များနှင့်လက်တွေ့အသုံးချမှုများကိုလေ့လာရမည်ဖြစ်ပါသည်။

### Key Learning Objectives

1. Understand Core Concepts — Power BI ၏အခြေခံသဘောတရားများကိုနားလည်ရန်
2. Hands-on Practice — ကိုယ်တိုင်လက်တွေ့ဆောက်လုပ်နိုင်ရန်
3. Best Practices — အကောင်းဆုံးနည်းလမ်းများကိုလေ့လာရန်
4. Real-world Application — တကယ့်လုပ်ငန်းခွင်တွင်အသုံးချနိုင်ရန်

### Step-by-Step Learning Path

1. Concept Understanding — အခြေခံသဘောတရားများကိုလေ့လာပါ
2. Tool Setup — Power BI Desktop ကို install လုပ်ပြီး configure လုပ်ပါ
3. Sample Project — Sample data ဖြင့်လက်တွေ့ဆောက်လုပ်ပါ
4. Advanced Features — DAX, Power Query, AI features များကိုလေ့လာပါ
5. Deployment — Service သို့ publish လုပ်ပြီး share လုပ်ပါ
6. Optimization — Performance ကိုစစ်ဆေးပြီး optimize လုပ်ပါ

### Practical Workshop

Exercise 1: Basic Report Creation
1. Open Power BI Desktop
2. Load sample data (Excel or CSV)
3. Create 3 visualizations (bar, line, table)
4. Add a slicer for filtering
5. Format and arrange on canvas
6. Save and publish

Exercise 2: Advanced Analysis
1. Create a calculated column
2. Write 2 DAX measures
3. Create a hierarchy
4. Add drill-through page
5. Configure row-level security
6. Test with different user roles

### Common Interview Questions

1. Power BI ၏အဓိက components များကိုဖော်ပြပါ။
2. Measure နှင့် Calculated Column ကွာခြားချက်ကိုရှင်းပြပါ။
3. Star Schema ဆိုတာဘာလဲ? ဘာကြောင့်အသုံးပြုရသလဲ။
4. CALCULATE function ရဲ့အလုပ်လုပ်ပုံကိုရှင်းပြပါ။
5. Import vs DirectQuery ဘယ်အချိန်မှာသုံးမလဲ?
6. Row-Level Security ကိုဘယ်လို implement လုပ်မလဲ?
7. Performance optimization techniques များကိုဖော်ပြပါ။
8. Power BI Service နဲ့ Power BI Desktop ကွာခြားချက်ကဘာလဲ?

### Troubleshooting Guide

| Issue | Check | Solution |
|-------|-------|----------|
| Data not loading | Connection settings | Check credentials and gateway |
| Wrong values | Measure formula | Review DAX context |
| Slow report | Performance Analyzer | Optimize measures and model |
| Refresh failure | Gateway status | Restart gateway service |
| Missing data | Relationship direction | Check cardinality |

### Resources

- Microsoft Learn: Power BI documentation
- DAX Guide: dax.guide (all DAX functions with examples)
- SQLBI: DAX patterns and best practices
- Power BI Community: forum for questions and answers
- GitHub: Sample datasets and report templates

### Best Practices Summary

1. Design with Star Schema — Fact + Dimensions
2. Use Measures over Calculated Columns — Better performance
3. Optimize Power Query — Filter early, remove unused columns
4. Implement RLS — Secure data by user role
5. Document Everything — Measures, model, data sources
6. Regular Performance Testing — Use Performance Analyzer
7. Version Control — Use Git for .pbip files
8. User Training — Train end users on report usage


## Comprehensive Guide and Examples

### Module Overview

ဤ module တွင် Power BI ၏အရေးကြီးသော concepts များနှင့်လက်တွေ့အသုံးချမှုများကိုလေ့လာရမည်ဖြစ်ပါသည်။

### Key Learning Objectives

1. Understand Core Concepts — Power BI ၏အခြေခံသဘောတရားများကိုနားလည်ရန်
2. Hands-on Practice — ကိုယ်တိုင်လက်တွေ့ဆောက်လုပ်နိုင်ရန်
3. Best Practices — အကောင်းဆုံးနည်းလမ်းများကိုလေ့လာရန်
4. Real-world Application — တကယ့်လုပ်ငန်းခွင်တွင်အသုံးချနိုင်ရန်

### Step-by-Step Learning Path

1. Concept Understanding — အခြေခံသဘောတရားများကိုလေ့လာပါ
2. Tool Setup — Power BI Desktop ကို install လုပ်ပြီး configure လုပ်ပါ
3. Sample Project — Sample data ဖြင့်လက်တွေ့ဆောက်လုပ်ပါ
4. Advanced Features — DAX, Power Query, AI features များကိုလေ့လာပါ
5. Deployment — Service သို့ publish လုပ်ပြီး share လုပ်ပါ
6. Optimization — Performance ကိုစစ်ဆေးပြီး optimize လုပ်ပါ

### Practical Workshop

Exercise 1: Basic Report Creation
1. Open Power BI Desktop
2. Load sample data (Excel or CSV)
3. Create 3 visualizations (bar, line, table)
4. Add a slicer for filtering
5. Format and arrange on canvas
6. Save and publish

Exercise 2: Advanced Analysis
1. Create a calculated column
2. Write 2 DAX measures
3. Create a hierarchy
4. Add drill-through page
5. Configure row-level security
6. Test with different user roles

### Common Interview Questions

1. Power BI ၏အဓိက components များကိုဖော်ပြပါ။
2. Measure နှင့် Calculated Column ကွာခြားချက်ကိုရှင်းပြပါ။
3. Star Schema ဆိုတာဘာလဲ? ဘာကြောင့်အသုံးပြုရသလဲ။
4. CALCULATE function ရဲ့အလုပ်လုပ်ပုံကိုရှင်းပြပါ။
5. Import vs DirectQuery ဘယ်အချိန်မှာသုံးမလဲ?
6. Row-Level Security ကိုဘယ်လို implement လုပ်မလဲ?
7. Performance optimization techniques များကိုဖော်ပြပါ။
8. Power BI Service နဲ့ Power BI Desktop ကွာခြားချက်ကဘာလဲ?

### Troubleshooting Guide

| Issue | Check | Solution |
|-------|-------|----------|
| Data not loading | Connection settings | Check credentials and gateway |
| Wrong values | Measure formula | Review DAX context |
| Slow report | Performance Analyzer | Optimize measures and model |
| Refresh failure | Gateway status | Restart gateway service |
| Missing data | Relationship direction | Check cardinality |

### Resources

- Microsoft Learn: Power BI documentation
- DAX Guide: dax.guide (all DAX functions with examples)
- SQLBI: DAX patterns and best practices
- Power BI Community: forum for questions and answers
- GitHub: Sample datasets and report templates

### Best Practices Summary

1. Design with Star Schema — Fact + Dimensions
2. Use Measures over Calculated Columns — Better performance
3. Optimize Power Query — Filter early, remove unused columns
4. Implement RLS — Secure data by user role
5. Document Everything — Measures, model, data sources
6. Regular Performance Testing — Use Performance Analyzer
7. Version Control — Use Git for .pbip files
8. User Training — Train end users on report usage


## Comprehensive Guide and Examples

### Module Overview

ဤ module တွင် Power BI ၏အရေးကြီးသော concepts များနှင့်လက်တွေ့အသုံးချမှုများကိုလေ့လာရမည်ဖြစ်ပါသည်။

### Key Learning Objectives

1. Understand Core Concepts — Power BI ၏အခြေခံသဘောတရားများကိုနားလည်ရန်
2. Hands-on Practice — ကိုယ်တိုင်လက်တွေ့ဆောက်လုပ်နိုင်ရန်
3. Best Practices — အကောင်းဆုံးနည်းလမ်းများကိုလေ့လာရန်
4. Real-world Application — တကယ့်လုပ်ငန်းခွင်တွင်အသုံးချနိုင်ရန်

### Step-by-Step Learning Path

1. Concept Understanding — အခြေခံသဘောတရားများကိုလေ့လာပါ
2. Tool Setup — Power BI Desktop ကို install လုပ်ပြီး configure လုပ်ပါ
3. Sample Project — Sample data ဖြင့်လက်တွေ့ဆောက်လုပ်ပါ
4. Advanced Features — DAX, Power Query, AI features များကိုလေ့လာပါ
5. Deployment — Service သို့ publish လုပ်ပြီး share လုပ်ပါ
6. Optimization — Performance ကိုစစ်ဆေးပြီး optimize လုပ်ပါ

### Practical Workshop

Exercise 1: Basic Report Creation
1. Open Power BI Desktop
2. Load sample data (Excel or CSV)
3. Create 3 visualizations (bar, line, table)
4. Add a slicer for filtering
5. Format and arrange on canvas
6. Save and publish

Exercise 2: Advanced Analysis
1. Create a calculated column
2. Write 2 DAX measures
3. Create a hierarchy
4. Add drill-through page
5. Configure row-level security
6. Test with different user roles

### Common Interview Questions

1. Power BI ၏အဓိက components များကိုဖော်ပြပါ။
2. Measure နှင့် Calculated Column ကွာခြားချက်ကိုရှင်းပြပါ။
3. Star Schema ဆိုတာဘာလဲ? ဘာကြောင့်အသုံးပြုရသလဲ။
4. CALCULATE function ရဲ့အလုပ်လုပ်ပုံကိုရှင်းပြပါ။
5. Import vs DirectQuery ဘယ်အချိန်မှာသုံးမလဲ?
6. Row-Level Security ကိုဘယ်လို implement လုပ်မလဲ?
7. Performance optimization techniques များကိုဖော်ပြပါ။
8. Power BI Service နဲ့ Power BI Desktop ကွာခြားချက်ကဘာလဲ?

### Troubleshooting Guide

| Issue | Check | Solution |
|-------|-------|----------|
| Data not loading | Connection settings | Check credentials and gateway |
| Wrong values | Measure formula | Review DAX context |
| Slow report | Performance Analyzer | Optimize measures and model |
| Refresh failure | Gateway status | Restart gateway service |
| Missing data | Relationship direction | Check cardinality |

### Resources

- Microsoft Learn: Power BI documentation
- DAX Guide: dax.guide (all DAX functions with examples)
- SQLBI: DAX patterns and best practices
- Power BI Community: forum for questions and answers
- GitHub: Sample datasets and report templates

### Best Practices Summary

1. Design with Star Schema — Fact + Dimensions
2. Use Measures over Calculated Columns — Better performance
3. Optimize Power Query — Filter early, remove unused columns
4. Implement RLS — Secure data by user role
5. Document Everything — Measures, model, data sources
6. Regular Performance Testing — Use Performance Analyzer
7. Version Control — Use Git for .pbip files
8. User Training — Train end users on report usage
