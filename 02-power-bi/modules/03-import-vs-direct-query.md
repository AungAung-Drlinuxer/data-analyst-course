# Module 3: Import Mode vs Direct Query Mode

## Import Mode

Data အားလုံးကို Power BI Desktop ၏ in-memory cache ထဲသို့ load လုပ်ပါသည်။

### Import Mode အားသာချက်များ
- မြန်ဆန်သော performance (in-memory)
- DAX functions အားလုံးသုံးနိုင်
- Power Query transformations အပြည့်အဝ
- Offline access ရနိုင်

### Import Mode အားနည်းချက်များ
- Dataset size ကိုကန့်သတ်ထား (Pro: 1GB, Premium: 100GB)
- Refresh လုပ်ရန်လိုအပ် (data ကသက်တမ်းရှိ)
- Memory consumption များ

## DirectQuery Mode

Data ကို original source မှတိုက်ရိုက် query လုပ်ပါသည်။

### DirectQuery အားသာချက်များ
- Real-time data
- Dataset size ကန့်သတ်ချက်မရှိ
- Data governance (source တွင်ပဲ security စီမံနိုင်)

### DirectQuery အားနည်းချက်များ
- Performance နှေးနိုင် (network round-trip)
- DAX functions အချို့ကန့်သတ်
- Time intelligence အတွက်ခက်ခဲ

### ဘယ် Mode ကိုရွေးမလဲ?

| Situation | Recommended Mode |
|-----------|-----------------|
| Data < 1GB, complex DAX | Import |
| Data > 1GB, real-time | DirectQuery |
| Frequent refresh needed | DirectQuery |
| Best performance | Import + Aggregations |

### Composite Models (2022+)

Import + DirectQuery + Aggregations ကိုပေါင်းစပ်အသုံးပြုနိုင်ပါသည်။ Large fact table ကို DirectQuery, small dimension tables ကို Import mode သုံးနိုင်ပါသည်။


## Performance Comparison Detail

### Import Mode Performance Factors

1. **Data Compression** — Power BI's VertiPaq engine သည် data ကိုအလွန်ကောင်းမွန်စွာ compress လုပ်ပါသည် (များသောအားဖြင့် 5-10x compression ratio)
2. **Columnar Storage** — Column-oriented storage သည် aggregation queries များအတွက်အလွန်မြန်ဆန်ပါသည်
3. **Query Cache** — ပထမဆုံး query run ပြီးပါက result ကို cache လုပ်ထားပါသည်

### DirectQuery Performance Factors

1. **Network Latency** — Every query = network round-trip to source
2. **Source Performance** — Source database ၏ query performance ပေါ်မူတည်ပါသည်
3. **Concurrency Limit** — Power BI Service က maximum 30 concurrent DirectQuery connections သာခွင့်ပြုပါသည်

### Hybrid Solutions

**Composite Models (2022+):**
- Large fact table → DirectQuery
- Small dimension tables → Import
- Aggregations → Import (pre-aggregated summaries)

**Dual Storage Mode:**
- Same table တွင် Import + DirectQuery ကိုတစ်ပြိုင်နက်သုံးနိုင်
- Power BI က query ပေါ်မူတည်ပြီးအကောင်းဆုံး mode ကိုအလိုအလျောက်ရွေးပေးပါသည်

### Decision Matrix

| Scenario | Recommended Mode | Rationale |
|----------|-----------------|-----------|
| Sales Dashboard (< 1M rows) | Import | Best performance |
| Real-time Operations Dashboard | DirectQuery | Fresh data required |
| Executive Summary (daily refresh) | Import | Performance > freshness |
| Data Warehouse (> 100M rows) | DirectQuery + Aggregations | Scale |
| Mobile Report | Import | Offline access |


## Detailed Explanation and Examples

### Practical Applications

Power BI ၏ feature များကိုလက်တွေ့အသုံးပြုရန် အောက်ပါအဆင့်များကိုလိုက်နာပါ-

1. **Data Preparation** — Power Query ဖြင့် data cleaning လုပ်ပါ
2. **Model Design** — Star Schema ကိုသုံးပြီး data model ဆောက်ပါ
3. **DAX Measures** — လိုအပ်သော calculations များရေးပါ
4. **Visualization** — သင့်တော်သော chart types များရွေးပါ
5. **Interactivity** — Slicers, Filters, Drill-through များထည့်ပါ
6. **Deployment** — Publish to Service, share with users

### Real-World Scenario

**Use Case:** Sales Dashboard တစ်ခုတည်ဆောက်ခြင်း

**Requirements:**
- Monthly sales by region (Line chart)
- Top 10 products by revenue (Bar chart)
- Sales vs Target by salesperson (Table with conditional formatting)
- YTD comparison with last year (KPI cards)
- Dynamic date range selector (Slicer)

**Steps:**
1. Import sales data from SQL Server (Import mode)
2. Create Calendar table with DAX
3. Build Star Schema: Sales (Fact) ↔ Products, Customers, Calendar (Dimensions)
4. Write DAX measures: Total Sales, Sales LY, Sales YTD, Sales vs Target
5. Create visualizations and arrange on canvas
6. Add slicers for date range, region, product category
7. Publish to Power BI Service and set up scheduled refresh

### Common Mistakes

1. **Too many visuals on one page** — 5-7 visuals max per page
2. **Wrong chart type** — Pie chart for > 5 categories, line chart for non-time data
3. **Ignoring performance** — Too many calculated columns, insufficient indexing
4. **Poor color choices** — Too many colors, low contrast, inaccessible for color-blind
5. **Missing context** — No titles, no axis labels, no data labels

### Performance Optimization Tips

- Reduce cardinality of columns (especially text)
- Use integer keys instead of text relationships
- Disable auto-date/time feature (File → Options → Data Load)
- Remove unnecessary columns and rows at source
- Use performance analyzer to identify slow visuals
- Consider aggregations for very large datasets
## Detailed Explanation and Examples

### Practical Applications

Power BI ၏ feature များကိုလက်တွေ့အသုံးပြုရန် အောက်ပါအဆင့်များကိုလိုက်နာပါ-

1. **Data Preparation** — Power Query ဖြင့် data cleaning လုပ်ပါ
2. **Model Design** — Star Schema ကိုသုံးပြီး data model ဆောက်ပါ
3. **DAX Measures** — လိုအပ်သော calculations များရေးပါ
4. **Visualization** — သင့်တော်သော chart types များရွေးပါ
5. **Interactivity** — Slicers, Filters, Drill-through များထည့်ပါ
6. **Deployment** — Publish to Service, share with users

### Real-World Scenario

**Use Case:** Sales Dashboard တစ်ခုတည်ဆောက်ခြင်း

**Requirements:**
- Monthly sales by region (Line chart)
- Top 10 products by revenue (Bar chart)
- Sales vs Target by salesperson (Table with conditional formatting)
- YTD comparison with last year (KPI cards)
- Dynamic date range selector (Slicer)

**Steps:**
1. Import sales data from SQL Server (Import mode)
2. Create Calendar table with DAX
3. Build Star Schema: Sales (Fact) ↔ Products, Customers, Calendar (Dimensions)
4. Write DAX measures: Total Sales, Sales LY, Sales YTD, Sales vs Target
5. Create visualizations and arrange on canvas
6. Add slicers for date range, region, product category
7. Publish to Power BI Service and set up scheduled refresh

### Common Mistakes

1. **Too many visuals on one page** — 5-7 visuals max per page
2. **Wrong chart type** — Pie chart for > 5 categories, line chart for non-time data
3. **Ignoring performance** — Too many calculated columns, insufficient indexing
4. **Poor color choices** — Too many colors, low contrast, inaccessible for color-blind
5. **Missing context** — No titles, no axis labels, no data labels

### Performance Optimization Tips

- Reduce cardinality of columns (especially text)
- Use integer keys instead of text relationships
- Disable auto-date/time feature (File → Options → Data Load)
- Remove unnecessary columns and rows at source
- Use performance analyzer to identify slow visuals
- Consider aggregations for very large datasets
## Detailed Explanation and Examples

### Practical Applications

Power BI ၏ feature များကိုလက်တွေ့အသုံးပြုရန် အောက်ပါအဆင့်များကိုလိုက်နာပါ-

1. **Data Preparation** — Power Query ဖြင့် data cleaning လုပ်ပါ
2. **Model Design** — Star Schema ကိုသုံးပြီး data model ဆောက်ပါ
3. **DAX Measures** — လိုအပ်သော calculations များရေးပါ
4. **Visualization** — သင့်တော်သော chart types များရွေးပါ
5. **Interactivity** — Slicers, Filters, Drill-through များထည့်ပါ
6. **Deployment** — Publish to Service, share with users

### Real-World Scenario

**Use Case:** Sales Dashboard တစ်ခုတည်ဆောက်ခြင်း

**Requirements:**
- Monthly sales by region (Line chart)
- Top 10 products by revenue (Bar chart)
- Sales vs Target by salesperson (Table with conditional formatting)
- YTD comparison with last year (KPI cards)
- Dynamic date range selector (Slicer)

**Steps:**
1. Import sales data from SQL Server (Import mode)
2. Create Calendar table with DAX
3. Build Star Schema: Sales (Fact) ↔ Products, Customers, Calendar (Dimensions)
4. Write DAX measures: Total Sales, Sales LY, Sales YTD, Sales vs Target
5. Create visualizations and arrange on canvas
6. Add slicers for date range, region, product category
7. Publish to Power BI Service and set up scheduled refresh

### Common Mistakes

1. **Too many visuals on one page** — 5-7 visuals max per page
2. **Wrong chart type** — Pie chart for > 5 categories, line chart for non-time data
3. **Ignoring performance** — Too many calculated columns, insufficient indexing
4. **Poor color choices** — Too many colors, low contrast, inaccessible for color-blind
5. **Missing context** — No titles, no axis labels, no data labels

### Performance Optimization Tips

- Reduce cardinality of columns (especially text)
- Use integer keys instead of text relationships
- Disable auto-date/time feature (File → Options → Data Load)
- Remove unnecessary columns and rows at source
- Use performance analyzer to identify slow visuals
- Consider aggregations for very large datasets
