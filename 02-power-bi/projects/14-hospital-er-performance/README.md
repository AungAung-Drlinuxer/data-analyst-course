# Hospital ER Performance 🏥

## Domain: Healthcare

---

## 📋 Project Overview

Hospital ER Data ကိုခွဲခြမ်းစိတ်ဖြာပြီး Wait Time, Patient Flow, ER Utilization များကို Dashboard ဖြင့်ပြသခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — er_patient_records.csv (1500 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `patient_id` | လူနာနံပါတ် | String |
| `arrival_datetime` | ရောက်ရှိချိန် | DateTime |
| `age` | အသက် | Integer |
| `gender` | ကျား/မ | String |
| `severity` | အရေးပေါ်အဆင့် | String |
| `chief_complaint` | အဓိကပြဿနာ | String |
| `department_referred` | လွှဲပြောင်းရာဌာန | String |
| `wait_time_min` | စောင့်ဆိုင်းချိန် | Integer |
| `treatment_time_min` | ကုသချိန် | Integer |
| `total_time_min` | စုစုပေါင်းအချိန် | Integer |


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
// Avg Wait Time = AVERAGE(er[wait_time_min])\n// Target Met % = DIVIDE(COUNTROWS(FILTER(er, er[wait_time_min]<=30)), [Total Visits])*100\n// Peak Hour = TOPN(1, VALUES(er[arrival_hour]), [Total Visits])
```

---

## 📊 Dashboard Visuals & Tools

Gauge, Line Chart, Drill-through, KPI Cards, Heatmap

---

## 💼 Business Problem Solved

### Problem
```
ER ဆောင်တွင်: Wait time 2+ hours — patient satisfaction ကျဆင်း။ ဘယ်အချိန်က peak လဲ? Resource လုံလောက်ရဲ့လား?
```

### Solution
```diff
+ Gauge for Wait Time Targets + Hourly Arrival Pattern + Drill-through: ER→Department + Resource Utilization
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
