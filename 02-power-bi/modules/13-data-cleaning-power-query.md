# Module 13: Data Cleaning & Transformation (Power Query)

## Power Query ဆိုတာဘာလဲ?

Power Query သည် Power BI ၏ data transformation engine ဖြစ်ပြီး M language ကိုအသုံးပြုပါသည်။ Data များကို source မှ load လုပ်ပြီး cleaning, transformation, merging စသည့်လုပ်ငန်းများကိုလုပ်ဆောင်ပါသည်။ Power Query သည် Excel, Power BI, Azure Data Factory, Microsoft Fabric တို့တွင်လည်းအသုံးပြုနိုင်ပါသည်။

## Common Transformations - Column Operations

1. **Rename** — Right-click column → Rename
2. **Remove** — Select column → Remove Columns
3. **Reorder** — Drag columns to desired position
4. **Split Column** — By delimiter (comma, space) or by number of characters
5. **Merge Columns** — Combine multiple columns with separator
6. **Pivot Column** — Transform unique values into columns
7. **Unpivot Columns** — Transform columns into rows (very important for data normalization)
8. **Change Data Type** — Text, Number, Date, etc.
9. **Add Column from Examples** — AI-powered column generation
10. **Conditional Column** — IF-THEN-ELSE logic

## Common Transformations - Row Operations

1. **Remove Top/Bottom Rows** — Headers, unnecessary rows
2. **Keep Top/Bottom Rows** — Sample data
3. **Remove Duplicates** — Deduplicate based on one or more columns
4. **Filter Rows** — Column dropdown → Text/Number/Date filters
5. **Sort Rows** — Ascending/Descending
6. **Keep/Remove Errors** — Handle transformation errors

## M Language မိတ်ဆက်

Power Query သည် M Language ကိုအသုံးပြုပြီး လုပ်ဆောင်ချက်တစ်ခုချင်းစီကို step အလိုက်မှတ်တမ်းတင်ပါသည်။

```m
let
    Source = Sql.Database("server", "database"),
    SalesTable = Source{[Schema="dbo",Item="Sales"]}[Data],
    FilteredRows = Table.SelectRows(SalesTable, each [Amount] > 1000),
    GroupedData = Table.Group(FilteredRows, {"Region"}, {{"Total", each List.Sum([Amount]), type number}})
in
    GroupedData
```

## Power Query Best Practices

1. **Steps ကို Rename လုပ်ပါ** — Query Settings pane တွင် step တစ်ခုချင်းစီကို right-click → Properties → Rename
2. **Source-level filter လုပ်ပါ** — Data များများရှိလျှင် source တွင်ပဲ filter လုပ်ပြီးမှ load လုပ်ပါ
3. **Reference vs Duplicate** — Reference = same source query ကိုပြန်သုံးသည် (query folding); Duplicate = copy လုပ်သည်
4. **Column type ကိုစောစောသတ်မှတ်ပါ** — Date/Number columns များကိုစောစောသတ်မှတ်ပါ
5. **Remove Columns** — မလိုအပ်သော columns များကိုဖယ်ရှားပါ (performance)



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
