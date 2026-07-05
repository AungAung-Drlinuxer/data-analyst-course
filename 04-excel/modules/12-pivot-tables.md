# Module 12: Pivot Tables

## 📌 ဒီ Module မှာလေ့လာရမည့်အကြောင်းအရာများ
- Pivot Table ဆိုတာဘာလဲ
- Pivot Table ဖန်တီးနည်း
- Rows, Columns, Values, Filters
- Pivot Table ထဲမှာ တွက်ချက်ခြင်း
- Slicers & Timelines

## Pivot Table ဆိုတာဘာလဲ?
Pivot Table သည် Data တွေကို အလွယ်တကူ အနှစ်ချုပ်ပြီး Analyze လုပ်နိုင်တဲ့ Tool တစ်ခုပါ။

## Pivot Table ဖန်တီးနည်း
1. Data ရှိတဲ့ Cell ထဲမှာ Click ပါ
2. Insert → PivotTable
3. Range ကို Auto-select လုပ်ပေးပါလိမ့်မယ်
4. New Worksheet ကိုရွေးပါ → OK

### Pivot Table Fields
```
PivotTable Fields Pane:
├── FILTERS          → Overall filter (e.g., Year)
├── COLUMNS          → Column headers (e.g., Quarter)
├── ROWS             → Row headers (e.g., Category)
└── VALUES           → Numbers to aggregate (e.g., Sum of Sales)
```

### လက်တွေ့ဥပမာ: Sales by Region
```
Rows:     Region
Columns:  Category
Values:   Sum of Total

= ဒေသအလိုက် Category အရောင်းပမာဏ
```

## Value Field Settings
- Sum (ပေါင်း) — default for numbers
- Count (ရေတွက်) — default for text
- Average (ပျမ်းမျှ)
- Max / Min
- % of Grand Total

## Calculated Field (Pivot Table ထဲမှာ Formula)
```
PivotTable Analyze → Fields, Items & Sets → Calculated Field
Name: "Profit Margin"
Formula: = Total * 0.2
```

## ✅ Key Takeaways
- Pivot Table က data ကိုအလွယ်တကူ summarize လုပ်တယ်
- Drag & Drop Interface — ဆွဲထည့်ရုံပဲ
- Values ကိုအမျိုးမျိုးပြောင်းလို့ရ (Sum, Count, Average)
- Slicer နဲ့ Timeline က interactive filtering အတွက်သုံး
