# India Elections Results 🗳️

## Domain: Political Data Analytics

---

## 📋 Project Overview

India Election Results Data ကိုခွဲခြမ်းစိတ်ဖြာပြီး Constituency Map, Party Performance, Voting Trends များကို Dashboard ဖြင့်ပြသခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — election_results.csv (500 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `constituency_name` | မဲဆန္ဒနယ်အမည် | String |
| `state` | ပြည်နယ် | String |
| `total_voters` | မဲဆန္ဒရှင်စုစုပေါင်း | Integer |
| `party` | ပါတီ | String |
| `candidate` | ကိုယ်စားလှယ်လောင်း | String |
| `votes` | မဲအရေအတွက် | Integer |
| `vote_share_pct` | မဲရာခိုင်နှုန်း | Float |
| `election_year` | ရွေးကောက်ပွဲနှစ် | Integer |
| `result_type` | ရလဒ် | String |


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
// Total Seats = COUNTROWS(FILTER(election, election[result_type]="Won"))\n// Vote Share % = DIVIDE(SUM(election[votes]), SUM(election[valid_votes]))*100\n// Seat Share % = DIVIDE([Total Seats], [Total Constituencies])*100
```

---

## 📊 Dashboard Visuals & Tools

Filled Map, Treemap, Stacked Bar, Parameter, Slicers

---

## 💼 Business Problem Solved

### Problem
```
Election Analysis အတွက်: ဘယ်ပါတီက ဘယ်ပြည်နယ်မှာ အင်အားကောင်းလဲ? Vote share vs seat share discrepancy ရှိလား? Historical comparison လုပ်ရန်။
```

### Solution
```diff
+ Filled Map for Constituencies + Treemap for Party Seats + Parameter for Year Selection + Coalition Analysis
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
