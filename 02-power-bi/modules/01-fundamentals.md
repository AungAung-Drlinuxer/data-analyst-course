# Module 1: Power BI Fundamentals & Overview

## Power BI ဆိုတာဘာလဲ?

Power BI သည် Microsoft မှထုတ်လုပ်သော Business Intelligence (BI) ကိရိယာတစ်ခုဖြစ်ပြီး Data များကို Visualization, Analysis, Reporting ပြုလုပ်ရန် အသုံးပြုပါသည်။ Power BI သည် Self-Service BI tool တစ်ခုဖြစ်ပြီး non-technical users များပင် data analysis များကိုလွယ်ကူစွာလုပ်ဆောင်နိုင်ပါသည်။

Power BI သည် အောက်ပါအဓိကအစိတ်အပိုင်းများဖြင့်ဖွဲ့စည်းထားပါသည်-

### Power BI Components

1. **Power BI Desktop** — Free desktop application ဖြစ်ပြီး reports များကိုတည်ဆောက်ရန်အသုံးပြုပါသည်။ Data connection, transformation, modeling, visualization အားလုံးကိုဤနေရာတွင်လုပ်ဆောင်ပါသည်။

2. **Power BI Service** — Cloud-based platform ဖြစ်ပြီး reports များကို publish, share, collaborate ပြုလုပ်ရန်အသုံးပြုပါသည်။ Scheduled refresh, row-level security, workspace management များကိုဤနေရာတွင်စီမံပါသည်။

3. **Power BI Mobile** — iOS, Android, Windows Mobile အတွက် apps များဖြစ်ပြီး road warriors များအတွက်သင့်တော်ပါသည်။

4. **Power BI Report Builder** — Paginated reports (print-ready, pixel-perfect) များဆောက်ရန်အသုံးပြုပါသည်။

5. **Power BI Embedded** — ISVs များအတွက် Power BI reports များကို ၎င်းတို့၏ applications များတွင် embed လုပ်ရန်အသုံးပြုပါသည်။

### Power BI Desktop Interface

Power BI Desktop ကိုဖွင့်လိုက်ပါက အောက်ပါအစိတ်အပိုင်းများကိုတွေ့ရပါမည်-

1. **Ribbon/Toolbar** — အပေါ်ဆုံးမှာရှိပြီး Home, Insert, Modeling, View, Help tabs များပါဝင်ပါသည်
2. **Canvas** — Report ရေးဆွဲရာနေရာ (visuals များကိုဤနေရာတွင်ထည့်ပါသည်)
3. **Visualizations Pane** — ညာဘက်တွင်ရှိပြီး chart အမျိုးအစားများ၊ field wells များပါဝင်ပါသည်
4. **Fields Pane** — Data model ထဲမှ column များစာရင်း
5. **Filters Pane** — Visual, Page, Report level filters များထားရှိရန်
6. **Pages Tab** — အောက်ခြေမှာရှိပြီး report pages များကိုစီမံရန်
7. **View Options** — Mobile layout, bookmarks, selection pane

### Power BI Architecture

Power BI ၏အလုပ်လုပ်ပုံကိုအဆင့်ဆင့်လေ့လာပါမည်-

**Data Sources → Power Query → Data Model → DAX → Visualizations → Dashboard → Service**

ပထမဆုံး data sources (SQL, Excel, API) များမှ data ကိုဆွဲယူပြီး Power Query ဖြင့် cleaning/transformation လုပ်ပါသည်။ ထို့နောက် data model ထဲတွင် relationships များတည်ဆောက်ပြီး DAX measures များရေးသားပါသည်။ နောက်ဆုံးတွင် visualizations များထည့်ကာ Service သို့ publish လုပ်ပါသည်။

### Power BI vs Traditional Tools

| Feature | Excel | Tableau | Power BI |
|---------|-------|---------|----------|
| Max Data Size | 1M rows | 100M+ | Unlimited (via DirectQuery) |
| Data Refresh | Manual | Manual/Scheduled | Scheduled (Service) |
| Collaborations | File sharing | Server-based | Workspace + Apps |
| Mobile Access | Limited | Good | Excellent |
| Cost | Part of Office | Expensive | Free Desktop / Low-cost Service |
| Learning Curve | Low (familiar) | Medium | Low-Medium |
| AI Features | Limited | Some | Built-in (Key Influencers, Q&A) |

### စတင်အသုံးပြုခြင်း

1. Microsoft Store မှ Power BI Desktop ကို download လုပ်ပါ (Free)
2. Power BI Desktop ကိုဖွင့်ပါ
3. Get Data → Excel/CSV/Database ကိုရွေးပါ
4. Data ကို load လုပ်ပါ
5. Visualizations pane မှ chart တစ်ခုကို click လုပ်ပြီး fields များကိုဆွဲထည့်ပါ
6. Report ကို .PBIX file အနေဖြင့် save လုပ်ပါ
7. Publish to Power BI Service ဖြင့် share လုပ်ပါ

### Power BI License Types

| License | Price | Features |
|---------|-------|----------|
| Free | $0 | Desktop only, cannot publish to Service |
| Pro | $10/user/month | Publish to Service, share reports, 1GB dataset limit |
| Premium Per User | $20/user/month | Larger datasets (100GB), AI features, more refreshes |
| Premium Capacity | ~$5K/month | Unlimited users, dedicated capacity, 100TB datasets |

### လေ့ကျင့်ခန်း

1. Power BI Desktop ကို install လုပ်ပါ
2. Sample Excel file တစ်ခုကို open လုပ်ပြီး data ကို load လုပ်ပါ
3. Bar chart တစ်ခုဆွဲပါ
4. Report ကို save လုပ်ပြီ� Publish လုပ်ကြည့်ပါ (Pro license ရှိလျှင်)


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
6. Add slicers for date range, region, product