# Module 28: Interview Questions & Answers

## Beginner Level

**Q: Measure vs Calculated Column ကွာခြားချက်ကဘာလဲ?**
A: Measure သည် query time တွင်တွက်သည် (dynamic, no storage)။ Calculated Column သည် refresh time တွင်တွက်ပြီး model တွင်သိမ်းသည် (uses RAM)။

**Q: Star Schema ဆိုတာဘာလဲ?**
A: Central fact table (transactions) နှင့် surrounding dimension tables (descriptive data) များပါဝင်သော data model ဖြစ်ပါသည်။

**Q: Import vs DirectQuery ကွာခြားချက်?**
A: Import = data ကို memory ထဲသို့ load; DirectQuery = source မှတိုက်ရိုက် query (real-time but slower)

## Intermediate Level

**Q: CALCULATE function ရဲ့အလုပ်လုပ်ပုံကိုရှင်းပြပါ။**
A: CALCULATE သည် filter context ကိုပြောင်းလဲပေးပြီး expression ကိုတွက်ချက်ပါသည်။ ၎င်းသည် DAX ၏အရေးကြီးဆုံး function ဖြစ်ပါသည်။

**Q: Time Intelligence ကိုဘယ်လိုသုံးမလဲ?**
A: Calendar table လိုအပ်ပါသည်။ TOTALYTD, SAMEPERIODLASTYEAR, DATEADD စသည့် functions များသုံးနိုင်ပါသည်။

## Advanced Level

**Q: Performance နှေးသော report ကိုဘယ်လို optimize လုပ်မလဲ?**
A: 1. Performance Analyzer ဖြင့်စစ်ဆေး 2. Star Schema သုံး 3. Calculated columns များကို Power Query သို့ပြောင်း 4. Aggregations သုံး

**Q: RLS ကိုဘယ်လို setup လုပ်မလဲ?**
A: Desktop → Modeling → Manage Roles → DAX Filter → Publish → Service → Assign Users


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
