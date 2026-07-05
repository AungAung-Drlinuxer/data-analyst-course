# Pizza Sales Dashboard 🍕

## Domain: Food Service

---

## 📋 Project Overview

ပီဇာဆိုင်တစ်ဆိုင်အတွက် sales analysis dashboard — popular items, peak hours, category performance များကိုခွဲခြမ်းစိတ်ဖြာခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — pizza_orders.csv (2000 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `order_id` | မှာယူမှုနံပါတ် | Integer |
| `order_date` | ရက်စွဲ | Date |
| `order_time` | အချိန် | Time |
| `pizza_name` | ပီဇာအမည် | String |
| `pizza_category` | အမျိုးအစား | String |
| `pizza_size` | အရွယ် | String |
| `quantity` | အရေအတွက် | Integer |
| `unit_price` | တစ်ခုချင်းစျေး ($) | Float |
| `total_price` | စုစုပေါင်းစျေး ($) | Float |


---

## 🔌 PowerBI Data Import

```
Get Data → Text/CSV → datasets/raw/*.csv
→ Transform Data (Power Query)
→ Create Relationships
→ Build DAX Measures
→ Design Dashboard
```

---

## 📐 Core DAX Measures

```dax
// Total Revenue = SUM(pizza_orders[total_price])\n// Total Orders = COUNTROWS(pizza_orders)\n// Avg Order Value = DIVIDE([Total Revenue],[Total Orders])\n// Peak Hour = TOPN(1, VALUES(pizza_orders[order_time]), [Total Orders])
```

---

## 📊 Dashboard Visuals & Tools

Bar Chart, Line Chart, Matrix, Stacked Bar, Slicers

---

## 💼 Business Problem Solved

### Problem
```
ပီဇာဆိုင်တွင်: Inventory waste များနေ — ဘယ် pizza က slow-moving လဲ? Peak time မှာ staff လုံလောက်ရဲ့လား? ဘယ်နေ့ဘယ်အချိန်က busy ဆုံးလဲ?
```

### Solution
```diff
+ Best/Worst Selling Pizza analysis + Peak Hours Staff Scheduling + Category Revenue Analysis + Day×Category Matrix
```

---

## 🧪 လက်တွေ့စမ်းသပ်ရန်

1. PowerBI Desktop ကိုဖွင့်ပါ → `Get Data` → CSV ကိုရွေးပါ
2. Power Query တွင် data cleaning လုပ်ပါ (remove nulls, change types)
3. Data model တွင် relationships တည်ဆောက်ပါ
4. DAX measures များကို ရိုက်ထည့်ပါ
5. Visuals များကို configure လုပ်ပါ
6. Dashboard ကို publish လုပ်ပါ (PowerBI Service)

---

## 📝 Dataset Notes
- Dataset သည် synthetic data ဖြစ်ပြီး real-world scenario ကိုအခြေခံထားပါသည်
- `datasets/raw/` တွင် full dataset, `datasets/sample/` တွင် sample data ရှိပါသည်
- PowerBI Desktop ဖြင့် လက်တွေ့စမ်းသပ်နိုင်ပါသည်
