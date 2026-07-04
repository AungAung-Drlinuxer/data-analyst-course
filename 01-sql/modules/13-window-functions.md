# Module 13: Window Functions

## Window Functions ဆိုတာဘာလဲ?

Window functions များသည် row အုပ်စုတစ်ခုပေါ်တွင်တွက်ချက်ပြီး row တစ်ခုချင်းစီအတွက်တန်ဖိုးပြန်ပေးပါသည်။ Aggregate functions များနှင့်မတူသည်မှာ window functions များသည် rows များကိုမစုစည်းဘဲ မူလ rows များအတိုင်းထားရှိပါသည်။ ၎င်းတို့သည် SQL ၏အစွမ်းထက်ဆုံးသော features များထဲမှတစ်ခုဖြစ်ပြီး ranking, running totals, moving averages စသည်တို့ကိုတွက်ချက်ရန်အသုံးပြုပါသည်။

### Window Function Syntax

```sql
window_function() OVER (
    PARTITION BY column1, column2  -- အုပ်စုခွဲရန် (optional)
    ORDER BY column3               -- စီရန် (optional)
    ROWS/RANGE BETWEEN ... AND ... -- frame သတ်မှတ်ရန် (optional)
)
```

### Ranking Functions

| Function | Description | ထူးခြားချက် |
|----------|-------------|-------------|
| ROW_NUMBER() | ဆက်တိုက်နံပါတ်များ | ထပ်တူတန်ဖိုးရှိလျှင်လည်းနံပါတ်ကွာမည် |
| RANK() | အဆင့်သတ်မှတ်ခြင်း | ထပ်တူပါက နံပါတ်တူ၊ နောက်တစ်ခုမှာ ကြားထပ်ကျော်မည် |
| DENSE_RANK() | စုစည်းအဆင့် | ထပ်တူပါက နံပါတ်တူ၊ နောက်တစ်ခုကပ်မည် |
| NTILE(n) | n စုခွဲခြင်း | Rows များကို n အုပ်စုခွဲမည် |

```sql
SELECT 
    Name, Department, Salary,
    ROW_NUMBER() OVER (ORDER BY Salary DESC) AS RowNum,
    RANK() OVER (ORDER BY Salary DESC) AS Rank,
    DENSE_RANK() OVER (ORDER BY Salary DESC) AS DenseRank,
    NTILE(4) OVER (ORDER BY Salary DESC) AS Quartile
FROM Employees;
```

### Aggregate Window Functions

```sql
SELECT 
    Department, Name, Salary,
    SUM(Salary) OVER (PARTITION BY Department) AS DeptTotal,
    AVG(Salary) OVER (PARTITION BY Department) AS DeptAvg,
    MAX(Salary) OVER (PARTITION BY Department) AS DeptMax,
    MIN(Salary) OVER (PARTITION BY Department) AS DeptMin,
    COUNT(*) OVER (PARTITION BY Department) AS DeptCount,
    ROUND(Salary * 100.0 / SUM(Salary) OVER (PARTITION BY Department), 2) AS PctOfDept
FROM Employees;
```

### Value Functions: LEAD / LAG

```sql
SELECT 
    OrderDate, Amount,
    LAG(Amount, 1) OVER (ORDER BY OrderDate) AS PreviousDay,
    LAG(Amount, 7) OVER (ORDER BY OrderDate) AS SameDayLastWeek,
    LEAD(Amount, 1) OVER (ORDER BY OrderDate) AS NextDay,
    Amount - LAG(Amount, 1) OVER (ORDER BY OrderDate) AS DayChange,
    AVG(Amount) OVER (
        ORDER BY OrderDate 
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) AS MovingAvg7Days
FROM DailySales
ORDER BY OrderDate;
```

### FIRST_VALUE / LAST_VALUE

```sql
SELECT 
    Department, Name, Salary,
    FIRST_VALUE(Name) OVER (
        PARTITION BY Department 
        ORDER BY Salary DESC
    ) AS HighestPaid,
    LAST_VALUE(Name) OVER (
        PARTITION BY Department 
        ORDER BY Salary DESC
        RANGE BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
    ) AS LowestPaid
FROM Employees;
```

### Running Total and Moving Average

```sql
SELECT 
    Date, Amount,
    SUM(Amount) OVER (ORDER BY Date) AS RunningTotal,
    AVG(Amount) OVER (
        ORDER BY Date 
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
    ) AS MovingAvg3Days
FROM DailySales;
```

## Exercises

1. Employees ကို ဌာနအလိုက် လစာအမြင့်ဆုံးမှအနိမ့်ဆုံးသို့ RANK လုပ်ပါ။
2. DailySales မှ 7 ရက်ပျမ်းမျှ moving average တွက်ပါ။
3. LAG သုံးပြီး day-over-day sales change ကိုတွက်ပါ။

## Window Functions အသေးစိတ် (Complete Reference with Examples)

Window functions များသည် row အုပ်စုတစ်ခုပေါ်တွင်တွက်ချက်ပြီး row တစ်ခုချင်းစီအတွက် result ပြန်ပေးပါသည်။ Aggregate functions များနှင့်မတူသည်မှာ rows များကိုမစုစည်းဘဲ မူလ rows အတိုင်းထားရှိပါသည်။

### OVER Clause အသေးစိတ်

Window function ၏အဓိက syntax မှာ — function_name() OVER (PARTITION BY col ORDER BY col) ဖြစ်ပါသည်။

**PARTITION BY** — Data ကိုအုပ်စုခွဲရန် (GROUP BY နှင့်ဆင်တူသော်လည်း rows များကိုမစုစည်းပါ)
**ORDER BY** — အုပ်စုတစ်ခုစီအတွင်း rows များကိုစီရန်
**ROWS/RANGE** — Frame သတ်မှတ်ရန် (running total အတွက်)

### ROW_NUMBER vs RANK vs DENSE_RANK

```sql
SELECT 
    Name, Department, Salary,
    ROW_NUMBER() OVER (ORDER BY Salary DESC) AS RowNum,
    -- 1, 2, 3, 4, 5 (ထပ်တူဆိုလည်းနံပါတ်ကွာမည်)
    RANK() OVER (ORDER BY Salary DESC) AS Rank,
    -- 1, 2, 2, 4, 5 (ထပ်တူပါက နံပါတ်တူ၊ နောက်ကွာမည်)
    DENSE_RANK() OVER (ORDER BY Salary DESC) AS DenseRank
    -- 1, 2, 2, 3, 4 (ထပ်တူပါက နံပါတ်တူ၊ နောက်ကပ်မည်)
FROM Employees;
```

### Running Total and Moving Average

```sql
SELECT 
    OrderDate,
    DailyAmount,
    SUM(DailyAmount) OVER (ORDER BY OrderDate) AS RunningTotal,
    AVG(DailyAmount) OVER (
        ORDER BY OrderDate 
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) AS MovingAvg7Days
FROM DailySales;
```

ဤ query သည် -
- Running Total: ပထမရက်မှစပြီးယနေ့အထိစုစုပေါင်း
- Moving Avg 7 Days: လွန်ခဲ့သော ၇ ရက်၏ပျမ်းမျှ (trailing)

### LEAD/LAG for Comparing Values

```sql
SELECT 
    OrderDate, Amount,
    LAG(Amount, 1) OVER (ORDER BY OrderDate) AS PrevDay,
    LAG(Amount, 7) OVER (ORDER BY OrderDate) AS SameDayLastWeek,
    LEAD(Amount, 1) OVER (ORDER BY OrderDate) AS NextDay,
    Amount - LAG(Amount, 1) OVER (ORDER BY OrderDate) AS DayOverDayChange
FROM DailySales;
```

### Exercises

၁။ Employees ကို ဌာနအလိုက်လစာအမြင့်ဆုံးမှအနိမ့်ဆုံးသို့ RANK လုပ်ပါ
၂။ DailySales မှ 7 ရက်ပျမ်းမျှ moving average တွက်ပါ
၃။ LAG သုံးပြီး day-over-day sales change ကိုတွက်ပါ
၄။ ဌာနတစ်ခုစီမှာ လစာအမြင့်ဆုံး ၃ ယောက်ကိုရှာပါ (PARTITION BY + ROW_NUMBER)



## Window Functions Practical Examples

### Window Functions များကိုလက်တွေ့အသုံးပြုခြင်း

Window functions များသည် SQL ၏အစွမ်းထက်ဆုံး feature များထဲမှတစ်ခုဖြစ်ပြီး ranking, running totals, moving averages, lag/lead analysis စသည့်လုပ်ငန်းများအတွက်အသုံးပြုပါသည်။

### Ranking Functions နှိုင်းယှဉ်ချက်

ROW_NUMBER() — Row များကိုဆက်တိုက်နံပါတ်ပေးပါသည်။ တူညီသော ORDER BY value ရှိလျှင်လည်း နံပါတ်ကွဲပါသည် (ties ကိုထည့်မတွက်ပါ)

RANK() — တူညီသော ORDER BY value ရှိပါက နံပါတ်တူပေးပြီး နောက်နံပါတ်ကိုကျော်လိုက်ပါသည် (gaps ရှိသည်)

DENSE_RANK() — တူညီသော ORDER BY value ရှိပါက နံပါတ်တူပေးပြီး နောက်နံပါတ်ကိုကပ်ပေးပါသည် (no gaps)

NTILE(n) — Rows များကို n အုပ်စုခွဲပေးပါသည် (ဥပမာ — quartile ခွဲရန်)

### LEAD/LAG အသေးစိတ်

LAG(column, offset, default) — ယခင်အတန်း (previous row) ၏တန်ဖိုးကိုယူပါသည်
LEAD(column, offset, default) — နောက်အတန်း (next row) ၏တန်ဖိုးကိုယူပါသည်

ဥပမာ — month-over-month growth တွက်ရန် LAG ကိုသုံးနိုင်ပြီး 7-day moving average အတွက် ROWS BETWEEN frame ကိုသုံးနိုင်ပါသည်။

### Window Function Frame Specification

ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW — ပထမဆုံးရက်မှယနေ့အထိ
ROWS BETWEEN 6 PRECEDING AND CURRENT ROW — လွန်ခဲ့သော ၇ ရက် (လက်ရှိအပါအဝင်)
ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING — ယနေ့မှနောက်ဆုံးရက်အထိ
ROWS BETWEEN 3 PRECEDING AND 3 FOLLOWING — ပတ်ဝန်းကျင် ၇ ရက်

### Common Window Function Patterns

၁။ ဌာနအလိုက်လစာအမြင့်ဆုံး employee — ROW_NUMBER() OVER (PARTITION BY Dept ORDER BY Salary DESC)
၂။ Daily running total — SUM(Amount) OVER (ORDER BY Date)
၃။ Previous period comparison — LAG(Amount) OVER (ORDER BY Date)
၄။ Moving average — AVG(Price) OVER (ORDER BY Date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)
၅။ Percent of total — SUM(Sales) OVER (PARTITION BY Category) / SUM(Sales) OVER ()

Window functions ကိုကျွမ်းကျင်စွာအသုံးပြုနိုင်ပါက complex aggregations များကိုရှင်းရှင်းလင်းလင်းရေးသားနိုင်ပါသည်။



### Window Functions Performance

Window functions များသည် powerful ဖြစ်သော်လည်း performance ကိုထိခိုက်နိုင်ပါသည်။

**Performance Tips** —
၁။ PARTITION BY column တွင် index ထားပါ
၂။ ORDER BY column တွင် index ထားပါ
၃။ Large window frames များကိုရှောင်ပါ
၄။ Multiple window functions များအစား single pass ကိုသုံးပါ
၅။ Window function ကို temp table သို့ဖြတ်ပြီးသုံးနိုင်

**When to Avoid Window Functions** —
- Very large datasets (millions of rows) အတွက် self-join သို့ temp table ကပိုမြန်နိုင်
- Real-time reporting အတွက် pre-aggregated tables များသုံးရန်
- Page-level calculations အတွက် application layer သုံးရန်

Window functions များသည် SQL ၏အစွမ်းထက်ဆုံးသော features များထဲမှတစ်ခုဖြစ်ပြီး ကျွမ်းကျင်စွာအသုံးပြုနိုင်ပါက complex analytical queries များကိုရေးသားနိုင်ပါသည်။

### Practical Window Function Applications

**1. Department Salary Analysis**
```sql
SELECT 
    Name, Department, Salary,
    AVG(Salary) OVER (PARTITION BY Department) AS DeptAvg,
    Salary - AVG(Salary) OVER (PARTITION BY Department) AS DiffFromAvg,
    ROUND(Salary * 100.0 / SUM(Salary) OVER (PARTITION BY Department), 2) AS PctOfDept
FROM Employees;
```

**2. Customer Order Pattern Analysis**
```sql
SELECT 
    CustomerID, OrderDate, Amount,
    LAG(OrderDate) OVER (PARTITION BY CustomerID ORDER BY OrderDate) AS PrevOrderDate,
    DATEDIFF(DAY, LAG(OrderDate) OVER (PARTITION BY CustomerID ORDER BY OrderDate), OrderDate) AS DaysBetweenOrders,
    SUM(Amount) OVER (PARTITION BY CustomerID ORDER BY OrderDate) AS CumulativeSpend,
    ROW_NUMBER() OVER (PARTITION BY CustomerID ORDER BY OrderDate DESC) AS OrderNumber
FROM Orders;
```

**3. Product Ranking by Category**
```sql
SELECT 
    ProductID, ProductName, Category, Price,
    ROW_NUMBER() OVER (PARTITION BY Category ORDER BY Price DESC) AS PriceRank_Category,
    DENSE_RANK() OVER (ORDER BY Price DESC) AS OverallRank,
    NTILE(4) OVER (ORDER BY Price DESC) AS PriceQuartile
FROM Products;
```
