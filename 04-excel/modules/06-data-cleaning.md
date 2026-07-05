# Module 06: Data Cleaning in Excel

## 📌 ဒီ Module မှာလေ့လာရမည့်အကြောင်းအရာများ
- Data Cleaning ဆိုတာဘာလဲ
- Remove Duplicates
- Text to Columns
- Flash Fill
- Find & Replace
- TRIM, CLEAN Functions

## Data Cleaning ဆိုတာဘာလဲ?
Data တွေ မသုံးခင် သန့်ရှင်းအောင်လုပ်တာပါ။ မသန့်ရှင်းရင် analysis မှားနိုင်တယ်။

## Key Functions
```excel
=TRIM(A1)          // Extra spaces တွေကိုဖယ်
=CLEAN(A1)         // Non-printable characters ဖယ်
=UPPER(A1)         // စာလုံးအကြီးပြောင်း
=LOWER(A1)         // စာလုံးအသေးပြောင်း
=PROPER(A1)        // စာလုံးပထမလုံးကိုအကြီးပြောင်း
=SUBSTITUTE(A1, "old", "new")   // Text အစားထိုး
```

## Remove Duplicates
1. Data Tab → Remove Duplicates
2. Column(s) ရွေးပါ
3. OK → Duplicates တွေကိုဖယ်ရှားမယ်

## Walkthrough: Clean dirty_data.csv
```
1. Open datasets/raw/dirty_data.csv
2. Remove Duplicates (ID column)
3. TRIM Names → =TRIM(B2)
4. Find Invalid Emails → =IF(ISNUMBER(FIND("@",C2)),"Valid","Invalid")
5. Fix Dates → Use Text to Columns or DATEVALUE
6. Replace Blank Cells → Find & Select → Go to Special → Blanks
7. Remove Negative Values → Filter → Number Filters → Less than 0
```

## ✅ Key Takeaways
- Data Cleaning က analysis မလုပ်ခင် အရေးကြီးဆုံးအဆင့်
- Remove Duplicates က data quality အတွက်ပထမဆုံးလုပ်ရန်
- TRIM, CLEAN, SUBSTITUTE တို့က text cleaning အတွက်သုံး
