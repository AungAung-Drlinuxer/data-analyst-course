# Insurance + Meta Ads 🛡️ — လက်တွေ့ခွဲခြမ်းစိတ်ဖြာခြင်း

## 1. Data Overview
- **Source:** `datasets/raw/` — Synthetic dataset (production-style)
- **Sample:** `datasets/sample/` — First 20 rows preview

## 2. Key Analysis Dimensions

Fraud detection patterns, Claims severity analysis, Ad ROAS, Risk assessment scoring

## 3. DAX Analysis Patterns Used

```dax
// KPIs
Total Records = COUNTROWS('table')
Avg Value = AVERAGE('table'[value])
YoY Growth = 
VAR ThisYear = [Total Sales]
VAR LastYear = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date]))
RETURN DIVIDE(ThisYear - LastYear, LastYear)

// Ranking
Top N Rank = RANKX(ALL('table'[category]), [Total], , DESC)

// Dynamic Segmentation
Segment = 
SWITCH(TRUE(),
    'table'[value] >= 0.8, "High",
    'table'[value] >= 0.5, "Medium",
    "Low"
)
```

## 4. Business Insights & Recommendations

| Question | Data Analysis | Recommendation |
|----------|--------------|---------------|
| Key driver identification | Use Key Influencers visual | Focus on top 3 drivers |
| Anomaly detection | Scatter plot + outliers | Investigate flagged items |
| Trend analysis | Time series line chart | Seasonal adjustment |
| Performance benchmark | Matrix with conditional formatting | Set dynamic targets |

## 5. Dashboard Navigation
1. **Page 1 — Executive Summary:** High-level KPIs, trends, alerts
2. **Page 2 — Detailed Breakdown:** Drill-down by dimensions
3. **Page 3 — Action Items:** Flagged items, recommendations

## 6. Next Steps for Production
- Replace synthetic data with live database connection
- Set up scheduled refresh in PowerBI Service
- Add Row-Level Security (RLS) for data governance
- Create mobile-optimized view for executives
