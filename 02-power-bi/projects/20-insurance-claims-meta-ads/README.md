# Insurance Risk & Claims Analytics + Meta Ads 🛡️

## Domain: Insurance & Digital Marketing

---

## 📋 Project Overview

Insurance Claims Data နှင့် Meta Ads Data ကိုပေါင်းစပ်ခွဲခြမ်းစိတ်ဖြာပြီး Risk Assessment, Claims Analytics, Ad Performance ROI များကို Dashboard ဖြင့်ပြသခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — insurance_claims.csv (600 rows) + meta_ads_performance.csv (200 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `claim_id` | တောင်းခံမှုနံပါတ် | Integer |
| `policy_type` | မူဝါဒအမျိုးအစား | String |
| `incident_type` | ဖြစ်စဉ်အမျိုးအစား | String |
| `incident_severity` | ပြင်းထန်မှု | String |
| `claimed_amount` | တောင်းခံငွေ ($) | Float |
| `approved_amount` | အတည်ပြုငွေ ($) | Float |
| `claim_status` | တောင်းခံမှုအခြေအနေ | String |
| `fraud_flag` | မသမာမှုအလံ | String |


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
// Avg Claim = AVERAGE(insurance[claimed_amount])\n// Approval Rate = DIVIDE(SUM(insurance[approved_amount]),SUM(insurance[claimed_amount]))*100\n// Fraud Rate = DIVIDE([Fraud Count],[Total Claims])*100\n// ROAS = DIVIDE(SUM(meta[conversions]),SUM(meta[spend]))
```

---

## 📊 Dashboard Visuals & Tools

Map, Funnel, AI Anomaly Detection, Scatter, KPIs

---

## 💼 Business Problem Solved

### Problem
```
အာမခံကုမ္ပဏီတွင်: Claims fraud နှင့် marketing spend waste နှစ်ခုလုံးကိုခံစားနေရ။ ဒေတာတွေက separate systems မှာရှိနေ။ Meta Ads ROI ကိုခြေရာခံရန်ခက်ခဲ။
```

### Solution
```diff
+ Composite Model (Import + DirectQuery) + AI Anomaly Detection for Fraud + Meta Ad Funnel + Risk Scorecard
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
