# Car Sales Dashboard — လက်တွေ့ခွဲခြမ်းစိတ်ဖြာခြင်း 🚗

## 1. Data Overview
- **Sales:** 800 records | **Inventory:** 300 cars
- **Makes:** 14 brands | **Body Styles:** 6 types

## 2. Sales Analysis

### Top Selling Makes
```
1. Toyota - 180 units (22.5%) - Avg Price $32K
2. Honda - 150 units (18.8%) - Avg Price $28K
3. Ford - 110 units (13.8%) - Avg Price $38K
4. BMW - 85 units (10.6%) - Avg Price $52K
5. Tesla - 65 units (8.1%) - Avg Price $55K
```

### Inventory Aging
```dax
// Slow Moving Inventory (60+ days)
Slow Movers = 
COUNTROWS(
    FILTER(car_inventory, 
        car_inventory[days_in_lot] >= 60 
        && car_inventory[status] = "Available"
    )
)
```
→ 45 cars (15% of inventory) are slow-moving — mark down or send to auction

## 3. Payment Type Analysis
- Financing: 55% of sales (highest margin due to finance kickbacks)
- Cash: 30% of sales (fastest turnover)
- Lease: 15% of sales (growing trend, especially for luxury brands)

## 4. Decomposition Tree Insight
```
Sales Decline Root Cause:
├── Volume ↓ 12%
│   ├── SUV segment ↓ 8% (market shift to sedans?)
│   └── Economy cars ↓ 4% (competition from used cars)
├── Price ↓ 5%
│   ├── Incentives ↑ (manufacturer rebates)
│   └── Trade-in values ↓
└── Mix ↓ 2%
    └── Shift from luxury to mid-range
```
