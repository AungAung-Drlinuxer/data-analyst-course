# Road Accident Report 🚦

## Domain: Transport & Safety

---

## 📋 Project Overview

Road Accident Data ကိုခွဲခြမ်းစိတ်ဖြာပြီး Accident Hotspots, Severity Analysis, Time Patterns များကို Dashboard ဖြင့်ပြသခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — road_accidents.csv (1000 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `accident_id` | မတော်တဆမှုနံပါတ် | Integer |
| `accident_date` | ရက်စွဲ | Date |
| `weather_condition` | ရာသီဥတု | String |
| `road_type` | လမ်းအမျိုးအစား | String |
| `speed_limit` | မြန်နှုန်းကန့်သတ်ချက် | Integer |
| `severity` | ပြင်းထန်မှု | String |
| `number_of_casualties` | ဒဏ်ရာရသူဦးရေ | Integer |
| `accident_reason` | မတော်တဆရခြင်းအကြောင်းရင်း | String |


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
// Total Accidents = COUNTROWS(road_accidents)\n// Fatal % = DIVIDE([Fatal Count],[Total Accidents])*100\n// Avg Casualties = AVERAGE(road_accidents[number_of_casualties])
```

---

## 📊 Dashboard Visuals & Tools

Heatmap, Pie, Donut, Line Chart, Slicers

---

## 💼 Business Problem Solved

### Problem
```
လမ်းအန္တရာယ်ကင်းရှင်းရေးအတွက်: ဘယ်နေရာတွေက accident hotspots လဲ? ဘယ်အချက်တွေက severity ကိုသက်ရောက်လဲ? ဘယ်အချိန်က accident အများဆုံးလဲ?
```

### Solution
```diff
+ Heatmap for High-Risk Locations + Severity Distribution + Time Pattern Analysis + Weather/Road Impact
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
