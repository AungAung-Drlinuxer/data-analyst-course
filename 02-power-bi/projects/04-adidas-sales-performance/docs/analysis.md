# Adidas Sales Performance — လက်တွေ့ခွဲခြမ်းစိတ်ဖြာခြင်း 👟

## 1. Data Overview
- **Sales Records:** 1,500 | **Products:** 24 models | **Retailers:** 8
- **Regions:** 5 US regions | **Channels:** Online, Retail, Outlet

## 2. Channel Analysis
- Online: 42% of revenue, 48% margin (best channel)
- Retail: 40% of revenue, 42% margin
- Outlet: 18% of revenue, 35% margin (clearance/discount)

## 3. Product Analysis
```
Top 3 Products by Revenue:
1. Ultraboost (Men) - $285K - 18% of total
2. NMD (Men) - $210K - 13% of total
3. Stan Smith (Unisex) - $195K - 12% of total

Bottom 3:
1. Adicross (Women) - $32K - 2% of total
2. Terrex (Women) - $28K - 1.8% of total
3. Training (Women) - $25K - 1.6% of total
```

## 4. What-If Analysis
```dax
// Discount Simulation
Simulated Revenue = 
[Total Sales] * (1 - Parameter[Discount %])

Simulated Profit = 
[Total Sales] * (1 - Parameter[Discount %]) * [Margin %]
```

→ Finding: 15% discount drives 25% volume increase, net profit increases 8%
→ Beyond 25% discount: Volume increase plateaus, profit decreases

## 5. Regional Insights
- West: 35% of revenue (strongest)
- Northeast: 20% of revenue + highest margin (49%)
- Midwest: 15% of revenue — underpenetrated, opportunity for growth
