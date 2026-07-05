# Module 23: How to Use ChatGPT to Build Excel Dashboards

## 📌 ChatGPT နဲ့ Excel တွဲသုံးခြင်း

### 1. Formula တွေရေးဖို့ ChatGPT ကိုသုံးခြင်း

**Prompt:**
```
"Write an Excel formula to calculate commission:
- If Sales > 10000 → 10% commission
- If Sales > 5000 → 7% commission
- Otherwise → 5% commission"
```

**ChatGPT Output:**
```excel
=IF(A2>10000, A2*0.1, IF(A2>5000, A2*0.07, A2*0.05))
```

### 2. VBA Code ရေးဖို့ ChatGPT ကိုသုံးခြင်း

**Prompt:**
```
"Write a VBA macro that:
1. Formats header row with blue background
2. Auto-fits columns
3. Adds a sum row at bottom
4. Shows a message when done"
```

### 3. Dashboard Layout Design

**Prompt:**
```
"Design a sales dashboard layout in Excel with:
- Monthly sales trend line chart
- Top 5 products bar chart
- Regional breakdown pie chart
- KPI cards for Total Sales, Growth %, Active Customers
- Slicers for Date range and Region"
```

### 4. Data Analysis Assistance

**Prompt:**
```
"I have sales data with columns: Date, Product, Region, Sales, Profit.
What analysis should I do to find:
- Most profitable product?
- Best performing region?
- Seasonal patterns?"
```

### 5. Excel Troubleshooting

**Prompt:**
```
"My VLOOKUP is returning #N/A. My formula is:
=VLOOKUP(A2, Prices!A:D, 4, FALSE)
What could be wrong?"
```

## 💡 Best ChatGPT Prompts for Excel

| Task | Prompt Pattern |
|------|---------------|
| Write Formula | "Write Excel formula for..." |
| Explain Formula | "Explain what this Excel formula does: =SUMIFS(...)" |
| Fix Error | "My Excel formula shows [error], fix it: [formula]" |
| Create Macro | "Write VBA code to..." |
| Design Dashboard | "Suggest dashboard layout for..." |
| Data Analysis | "Analyze this Excel data pattern: [describe]" |

## ✅ Key Takeaways
- ChatGPT က Excel Formulas, VBA, Dashboard Design အတွက်ကူညီနိုင်
- Clear prompts တွေရေးတတ်ဖို့လိုတယ်
- ChatGPT output ကို verify လုပ်ပြီးမှသုံးပါ
- Complex task တွေကို step-by-step ခွဲမေးပါ
