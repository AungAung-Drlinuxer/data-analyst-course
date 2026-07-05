# Adidas Sales Performance 👟

## Domain: Retail

---

## 📋 Project Overview

Adidas US Sales ဒေတာကို ခွဲခြမ်းစိတ်ဖြာပြီး product category, region, sales channel အလိုက် performance ကို dashboard ဖြင့်ပြသခြင်း။ Online vs Retail store channel comparison, What-If discount simulation တို့ပါဝင်သည်။

---

## 📂 Datasets

### `datasets/raw/` — adidas_sales.csv (1500 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `sale_id` | ရောင်းအားနံပါတ် | Integer |
| `date` | ရက်စွဲ | Date |
| `product_sku` | ပစ္စည်းကုဒ် | String |
| `product_name` | ပစ္စည်းအမည် | String |
| `category` | အမျိုးအစား | String |
| `gender` | ကျား/မ | String |
| `region` | ဒေသ | String |
| `state` | ပြည်နယ် | String |
| `retailer` | လက်လီအရောင်းဆိုင် | String |
| `sales_channel` | အရောင်းလမ်းကြောင်း | String |
| `units_sold` | အရေအတွက် | Integer |
| `unit_price` | တစ်ခုချင်းစျေး ($) | Float |
| `total_sales` | စုစုပေါင်းရောင်းရငွေ ($) | Float |
| `operating_profit` | အမြတ်ငွေ ($) | Float |
| `margin_pct` | အမြတ်နှုန်း (%) | Float |


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
// Total Sales = SUM(adidas_sales[total_sales])\n// Total Profit = SUM(adidas_sales[operating_profit])\n// Margin % = DIVIDE([Total Profit],[Total Sales])*100\n// Discount Simulation = [Total Sales] * (1 - Parameter[Discount Value])
```

---

## 📊 Dashboard Visuals & Tools

Map Visual, Waterfall Chart, What-If Parameter, Slicers

---

## 💼 Business Problem Solved

### Problem
```
Adidas အရောင်းဆိုင်ခွဲများတွင်: Discount strategy က profit ကိုဘယ်လိုသက်ရောက်လဲဆိုတာမသိ။ Online vs Retail channel performance ကိုနှိုင်းယှဉ်ရန်မရှိ။ ဘယ် region က underperforming လဲဆိုတာ visibility မရှိ။
```

### Solution
```diff
+ What-If Parameter for Discount Simulation + Map for Regional Performance + Waterfall for Profit Variance + Channel Comparison Dashboard
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
