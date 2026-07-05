# Blinkit Analysis ⚡

## Domain: Quick Commerce

---

## 📋 Project Overview

Blinkit (Quick Commerce) Data ကိုခွဲခြမ်းစိတ်ဖြာပြီး Delivery Performance, SKU Analysis, Zone-wise Metrics များကို Dashboard ဖြင့်ပြသခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — blinkit_orders.csv (1500 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `order_id` | မှာယူမှုနံပါတ် | Integer |
| `zone` | ဇုန် | String |
| `category` | အမျိုးအစား | String |
| `sku` | SKU ကုဒ် | String |
| `order_qty` | အရေအတွက် | Integer |
| `unit_price` | တစ်ခုချင်းစျေး | Float |
| `delivery_fee` | ပို့ဆောင်ခ | Float |
| `estimated_delivery_min` | ခန့်မှန်းပို့ချိန် | Integer |
| `actual_delivery_min` | တကယ့်ပို့ချိန် | Integer |
| `delivery_status` | ပို့ဆောင်မှုအခြေအနေ | String |


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
// On-Time Delivery % = DIVIDE(COUNTROWS(FILTER(orders,orders[actual_delivery_min]<=orders[estimated_delivery_min])),[Total Orders])*100\n// Avg Delivery Time = AVERAGE(blinkit[actual_delivery_min])
```

---

## 📊 Dashboard Visuals & Tools

Waterfall, Matrix, KPI Cards, Line Chart, Map

---

## 💼 Business Problem Solved

### Problem
```
Quick Commerce တွင်: Delivery time SLAs ပျက်နေ — ဘယ် zone က bottleneck လဲ? SKU performance ကိုခြေရာခံရန်မရှိ။ Customer retention metrics ဘယ်လိုရှိလဲ?
```

### Solution
```diff
+ Running Total DAX + Fulfillment Waterfall + SKU×Zone Matrix + Delivery Time Analysis
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
