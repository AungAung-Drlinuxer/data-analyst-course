# Module 9: Filters & Interactivity

## Filter အမျိုးအစားများ

Power BI တွင် filter အမျိုးအစား ၄ မျိုးရှိပြီး ၎င်းတို့မှာ - Visual Level, Page Level, Report Level, နှင့် Drill-through filters တို့ဖြစ်ပါသည်။

### 1. Visual Level Filter
Visual တစ်ခုချင်းစီအတွက်သာသက်ရောက်ပါသည်။ Visual ကိုရွေးပြီး Filters pane တွင် filter ထည့်နိုင်ပါသည်။

### 2. Page Level Filter
Page တစ်ခုလုံးရှိ visual အားလုံးကိုသက်ရောက်ပါသည်။

### 3. Report Level Filter
Report page အားလုံးကိုသက်ရောက်ပါသည်။

### 4. Drill-through Filter
Page တစ်ခုမှတစ်ခုသို့ context ယူသွားခြင်း။

### Filter Types

| Type | Description |
|------|-------------|
| Basic Filter | Checkbox list |
| Advanced Filter | Contains, Starts with, Between |
| Top N Filter | Top/Bottom N values |
| Relative Date Filter | Last 30 days, This year |
| Relative Time Filter | Last hour, Today |
| Numeric Filter | Greater than, Between |
| Text Filter | Contains, Is exactly |

### Visual Interactions

Visual တစ်ခုကိုရွေးချယ်ပါက အခြား visual များကိုမည်သို့သက်ရောက်မည်ကိုသတ်မှတ်နိုင်ပါသည်။

| Interaction | Description |
|-------------|-------------|
| Cross-filter | ဆက်စပ် data ကိုစစ်ထုတ်မည် |
| Cross-highlight | ဆက်စပ် data ကိုအရောင်ပြမည် |
| None | သက်ရောက်မှုမရှိ |


## Practical Examples

### Example 1: Basic Setup
Power BI Desktop တွင် data source များကိုချိတ်ဆက်ပြီး report များဆောက်ရန်:
1. Get Data → Select Source → Load
2. Visualizations Pane → Select Chart → Drag Fields
3. Format → Adjust Colors, Labels, Titles
4. Save → Publish to Service

### Example 2: Advanced Techniques
- Use bookmarks for storytelling
- Use buttons for navigation
- Use tooltips for additional context
- Use drill-through for detailed analysis

### Best Practices

1. **Keep it simple** — ရှုပ်ထွေးသော visual ထက်ရှင်းလင်းသော visual ကပိုကောင်းပါသည်
2. **Consistent design** — Color scheme, font, layout ကိုတစ်ပြေးညီထားပါ
3. **User feedback** — Report ကို actual users များနှင့်စမ်းသပ်ပါ
4. **Documentation** — Report အတွက် documentation ရေးထားပါ
5. **Performance** — Performance Analyzer ဖြင့်စစ်ဆေးပါ

### Common Issues and Solutions

| Issue | Cause | Solution |
|-------|-------|----------|
| Slow refresh | Large dataset, complex transformations | Use incremental refresh |
| Visual too slow | Too many data points | Use filters, reduce cardinality |
| Memory error | Dataset too large | Reduce columns, use aggregations |
| Wrong totals | Measure context issue | Review DAX formula |
| Data mismatch | Relationship issue | Check cardinality and direction |


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
