# Module 18: Automate Data Tasks with Power Query

## 📌 Automation Features

### 1. Refreshing Data
1. Data tab → Queries & Connections
2. Right-click query → Properties
3. Set refresh schedule (every N minutes)
4. Or: Data → Refresh All

### 2. Parameters
1. Power Query → Manage Parameters
2. Create parameter (e.g., "SelectedMonth")
3. Use parameter in query filter
4. Change parameter → Query auto-updates

### 3. Loading to Data Model
1. Power Query → Close & Load To
2. "Add this data to the Data Model" (check)
3. Creates relationship-ready model
4. Use with Power Pivot for advanced analysis

### 4. Appending Queries
```powerquery
let
    Jan = Excel.CurrentWorkbook(){[Name="Jan"]}[Content],
    Feb = Excel.CurrentWorkbook(){[Name="Feb"]}[Content],
    Mar = Excel.CurrentWorkbook(){[Name="Mar"]}[Content],
    Combined = Table.Combine({Jan, Feb, Mar})
in
    Combined
```
→ Multiple sheets/tables ကိုပေါင်းမယ်

## ✅ Key Takeaways
- Power Query workflows တွေက auto-refresh လုပ်လို့ရ
- Parameters သုံးပြီး dynamic queries ဆောက်လို့ရ
- Append = SQL UNION / Merge = SQL JOIN
- Data Model က relationships နဲ့အတူ Pivot လုပ်လို့ရ
