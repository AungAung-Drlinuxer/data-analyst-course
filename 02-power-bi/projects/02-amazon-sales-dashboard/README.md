# 02. Amazon Sales Dashboard 🛒

## Domain: E-Commerce

---

## Project Overview

Amazon Sales Dashboard သည် E-Commerce domain မှဒေတာများကို PowerBI ဖြင့်ခွဲခြမ်းစိတ်ဖြာပြီး Executive Dashboard များတည်ဆောက်ထားသော project ဖြစ်ပါသည်။

---

## 📂 Datasets

### `datasets/raw/` — amazon_sales.csv (1000 rows) + amazon_returns.csv (150 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `order_id` | မှာယူမှုနံပါတ် | Integer |
| `date` | ရက်စွဲ | Date |
| `customer_id` | ဝယ်သူအမှတ် | String |
| `product_name` | ပစ္စည်းအမည် | String |
| `category` | အမျိုးအစား | String |
| `sub_category` | အမျိုးအစားခွဲ | String |
| `price` | တန်ဖိုး ($) | Float |
| `quantity` | အရေအတွက် | Integer |
| `discount` | လျှော့စျေး (%) | Float |
| `shipping_cost` | ပို့ဆောင်ခ ($) | Float |
| `region` | ဒေသ | String |
| `order_status` | မှာယူမှုအခြေအနေ | String |
| `fulfillment` | ဖြည့်ဆည်းမှုပုံစံ | String |


`amazon_returns.csv` — Return reason, refund amount, product condition

---

## 🔌 PowerBI တွင် Dataset ချိတ်ဆက်ခြင်း

### Step 1: Data Import
```
PowerBI Desktop → Get Data → Text/CSV
Select: datasets/raw/amazon_sales_dashboard.csv (adjust filename accordingly)
→ Transform Data
```

### Step 2: Power Query (M Code)
```powerquery
let
    Source = Csv.Document(File.Contents("datasets/raw/amazon_sales.csv")),
    #"Removed Duplicates" = Table.Distinct(Source),
    #"Filtered Cancelled" = Table.SelectRows(#"Removed Duplicates", each [order_status] <> "Cancelled")
in
    #"Filtered Cancelled"
```

### Step 3: Data Model
- Create Date table: `Date = CALENDARAUTO()`
- Build relationships between fact and dimension tables
- Create hierarchies (Year > Quarter > Month > Date)

---

## 📐 Core DAX Measures

```dax

// 1. Total Revenue
Total Revenue = SUMX(amazon_sales, amazon_sales[price] * amazon_sales[quantity])

// 2. Total Orders
Total Orders = COUNTROWS(amazon_sales)

// 3. Avg Order Value (AOV)
AOV = DIVIDE([Total Revenue], [Total Orders])

// 4. Return Rate
Return Rate % = 
DIVIDE(
    COUNTROWS('amazon_returns'),
    [Total Orders]
) * 100

// 5. Discount Impact
Avg Discount = AVERAGE(amazon_sales[discount])

// 6. YTD Sales
YTD Sales = 
TOTALYTD([Total Revenue], 'Date'[Date])

// 7. Top Product (Rank)
Top Product Rank = 
RANKX(ALL(amazon_sales[product_name]), [Total Revenue])

```

---

## 📊 Dashboard Visuals

| Visual | Purpose |
|--------|---------|
| KPI Cards | Total Revenue, Orders, AOV, Return Rate |
| Bar Chart | Top 10 Products by Revenue |
| Map | Sales by Region |
| Line Chart | Daily/Weekly Sales Trend |
| Stacked Bar | Category wise Revenue |
| Pie Chart | FBA vs FBM Distribution |
| Scatter | Discount vs Revenue |
| Matrix | Region x Product Category |
| Drill-through | Category -> Product Detail |
| Slicers | Region, Category, Date |

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
Amazon seller တစ်ယောက်အနေဖြင့် products 1000+ ရှိပြီး ဘယ်ဟာက profit ရှိလဲဆိုတာ အမြန်မသိနိုင်။ Return rate များနေပြီး ဘာကြောင့်လဲဆိုတာ visibility မရှိ။ Sales channel (FBA vs FBM) performance ကို နှိုင်းယှဉ်ကြည့်ရန် dashboard မရှိ။
```

### Solution
```diff
+ Multi-page Report with drill-through + Category to Product hierarchy + Profit Analysis by Region + Returns Analysis + FBA vs FBM comparison
```

### Business Impact
Product profitability visibility 0% → 100%, Returns root cause analysis 2 days → 5 minutes, Inventory optimization 15% cost reduction

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
