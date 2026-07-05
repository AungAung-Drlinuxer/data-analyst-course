# Amazon Sales Dashboard — လက်တွေ့ခွဲခြမ်းစိတ်ဖြာခြင်း 🛒

## 1. Data Overview
- **Total Orders:** 1,000 | **Returns:** 150
- **Categories:** Electronics, Clothing, Home, Books, Sports
- **Time Period:** 12 months

## 2. Key Analysis Dimensions

### Sales Performance
- Electronics: 35% of total revenue (highest)
- Books: 8% of revenue but 40% profit margin (most profitable category)
- Clothing: "Kids" sub-category has 22% return rate (quality issue?)

### Return Analysis
```
Return Rate by Category:
  Electronics: 12% (mostly "Defective")
  Clothing: 18% (mostly "Wrong Size/Wrong Item")
  Home: 8% (mostly "Quality Issue")
```
→ Action: Improve product descriptions for clothing sizes

### Fulfillment Performance
- FBA: Avg 3.5 days delivery, 98% on-time
- FBM: Avg 5.2 days delivery, 85% on-time
- Easy Ship: Avg 4.1 days, 91% on-time
→ Recommendation: Convert top 20% FBM products to FBA

## 3. DAX Analysis
```dax
// FBA vs FBM Profitability
FBA Profit = 
CALCULATE([Total Profit], amazon_sales[fulfillment] = "FBA")

// Return Rate with Dynamic Threshold
High Return Products = 
CALCULATE(
    COUNTROWS(amazon_sales),
    FILTER(amazon_sales, [Return Rate %] > 15),
    ALLEXCEPT(amazon_sales, amazon_sales[category])
)
```

## 4. Actionable Insights
- Discount > 20% does NOT significantly increase sales volume (diminishing returns)
- Amazon Pay users have 15% higher AOV than COD users
- "West" region has 40% of returns — investigate logistics partner
