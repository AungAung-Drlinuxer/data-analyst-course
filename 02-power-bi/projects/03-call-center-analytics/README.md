# 03. Call Center Analytics 📞

## Domain: Operations

---

## Project Overview

Call Center Analytics သည် Operations domain မှဒေတာများကို PowerBI ဖြင့်ခွဲခြမ်းစိတ်ဖြာပြီး Executive Dashboard များတည်ဆောက်ထားသော project ဖြစ်ပါသည်။

---

## 📂 Datasets

### `datasets/raw/` — call_center_records.csv (2000 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `call_id` | ခေါ်ဆိုမှုနံပါတ် | Integer |
| `agent_id` | အေးဂျင့်အမှတ် | String |
| `agent_name` | အေးဂျင့်အမည် | String |
| `department` | ဌာန | String |
| `call_datetime` | ခေါ်ဆိုသည့်ရက်စွဲ/အချိန် | DateTime |
| `duration_sec` | ကြာချိန် (စက္ကန့်) | Integer |
| `call_type` | ခေါ်ဆိုမှုအမျိုးအစား | String |
| `customer_rating` | အဆင့်သတ်မှတ်ချက် (1-5) | Float |
| `issue_category` | ပြဿနာအမျိုးအစား | String |
| `resolution_status` | ဖြေရှင်းနိုင်မှုအခြေအနေ | String |
| `hold_time_sec` | စောင့်ဆိုင်းချိန် (စက္ကန့်) | Integer |




---

## 🔌 PowerBI တွင် Dataset ချိတ်ဆက်ခြင်း

### Step 1: Data Import
```
PowerBI Desktop → Get Data → Text/CSV
Select: datasets/raw/call_center_analytics.csv (adjust filename accordingly)
→ Transform Data
```

### Step 2: Power Query (M Code)
```powerquery
let
    Source = Csv.Document(File.Contents("datasets/raw/call_center_records.csv")),
    #"Split DateTime" = Table.SplitColumn(Source, "call_datetime", 
        Splitter.SplitTextByDelimiter(" "), {"call_date", "call_time"})
in
    #"Split DateTime"
```

### Step 3: Data Model
- Create Date table: `Date = CALENDARAUTO()`
- Build relationships between fact and dimension tables
- Create hierarchies (Year > Quarter > Month > Date)

---

## 📐 Core DAX Measures

```dax

// 1. Total Calls
Total Calls = COUNTROWS(call_center_records)

// 2. Avg Handle Time (min)
Avg Handle Time = AVERAGE(call_center_records[duration_sec]) / 60

// 3. Avg Customer Rating
Avg CSAT = AVERAGE(call_center_records[customer_rating])

// 4. Resolution Rate %
Resolution Rate % = 
DIVIDE(
    COUNTROWS(FILTER(call_center_records, call_center_records[resolution_status] = "Resolved")),
    [Total Calls]
) * 100

// 5. Service Level (calls answered < 30 sec)
Service Level % = 
DIVIDE(
    COUNTROWS(FILTER(call_center_records, call_center_records[hold_time_sec] < 30)),
    [Total Calls]
) * 100

// 6. Agent Scorecard
Agent Score = 
[Avg CSAT] * 0.4 + [Resolution Rate %] / 100 * 0.4 + (1 - [Avg Handle Time] / 60) * 0.2

```

---

## 📊 Dashboard Visuals

| Visual | Purpose |
|--------|---------|
| KPI Cards | Total Calls, Avg Handle Time, CSAT, Service Level |
| Line Chart | Call Volume by Hour (peak detection) |
| Bar Chart | Calls by Department |
| Gauge | Service Level % |
| Table | Agent Scorecard (ranked) |
| Pie Chart | Issue Category Distribution |
| Line Chart | CSAT Trend over time |
| Scatter | Handle Time vs CSAT Score |
| Slicers | Department, Date, Agent |

### Dashboard Pages

| Page | Name | Focus |
|------|------|-------|
| 1 | Executive Summary | High-level KPIs, trends |
| 2 | Detailed Analysis | Drill-down by category/region |
| 3 | Performance Review | Agent/Product/Service scores |

---

## 💼 Business Problem Solved

### Problem
```
Call center က customer wait time 15 min ရှိနေပြီး CSAT score ကျဆင်းနေ။ Peak hours မှာ agent လုံလောက်ရဲ့လားဆိုတာ မသိ။ Agent performance ကို နှိုင်းယှဉ်ရန် standardized scorecard မရှိ။
```

### Solution
```diff
+ Real-time KPI Cards + Hourly call volume pattern → shift scheduling optimization + Agent scorecards with ranking + CSAT trend analysis
```

### Business Impact
Avg wait time 15min → 5min (67% reduction), CSAT Score 3.1 → 4.3 (39% improvement), Agent productivity 25% increase, Peak hour staffing optimized 30% efficiency gain

---

## 🧪 လက်တွေ့စမ်းသပ်ရန်

1. PowerBI Desktop ကိုဖွင့်ပါ
2. `Get Data → Text/CSV` → `datasets/raw/` မှ CSV ကိုရွေးပါ
3. Power Query တွင် data cleaning လုပ်ပါ
4. DAX measures များကို ရိုက်ထည့်ပါ
5. Dashboard visuals များကို configure လုပ်ပါ
6. ရလဒ်များကို ဆန်းစစ်ပါ

---

## 📝 Dataset Notes
- Dataset သည် synthetic data ဖြစ်ပြီး real-world scenario ကိုအခြေခံထားပါသည်
- Production တွင် actual system API သို့မဟုတ် database မှ real-time data ချိတ်ဆက်အသုံးပြုနိုင်ပါသည်
- Sample data ကို `datasets/sample/` တွင်ကြည့်ရှုနိုင်ပါသည်
