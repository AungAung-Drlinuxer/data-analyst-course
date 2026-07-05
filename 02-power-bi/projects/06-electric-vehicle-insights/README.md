# Electric Vehicle Insights 🔋

## Domain: EV/Manufacturing

---

## 📋 Project Overview

EV Market Data ကိုခွဲခြမ်းစိတ်ဖြာပြီး Market Share, Charging Infrastructure, Battery Trends များကို Dashboard ဖြင့်ပြသခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — ev_population.csv (750 rows) + charging_stations.csv (200 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `ev_id` | EV မှတ်တမ်းနံပါတ် | Integer |
| `make` | ထုတ်လုပ်သူ | String |
| `model` | မော်ဒယ် | String |
| `model_year` | ထုတ်လုပ်သည့်နှစ် | Integer |
| `electric_type` | လျှပ်စစ်အမျိုးအစား | String |
| `range_miles` | မောင်းနှင်နိုင်မှုအကွာအဝေး | Integer |
| `base_price` | စျေးနှုန်း ($) | Float |
| `battery_kwh` | ဘက်ထရီပမာဏ | Float |


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
// Total EVs = COUNTROWS(ev_population)\n// Avg Range = AVERAGE(ev_population[range_miles])\n// BEV % = DIVIDE(COUNTROWS(FILTER(evs, evs[electric_type]="BEV")),[Total EVs])*100\n// Adoption Rate = [Total EVs] / [Total Population]
```

---

## 📊 Dashboard Visuals & Tools

Bubble Map, Scatter, AI Key Influencers, Donut, Slicers

---

## 💼 Business Problem Solved

### Problem
```
EV market ကို analyze လုပ်ရန်: ဘယ်ပြည်နယ်က adoption အများဆုံးလဲ? Charging infrastructure က လုံလောက်ရဲ့လား? Range vs Price best value ကိုရှာရန်။
```

### Solution
```diff
+ Bubble Map for EV Density + Scatter for Range vs Price + AI Key Influencers for Adoption Factors + Charging Station Analysis
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
