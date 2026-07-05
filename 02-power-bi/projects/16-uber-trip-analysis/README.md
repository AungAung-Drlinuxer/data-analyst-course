# Uber Trip Analysis 🚕

## Domain: Mobility

---

## 📋 Project Overview

Uber Trip Data ကိုခွဲခြမ်းစိတ်ဖြာပြီး Trip Trends, Surge Pricing, Driver Performance များကို Dashboard ဖြင့်ပြသခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — uber_trips.csv (1200 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `trip_id` | ခရီးစဉ်နံပါတ် | Integer |
| `pickup_datetime` | စတင်ချိန် | DateTime |
| `pickup_zone` | စတင်ရာဇုန် | String |
| `dropoff_zone` | ဆင်းရာဇုန် | String |
| `passenger_count` | ခရီးသည်ဦးရေ | Integer |
| `trip_distance_miles` | အကွာအဝေး | Float |
| `fare_amount` | ခရီးစရိတ် ($) | Float |
| `tip_amount` | ဆုကြေး ($) | Float |
| `total_amount` | စုစုပေါင်း ($) | Float |
| `surge_multiplier` | Surge မြှောက်ဖော်ကိန်း | Float |


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
// Total Trips = COUNTROWS(uber_trips)\n// Avg Fare = AVERAGE(uber_trips[fare_amount])\n// Avg Tip % = DIVIDE(AVERAGE(uber_trips[tip_amount]),AVERAGE(uber_trips[fare_amount]))*100
```

---

## 📊 Dashboard Visuals & Tools

Map, Scatter, Line Chart, Heatmap, Slicers

---

## 💼 Business Problem Solved

### Problem
```
Ride-hailing company အတွက်: ဘယ်နေရာက demand အများဆုံးလဲ? Surge pricing က revenue ကိုဘယ်လောက်တိုးလဲ? Driver allocation ကို optimize လုပ်ရန်။
```

### Solution
```diff
+ Map for Pickup Hotspots + Hourly Demand Patterns + Fare vs Distance Scatter + Surge Impact Analysis
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
