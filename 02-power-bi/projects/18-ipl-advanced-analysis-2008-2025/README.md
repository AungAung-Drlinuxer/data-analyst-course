# IPL Advanced Analysis 2008-2025 📈

## Domain: Big Data Sports

---

## 📋 Project Overview

IPL Data 2008-2025 ကိုအဆင့်မြှင့်တင်ခွဲခြမ်းစိတ်ဖြာပြီး Predictive Insights, Player Value, Team Strategy များကို Dashboard ဖြင့်ပြသခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — ipl_advanced_matches.csv (600 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `match_id` | ပွဲစဉ်နံပါတ် | Integer |
| `season` | ရာသီ | Integer |
| `team1` | အသင်း ၁ | String |
| `team2` | အသင်း ၂ | String |
| `innings1_runs` | ပထမ Innings ရမှတ် | Integer |
| `innings2_runs` | ဒုတိယ Innings ရမှတ် | Integer |
| `winner` | အနိုင်ရအသင်း | String |
| `player_of_match` | ပွဲစဉ်လူစွမ်းကောင်း | String |
| `top_scorer` | အမှတ်အများဆုံး | String |
| `best_bowler` | အကောင်းဆုံးဘိုးလာ | String |
| `total_fours` | စုစုပေါင်း လေးချက် | Integer |
| `total_sixes` | စုစုပေါင်း ခြောက်ချက် | Integer |


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
// 4s per Match = AVERAGE(ipl_advanced[total_fours])\n// 6s per Match = AVERAGE(ipl_advanced[total_sixes])\n// Win Margin Avg = AVERAGE(ipl_advanced[win_margin_runs])
```

---

## 📊 Dashboard Visuals & Tools

Custom Visuals, Python Visual, Scatter, Time Series, Parameters

---

## 💼 Business Problem Solved

### Problem
```
IPL franchise auction အတွက်: Player တစ်ယောက်ရဲ့ true value ကဘယ်လောက်လဲ? Toss decision က match outcome ကိုသက်ရောက်လား? 17 seasons trend ကဘယ်လိုရှိလဲ?
```

### Solution
```diff
+ Advanced DAX Time Intelligence + AutoML Prediction + Auction Value Analysis + Toss Decision Impact
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
