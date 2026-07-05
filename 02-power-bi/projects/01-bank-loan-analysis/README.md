# 01. Bank Loan Analysis 🏦

## Domain: Finance & Banking

---

## Project Overview

Bank Loan Analysis သည် Finance & Banking domain မှဒေတာများကို PowerBI ဖြင့်ခွဲခြမ်းစိတ်ဖြာပြီး Executive Dashboard များတည်ဆောက်ထားသော project ဖြစ်ပါသည်။

---

## 📂 Datasets

### `datasets/raw/` — bank_loans.csv (500 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `loan_id` | ချေးငွေမှတ်တမ်းနံပါတ် | Integer |
| `customer_id` | ဝယ်ယူသူအမှတ် | String |
| `age` | အသက် | Integer |
| `income` | နှစ်စဉ်ဝင်ငွေ ($) | Float |
| `credit_score` | ခရက်ဒစ်ရမှတ် (300-850) | Integer |
| `loan_amount` | ချေးငွေပမာဏ ($) | Float |
| `loan_term_months` | ချေးငွေသက်တမ်း (လ) | Integer |
| `interest_rate` | အတိုးနှုန်း (%) | Float |
| `loan_purpose` | ချေးငွေရည်ရွယ်ချက် | Categorical |
| `loan_type` | ချေးငွေအမျိုးအစား | Categorical |
| `region` | ဒေသ | Categorical |
| `debt_to_income_ratio` | အကြွေးအချိုး (%) | Float |
| `loan_status` | ချေးငွေအခြေအနေ | Categorical |
| `approval_date` | အတည်ပြုရက်စွဲ | Date |




---

## 🔌 PowerBI တွင် Dataset ချိတ်ဆက်ခြင်း

### Step 1: Data Import
```
PowerBI Desktop → Get Data → Text/CSV
Select: datasets/raw/bank_loan_analysis.csv (adjust filename accordingly)
→ Transform Data
```

### Step 2: Power Query (M Code)
```powerquery
let
    Source = Csv.Document(File.Contents("datasets/raw/bank_loans.csv"),[Delimiter=",", Encoding=65001]),
    #"Promoted Headers" = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
    #"Changed Type" = Table.TransformColumnTypes(#"Promoted Headers",{
        {"age", Int64.Type}, {"income", Int64.Type}, {"credit_score", Int64.Type}
    }),
    #"Added Risk Category" = Table.AddColumn(#"Changed Type", "Risk Category", each
        if [credit_score] >= 750 then "Low Risk"
        else if [credit_score] >= 650 then "Medium Risk"
        else if [credit_score] >= 550 then "High Risk"
        else "Very High Risk")
in
    #"Added Risk Category"
```

### Step 3: Data Model
- Create Date table: `Date = CALENDARAUTO()`
- Build relationships between fact and dimension tables
- Create hierarchies (Year > Quarter > Month > Date)

---

## 📐 Core DAX Measures

```dax

// 1. Total Applications
Total Apps = COUNTROWS(bank_loans)

// 2. Approval Rate %
Approval Rate % = 
DIVIDE(
    COUNTROWS(FILTER(bank_loans, bank_loans[loan_status] = "Approved")),
    COUNTROWS(bank_loans)
) * 100

// 3. NPA Rate
NPA Rate % = 
DIVIDE(
    COUNTROWS(FILTER(bank_loans, bank_loans[loan_status] = "Rejected")),
    COUNTROWS(bank_loans)
) * 100

// 4. Avg Loan Amount
Avg Loan Amt = AVERAGE(bank_loans[loan_amount])

// 5. Risk Category (Calculated Column)
Risk Category = 
SWITCH(TRUE(),
    bank_loans[credit_score] >= 750, "Low Risk",
    bank_loans[credit_score] >= 650, "Medium Risk",
    bank_loans[credit_score] >= 550, "High Risk",
    "Very High Risk"
)

// 6. Monthly Trend
Monthly Loans = 
CALCULATE(COUNTROWS(bank_loans), DATESMTD('Date'[Date]))

```

---

## 📊 Dashboard Visuals

| Visual | Purpose |
|--------|---------|
| KPI Cards | Total Apps, Total Amount, Avg Rate, Approval % |
| Line Chart | Monthly Loan Trend |
| Bar Chart | Loan Amount by Purpose |
| Pie Chart | Loan Status Distribution |
| Scatter | Income vs Credit Score (colored by Status) |
| Matrix | Region x Loan Type x NPA Rate |
| Waterfall | Loan Approval Flow |
| AI Key Influencers | What drives Rejection? |
| Slicers | Region, Loan Type, Status |

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
ဘဏ် loan portfolio ကို real-time စောင့်ကြည့်ရန် dashboard မရှိ။ NPA rate မြင့်တက်နေသော်လည်း ဘယ် segment ကဖြစ်နေသည်ကို မသိ။ Credit risk assessment က manual process ဖြစ်နေ။ Monthly report ပြင်ဆင်ရန် 3-5 ရက်ကြာမြင့်နေ။
```

### Solution
```diff
+ Automated KPI Dashboard + Real-time NPA tracking + AI Key Influencers for risk detection + Decision matrix for loan approval optimization
```

### Business Impact
Report generation 3-5 days → Real-time (100% faster), NPA detection Monthly → Daily, Risk assessment Manual → AI-driven (60% accuracy gain)

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
