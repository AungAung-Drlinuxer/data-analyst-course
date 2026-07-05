# Module 13: Pivot Table Multiple Sheets

## 📌 ဒီ Module မှာလေ့လာရမည့်အကြောင်းအရာများ
- Sheets များစွာက Data ပေါင်းပြီး Pivot Table ဆောက်နည်း
- Power Pivot မိတ်ဆက်
- Consolidate Function

## Method 1: Alt + D + P (PivotTable Wizard)

1. Alt + D + P နှိပ်ပါ (or Quick Access Toolbar ထဲထည့်)
2. "Multiple consolidation ranges" ကိုရွေးပါ
3. Next → I will create the page fields
4. Each sheet's range ကိုထည့်ပါ
5. Finish

## Method 2: Power Pivot (Excel 365)

1. Data Tab → Get Data → From File → From Workbook
2. ပေါင်းချင်တဲ့ Sheets တွေကိုရွေးပါ
3. Power Pivot Editor ထဲမှာ Relationships ဆောက်ပါ
4. PivotTable ဆောက်ပါ

## Method 3: Consolidate

1. Data → Consolidate
2. Function: Sum
3. Sheet1 range ထည့်ပါ → Add
4. Sheet2 range ထည့်ပါ → Add
5. Sheet3 range ထည့်ပါ → Add
6. "Top row" + "Left column" check → OK

## ✅ Key Takeaways
- Alt + D + P က classic way for multi-sheet Pivot
- Power Pivot က big data အတွက်သုံး
- Consolidate က simple summary အတွက်သုံး
