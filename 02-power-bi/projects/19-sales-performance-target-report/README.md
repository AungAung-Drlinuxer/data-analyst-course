# Sales Performance & Target Report 📊

## Domain: Corporate Analytics

---

## 📋 Project Overview

Sales Target vs Actual Data ကိုခွဲခြမ်းစိတ်ဖြာပြီး Performance, Forecast, Manager Dashboards များတည်ဆောက်ခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — sales_performance.csv (800 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `sale_id` | အရောင်းနံပါတ် | Integer |
| `date` | ရက်စွဲ | Date |
| `sales_rep_name` | အရောင်းကိုယ်စားလှယ် | String |
| `region` | ဒေသ | String |
| `product_category` | ပစ္စည်းအမျိုးအစား | String |
| `deal_value` | သဘောတူညီမှုတန်ဖိုး ($) | Float |
| `target_amount` | ပစ်မှတ်တန်ဖိုး ($) | Float |
| `target_achievement_pct` | ပစ်မှတ်အောင်မြင်မှု (%) | Float |
| `deal_stage` | သဘောတူညီမှုအဆင့် | String |
| `fiscal_quarter` | ဘဏ္ဍာရေးသုံးလပတ် | String |


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
// Achievement % = DIVIDE(SUM(sales[deal_value]), SUM(sales[target_amount]))*100\n// Pipeline Value = CALCULATE(SUM(sales[deal_value]), sales[deal_stage]<>"Closed Won")
```

---

## 📊 Dashboard Visuals & Tools

Gauge, Waterfall, What-If, RLS, Forecast, KPI Cards

---

## 💼 Business Problem Solved

### Problem
```
Corporate sales team: Quarterly target vs actual gap — ဘယ် rep က underperforming လဲ? Forecast accurate ရဲ့လား? Commission structure ကိုဘယ်လိုအကောင်းဆုံးဖြစ်အောင်လုပ်မလဲ?
```

### Solution
```diff
+ Gauge for Target vs Actual + What-If Parameter + Waterfall for Variance + RLS for Managers + Revenue Forecasting
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
