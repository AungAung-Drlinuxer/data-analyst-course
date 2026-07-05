# Bank Loan Analysis — လက်တွေ့ခွဲခြမ်းစိတ်ဖြာခြင်း 📊

## 1. Data Overview
- **Total Records:** 500 loan applications
- **Time Period:** 2 years
- **Key Metrics:** Approval Rate, NPA %, Avg Interest Rate

## 2. Exploratory Data Analysis (Power Query)

### Data Quality Check
```powerquery
// Check null values
Table.TransformColumnTypes(Source, {each {_, type text}})
// Remove duplicates
Table.Distinct(Source, {"loan_id"})
```

### Key Findings from Raw Data
- Credit Score Range: 300-850 (Mean: ~620)
- Loan Amount: $5,000 - $500,000 (Mean: ~$150,000)
- Most common purpose: "Home" (32%), "Auto" (25%)
- Default segments: Self-Employed (40%), Region "Central" (35%)

## 3. DAX Analysis Walkthrough

### Approval Rate by Credit Score Bucket
```dax
Approval by Risk = 
CALCULATE(
    [Approval Rate %],
    ALLEXCEPT(bank_loans, bank_loans[Risk Category])
)
```
→ Low Risk: 95% approved | High Risk: only 35% approved

### NPA Heatmap
- Region x Loan Type Matrix shows: "Central + Business" = highest NPA (22%)
- Recommendation: Tighten business loan criteria in Central region

## 4. Business Insights Generated

| Question | Answer | Action |
|----------|--------|--------|
| What drives rejection? | Low credit score + High DTI > 40% | Automated pre-screening system |
| Which region is riskiest? | Central (NPA 18%) | Regional credit policy adjustment |
| Best performing loan type? | Mortgage (99% approval) | Cross-sell to existing customers |
| Seasonal pattern? | Q4 loan applications spike 40% | Pre-approve in Q3 for faster Q4 processing |

## 5. PowerBI Dashboard Export Notes
- KPIs auto-refresh when connected to live database
- Slicers: Region, Loan Type, Status
- Drill-through: Region → Branch → Loan Officer
