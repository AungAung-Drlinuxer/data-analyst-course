# Module 24: Top Excel Interview Questions

## 📌 အမေးများဆုံး Excel Interview Questions

### အခြေခံအဆင့် (Entry Level)

**Q1. What is the difference between COUNT and COUNTA?**
```
COUNT → Number ပါတဲ့ Cell တွေကိုပဲရေတွက်
COUNTA → Data ရှိတဲ့ Cell အားလုံးကိုရေတွက် (Text, Number, etc.)
```

**Q2. How do you remove duplicates in Excel?**
```
Data Tab → Remove Duplicates → Select columns → OK
```

**Q3. What is Freeze Panes used for?**
```
Header Row တွေကို Scroll လုပ်တဲ့အခါမပျောက်အောင်
View → Freeze Panes → Freeze Top Row
```

**Q4. Explain VLOOKUP and its limitations.**
```
=VLOOKUP(value, table, col_num, FALSE)
Limitations:
- Lookup column must be first column
- Can't look to the left
- Slow on large datasets
- XLOOKUP က ပိုကောင်းတယ်
```

### အလယ်အလတ်အဆင့် (Mid Level)

**Q5. What is the difference between Pivot Table and VLOOKUP?**
```
Pivot Table: Summarize & aggregate data quickly
VLOOKUP: Retrieve specific data from another table
```

**Q6. Explain INDEX-MATCH vs VLOOKUP.**
```
INDEX-MATCH က VLOOKUP ထက်ပိုပြီး flexible:
- Lookup column anywhere
- Faster on large data
- Can do 2-way lookups
```

**Q7. What is Power Query?**
```
Data transformation tool in Excel
- Import from multiple sources
- Clean & transform data
- Create repeatable workflows
```

### အဆင့်မြင့် (Advanced Level)

**Q8. How do you create a dynamic dashboard in Excel?**
```
- Use Excel Tables (Ctrl + T) for auto-expanding ranges
- Use Pivot Tables + Slicers for interactivity
- Use named ranges + OFFSET/INDEX for dynamic charts
- Add timelines for date filtering
```

**Q9. Explain XLOOKUP and how it improves on VLOOKUP.**
```
=XLOOKUP(lookup, lookup_array, return_array, [not_found], [match_mode])
Improvements:
- Can search left or right
- Built-in error handling
- Optional search mode (first-to-last or last-to-first)
```

**Q10. How do you automate repetitive tasks in Excel?**
```
1. Record Macro (View → Macros → Record)
2. VBA code editing (Alt + F11)
3. Power Query for data transformation automation
4. Scheduled refresh for connected data sources
```

**Q11. How do you connect to external data sources?**
```
Data Tab → Get Data:
├── From File (Excel, CSV, Text)
├── From Database (SQL Server, Access)
├── From Azure
├── From Power BI
└── From Other Sources (Web, ODBC, OData)
```

### Bonus: Practical Scenario Questions

**Q12. Walk me through how you'd analyze sales data.**
```
Step 1: Data Cleaning (Remove duplicates, fix formats)
Step 2: Power Query (Transform/merge if needed)
Step 3: Pivot Tables (Summarize by product, region, month)
Step 4: Charts (Line for trends, Bar for comparison)
Step 5: Dashboard (KPIs + Slicers + Timeline)
Step 6: Insights (Top products, growth areas, recommendations)
```

**Q13. How do you handle errors in Excel?**
```excel
=IFERROR(VLOOKUP(A2, B:C, 2, FALSE), "Not Found")
=IF(ISNA(VLOOKUP(A2, B:C, 2, FALSE)), "Missing", VLOOKUP(...))
```

**Q14. What Excel formulas do you use daily?**
```
SUM, AVERAGE, COUNT, IF, VLOOKUP/XLOOKUP
SUMIFS/COUNTIFS (condition-based calculations)
TEXT, LEFT/RIGHT/MID (text manipulation)
DATE functions (date calculations)
INDEX-MATCH (advanced lookups)
```

## ✅ Interview Tips
- Concept ကိုနားလည်မှရမယ် — formula အလွတ်ကျက်တာမလုံလောက်
- လက်တွေ့အသုံးချပုံကိုပြောပြနိုင်ရမယ်
- Limitations တွေကိုသိထားပါ (e.g., VLOOKUP limitations vs XLOOKUP)
- Shortcut keys တွေကိုသုံးပြနိုင်ရမယ် (Ctrl + T, Alt + F11)
- Portfolio ထဲမှာ dashboard/project တွေထည့်ပြပါ
