# Ecommerce Supply Chain 📦

## Domain: Supply Chain

---

## 📋 Project Overview

E-commerce supply chain data ကိုခွဲခြမ်းစိတ်ဖြာပြီး Order Fulfillment, Shipping, Returns များကို Dashboard ဖြင့်ပြသခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — ecommerce_orders.csv (1200 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `order_id` | မှာယူမှုနံပါတ် | Integer |
| `order_date` | ရက်စွဲ | Date |
| `product_category` | ပစ္စည်းအမျိုးအစား | String |
| `warehouse_zone` | ဂိုဒေါင်ဇုန် | String |
| `order_qty` | အရေအတွက် | Integer |
| `unit_cost` | ကုန်ကျစရိတ် ($) | Float |
| `unit_price` | ရောင်းစျေး ($) | Float |
| `total_revenue` | စုစုပေါင်းဝင်ငွေ ($) | Float |
| `order_status` | မှာယူမှုအခြေအနေ | String |
| `fulfillment_days` | ဖြည့်ဆည်းရက်ကြာ | Integer |
| `return_status` | ပြန်အမ်းမှု | String |


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
// Fulfillment Rate = DIVIDE(COUNTROWS(FILTER(orders,orders[fulfillment_days]<=3)),[Total Orders])*100\n// Return Rate = DIVIDE([Total Returns],[Total Orders])*100\n// Avg Fulfillment Days = AVERAGE(ecommerce[fulfillment_days])
```

---

## 📊 Dashboard Visuals & Tools

Funnel, Map, Waterfall, KPI Cards, Slicers

---

## 💼 Business Problem Solved

### Problem
```
E-commerce ကုမ္ပဏီတွင်: Order fulfillment time တက်နေပြီး return rate များနေ။ ဘယ် warehouse က bottleneck လဲ? Carrier performance ကိုနှိုင်းယှဉ်ရန်မရှိ။
```

### Solution
```diff
+ Funnel Chart for Order Process + Map for Shipping Routes + Warehouse Performance + Return Analysis
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
