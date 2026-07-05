# Call Center Analytics — လက်တွေ့ခွဲခြမ်းစိတ်ဖြာခြင်း 📞

## 1. Data Overview
- **Total Calls:** 2,000 | **Agents:** 50 | **Duration:** 30-3600 sec
- **Departments:** Billing, Tech Support, Sales, Account Mgmt, General

## 2. Performance Analysis

### Service Level (Calls answered within 30 seconds)
- Current: 62% (Target: 80%)
- Peak hours: 10-11 AM, 2-3 PM (avg hold time > 5 min)
- Slow hours: 12-1 PM, after 6 PM

### Agent Scorecard (Top 5)
| Rank | Agent | CSAT | Resolution Rate | Avg Handle Time |
|------|-------|------|----------------|----------------|
| 1 | Top Agent | 4.8 | 96% | 4.2 min |
| 5 | Fifth | 4.2 | 88% | 5.8 min |

### Issue Category Breakdown
```
Technical Support: 35% (highest volume, CSAT 3.9)
Billing: 25% (CSAT 3.5 — needs improvement)
Sales: 20% (CSAT 4.5 — best)
Account Mgmt: 12% (CSAT 4.0)
General: 8% (CSAT 4.2)
```

## 3. DAX-Driven Insights
```dax
// Busiest Hour Detection
Peak Hour Score = 
RANKX(ALL('Hour'[Hour]), [Total Calls], , DESC)

// Agent Ranking Composite
Agent Composite Score = 
[Avg CSAT] * 0.3 + [Resolution Rate %] * 0.4 + (1 - [Avg Handle Time] / MAX([Avg Handle Time])) * 0.3
```

## 4. Recommendations
1. Shift optimization: +2 agents during 10-11 AM, -1 agent after 6 PM
2. Billing team training: Target CSAT improvement from 3.5 to 4.0
3. Technical support: Self-service knowledge base implementation
