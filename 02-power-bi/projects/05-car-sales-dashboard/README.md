# Car Sales Dashboard 🚗

## Domain: Automotive

---

## 📋 Project Overview

ကားရောင်းဝယ်ရေးလုပ်ငန်းအတွက် sales performance, inventory turnover, seasonal patterns များကို dashboard ဖြင့်ခွဲခြမ်းစိတ်ဖြာခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — car_sales.csv (800 rows) + car_inventory.csv (300 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `sale_id` | အရောင်းနံပါတ် | Integer |
| `date` | ရက်စွဲ | Date |
| `make` | ကားအမှတ်တံဆိပ် | String |
| `model` | မော်ဒယ် | String |
| `year` | ထုတ်လုပ်သည့်နှစ် | Integer |
| `body_style` | ကိုယ်ထည်ပုံစံ | String |
| `mileage` | မိုင်နံပါတ် | Integer |
| `condition` | အခြေအနေ | String |
| `price` | စျေးနှုန်း ($) | Float |
| `sale_price` | အရောင်းစျေး ($) | Float |
| `payment_type` | ငွေပေးချေမှုပုံစံ | String |
| `financing_bank` | ဘဏ် | String |


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
// Total Revenue = SUM(car_sales[sale_price])\n// Avg Price = AVERAGE(car_sales[sale_price])\n// Inventory Turn = SUM(inventory[days_in_lot]) / COUNTROWS(inventory)\n// Days on Lot Avg = AVERAGE(car_inventory[days_in_lot])
```

---

## 📊 Dashboard Visuals & Tools

Matrix, Gauge, Decomposition Tree, Scatter, Slicers

---

## 💼 Business Problem Solved

### Problem
```
Dealership တွင်: Inventory turnover နှေးနေပြီး ဘယ် model က slow-moving လဲမသိ။ Price trend ကိုခြေရာခံရန်ခက်ခဲ။ Financing options က sales ကိုဘယ်လိုသက်ရောက်လဲဆိုတာမသိ။
```

### Solution
```diff
+ Matrix Brand×Model + Gauge for Targets + Decomposition Tree for Root Cause + Inventory Aging Report
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
