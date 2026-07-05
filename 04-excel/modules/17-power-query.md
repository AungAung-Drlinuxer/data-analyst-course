# Module 17: Excel Power Query Tutorial

## 📌 Power Query ဆိုတာဘာလဲ?
Data Transformation & Cleaning Tool ပါ။ Excel 2016 ကစပြီး built-in ပါတယ်။

## Power Query ကိုဘယ်လိုဖွင့်မလဲ?
Data Tab → Get & Transform Data → From Table/Range

## Power Query Editor

### Basic Operations
```
Home Tab:
├── Close & Load
├── Remove Rows (Remove Top/Remove Bottom)
├── Keep Rows
├── Split Column
├── Group By
└── Merge Queries

Transform Tab:
├── Replace Values
├── Pivot/Unpivot Columns
├── Extract (Length, First characters)
├── Parse (JSON, XML)
└── Data Type
```

## လက်တွေ့ဥပမာ: dirty_data.csv ကို Clean လုပ်ခြင်း

### Step-by-Step:
1. Data → From Table/Range → Select dirty_data
2. Remove Duplicates (Home → Remove Duplicates)
3. Replace null values (Transform → Replace Values)
4. Split Names (if needed)
5. Fix Date formats
6. Close & Load

## M Language (Power Query Formula)
```powerquery
let
    Source = Excel.CurrentWorkbook(){[Name="Table1"]}[Content],
    #"Removed Duplicates" = Table.Distinct(Source, {"ID"}),
    #"Replaced Value" = Table.ReplaceValue(#"Removed Duplicates", null, 0, Replacer.ReplaceValue, {"Amount"})
in
    #"Replaced Value"
```

## ✅ Key Takeaways
- Power Query က Excel ထဲမှာ built-in ETL tool
- Repeatable workflow — တစ်ခါသတ်မှတ်ရင် ထပ်သုံးလို့ရ
- M Language က advanced transformation အတွက်သုံး
- Merge Queries နဲ့ Join လုပ်နိုင် (SQL JOIN လိုပါပဲ)
