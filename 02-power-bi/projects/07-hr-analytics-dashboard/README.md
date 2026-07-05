# HR Analytics Dashboard 👥

## Domain: Human Resources

---

## 📋 Project Overview

Employee Data ကိုခွဲခြမ်းစိတ်ဖြာပြီး Attrition, Diversity, Performance, Headcount များကို Dashboard ဖြင့်ပြသခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — hr_employee_attrition.csv (1500 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `employee_id` | ဝန်ထမ်းနံပါတ် | Integer |
| `age` | အသက် | Integer |
| `gender` | ကျား/မ | String |
| `department` | ဌာန | String |
| `job_role` | ရာထူး | String |
| `education` | ပညာအရည်အချင်း | String |
| `environment_satisfaction` | ပတ်ဝန်းကျင်ကျေနပ်မှု | Integer |
| `job_satisfaction` | အလုပ်ကျေနပ်မှု | Integer |
| `work_life_balance` | လုပ်ငန်းခွင်ဘဝဟန်ချက် | Integer |
| `performance_rating` | စွမ်းဆောင်ရည်အဆင့် | Integer |
| `overtime` | အချိန်ပို | String |
| `years_at_company` | လုပ်သက် | Integer |
| `monthly_income` | လစာ ($) | Float |
| `attrition` | ထွက်ခွာမှု | String |


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
// Attrition Rate = DIVIDE([Attrition Count],[Total Employees])*100\n// Avg Tenure = AVERAGE(hr[years_at_company])\n// Overtime Impact = CALCULATE([Attrition Rate], hr[overtime]="Yes")
```

---

## 📊 Dashboard Visuals & Tools

AI Key Influencers, Decomposition Tree, KPI Cards, Matrix, Slicers + RLS

---

## 💼 Business Problem Solved

### Problem
```
Company တွင်: Quarterly attrition rate 25% — ဘယ်ဌာနကအဆိုးဆုံးလဲ? ဘာကြောင့်ထွက်သွားတာလဲ? Overtime policy က retention ကိုသက်ရောက်လား?
```

### Solution
```diff
+ AI Key Influencers for Attrition + Decomposition Tree + RLS for Department Managers + Diversity Scorecard
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
