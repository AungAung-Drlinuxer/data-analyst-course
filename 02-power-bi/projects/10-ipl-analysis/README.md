# IPL Analysis 🏏

## Domain: Sports Analytics

---

## 📋 Project Overview

IPL Cricket Data 2008-2024 ကိုခွဲခြမ်းစိတ်ဖြာပြီး Team Performance, Player Stats, Match History များကို Dashboard ဖြင့်ပြသခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — ipl_matches.csv (500 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `match_id` | ပွဲစဉ်နံပါတ် | Integer |
| `season` | ရာသီ | Integer |
| `date` | ရက်စွဲ | Date |
| `venue` | ကစားကွင်း | String |
| `team1` | အသင်း ၁ | String |
| `team2` | အသင်း ၂ | String |
| `toss_winner` | မဲနိုင်သောအသင်း | String |
| `toss_decision` | မဲဆုံးဖြတ်ချက် | String |
| `winner` | အနိုင်ရအသင်း | String |
| `player_of_match` | ပွဲစဉ်လူစွမ်းကောင်း | String |


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
// Total Matches = COUNTROWS(ipl_matches)\n// Win % = DIVIDE(COUNTROWS(FILTER(ipl,ipl[winner]=SELECTEDVALUE(teams))),[Total Matches])*100\n// Toss Impact = DIVIDE(COUNTROWS(FILTER(ipl,ipl[toss_winner]=ipl[winner])),[Total Matches])*100
```

---

## 📊 Dashboard Visuals & Tools

Parameter, Drill-through, Bar Chart, Map, Matrix, Slicers

---

## 💼 Business Problem Solved

### Problem
```
IPL franchise အတွက်: ဘယ် player က current form ရှိလဲ? Home ground advantage ရှိရဲ့လား? Toss decision က win ကိုသက်ရောက်လား?
```

### Solution
```diff
+ Parameter for Season Selection + Drill-through: Season→Match + Venue Analysis + Player Performance Trends
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
