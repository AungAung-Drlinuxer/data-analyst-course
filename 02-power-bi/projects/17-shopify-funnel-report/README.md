# Shopify Funnel Report 🛍️

## Domain: Digital Commerce

---

## 📋 Project Overview

Shopify Store Data ကိုခွဲခြမ်းစိတ်ဖြာပြီး Conversion Funnel, Cart Abandonment, AOV များကို Dashboard ဖြင့်ပြသခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — shopify_funnel.csv (1500 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `session_id` | Session နံပါတ် | Integer |
| `date` | ရက်စွဲ | Date |
| `utm_source` | Traffic အရင်းအမြစ် | String |
| `product_viewed` | ပစ္စည်းကြည့်ရှုမှု | String |
| `added_to_cart` | Cart ထဲထည့်မှု | String |
| `reached_checkout` | Checkout ရောက်မှု | String |
| `purchase_completed` | ဝယ်ယူမှုပြီးဆုံး | String |
| `revenue` | ဝင်ငွေ ($) | Float |
| `device_type` | စက်ပစ္စည်းအမျိုးအစား | String |
| `abandonment_reason` | စွန့်လွှတ်ရခြင်းအကြောင်းရင်း | String |


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
// Conversion Rate = DIVIDE([Purchases],[Sessions])*100\n// AOV = DIVIDE([Total Revenue],[Purchases])\n// Abandonment Rate = DIVIDE([Cart Added]-[Purchases],[Cart Added])*100
```

---

## 📊 Dashboard Visuals & Tools

Funnel, Cohort Table, AI Key Influencers, Bar Chart, Slicers

---

## 💼 Business Problem Solved

### Problem
```
Shopify store တွင်: Cart abandonment rate 70%+ ရှိနေ။ ဘာကြောင့်လဲ? ဘယ် traffic source က quality customers ပေးလဲ?
```

### Solution
```diff
+ Funnel Chart for Conversion + Cohort Analysis + AI Key Influencers for Abandonment + AOV by Source
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
