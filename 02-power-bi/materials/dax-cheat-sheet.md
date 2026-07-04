# DAX Cheat Sheet

## Basic Aggregations

```dax
Total Sales = SUM(Sales[Amount])
Total Qty = SUM(Sales[Quantity])
Avg Price = AVERAGE(Products[Price])
Row Count = COUNTROWS(Orders)
Distinct Customers = DISTINCTCOUNT(Sales[CustomerID])
Min Amount = MIN(Sales[Amount])
Max Amount = MAX(Sales[Amount])
```

## Iterator Functions (X Functions)

```dax
Revenue = SUMX(Sales, Sales[Qty] * Sales[Price])
Avg Line = AVERAGEX(Sales, Sales[Qty] * Sales[Price])
```

## CALCULATE (Filter Context Modifier)

```dax
Electronics Sales = 
    CALCULATE([Total Sales], Products[Category] = "Electronics")

Sales 2024 = 
    CALCULATE([Total Sales], 'Calendar'[Year] = 2024)

Sales All = 
    CALCULATE([Total Sales], ALL(Products))
```

## Time Intelligence

```dax
Sales YTD = TOTALYTD([Total Sales], 'Date'[Date])
Sales QTD = TOTALQTD([Total Sales], 'Date'[Date])
Sales MTD = TOTALMTD([Total Sales], 'Date'[Date])
Sales LY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date]))
Sales YoY % = DIVIDE([Total Sales] - [Sales LY], [Sales LY], 0)
```

## Logical Functions

```dax
IF(Sales[Amount] > 1000, "High", "Low")
SWITCH(Products[Category], "A", "Cat A", "B", "Cat B", "Other")
SWITCH(TRUE(), [Total] > 1000, "High", [Total] > 500, "Mid", "Low")
COALESCE(Customers[Phone], Customers[Email], "No Contact")
```

## Filter Functions

```dax
CALCULATE([M], FILTER(Table, Condition))  -- Row-by-row filter
CALCULATE([M], ALL(Table))                 -- Remove all filters
CALCULATE([M], ALLEXCEPT(Table, Col))     -- Keep only Col filter
CALCULATE([M], KEEPFILTERS(Col = "X"))   -- Add filter without removing existing
```

## Date Functions

```dax
YEAR(DateCol), MONTH(DateCol), DAY(DateCol)
WEEKDAY(DateCol, 2)  -- Monday = 1
FORMAT(DateCol, "MMM-YYYY")  -- Jan-2024
DATEDIFF(d1, d2, DAY)
EOMONTH(DateCol, 0)  -- End of current month
```

## Text Functions

```dax
CONCATENATE(a, b)  -- a & b
LEFT(s, n), RIGHT(s, n)
SUBSTITUTE(s, old, new)
SEARCH(find, s, start, 0)  -- Case insensitive
UPPER(s), LOWER(s)
TRIM(s)  -- Remove extra spaces
FORMAT(Value, "#,##0.00")  -- Number formatting
```

## Best Practices

1. Use DIVIDE instead of / (handles division by zero)
2. Use variables for complex measures
3. Use SELECTEDVALUE for slicers
4. Use USERELATIONSHIP for inactive relationships
5. Comment your measures with //


### Useful DAX Patterns

**Pattern 1: Dynamic Ranking**
```dax
Dynamic Rank = 
RANK(
    ALL(Products[Category]),
    ORDERBY([Total Sales], DESC)
)
```

**Pattern 2: New vs Returning Customers**
```dax
New Customers = 
CALCULATE(
    DISTINCTCOUNT(Sales[CustomerID]),
    FILTER(
        Sales,
        Sales[CustomerID] IN 
        VALUES(Customer[CustomerID]) &&
        Sales[OrderDate] = MIN(Customer[FirstPurchaseDate])
    )
)
```

### Power Query Tips

1. Always rename your query steps (descriptive names)
2. Use 'Remove Other Columns' instead of 'Remove Columns' (whitelist approach)
3. Keep data types set correctly (date, number, text)
4. Use native database queries (query folding) for large datasets
5. Avoid expanding entire columns (be selective)


### Useful DAX Patterns

**Pattern 1: Dynamic Ranking**
```dax
Dynamic Rank = 
RANK(
    ALL(Products[Category]),
    ORDERBY([Total Sales], DESC)
)
```

**Pattern 2: New vs Returning Customers**
```dax
New Customers = 
CALCULATE(
    DISTINCTCOUNT(Sales[CustomerID]),
    FILTER(
        Sales,
        Sales[CustomerID] IN 
        VALUES(Customer[CustomerID]) &&
        Sales[OrderDate] = MIN(Customer[FirstPurchaseDate])
    )
)
```

### Power Query Tips

1. Always rename your query steps (descriptive names)
2. Use 'Remove Other Columns' instead of 'Remove Columns' (whitelist approach)
3. Keep data types set correctly (date, number, text)
4. Use native database queries (query folding) for large datasets
5. Avoid expanding entire columns (be selective)


### Useful DAX Patterns

**Pattern 1: Dynamic Ranking**
```dax
Dynamic Rank = 
RANK(
    ALL(Products[Category]),
    ORDERBY([Total Sales], DESC)
)
```

**Pattern 2: New vs Returning Customers**
```dax
New Customers = 
CALCULATE(
    DISTINCTCOUNT(Sales[CustomerID]),
    FILTER(
        Sales,
        Sales[CustomerID] IN 
        VALUES(Customer[CustomerID]) &&
        Sales[OrderDate] = MIN(Customer[FirstPurchaseDate])
    )
)
```

### Power Query Tips

1. Always rename your query steps (descriptive names)
2. Use 'Remove Other Columns' instead of 'Remove Columns' (whitelist approach)
3. Keep data types set correctly (date, number, text)
4. Use native database queries (query folding) for large datasets
5. Avoid expanding entire columns (be selective)


### Useful DAX Patterns

**Pattern 1: Dynamic Ranking**
```dax
Dynamic Rank = 
RANK(
    ALL(Products[Category]),
    ORDERBY([Total Sales], DESC)
)
```

**Pattern 2: New vs Returning Customers**
```dax
New Customers = 
CALCULATE(
    DISTINCTCOUNT(Sales[CustomerID]),
    FILTER(
        Sales,
        Sales[CustomerID] IN 
        VALUES(Customer[CustomerID]) &&
        Sales[OrderDate] = MIN(Customer[FirstPurchaseDate])
    )
)
```

### Power Query Tips

1. Always rename your query steps (descriptive names)
2. Use 'Remove Other Columns' instead of 'Remove Columns' (whitelist approach)
3. Keep data types set correctly (date, number, text)
4. Use native database queries (query folding) for large datasets
5. Avoid expanding entire columns (be selective)


### Useful DAX Patterns

**Pattern 1: Dynamic Ranking**
```dax
Dynamic Rank = 
RANK(
    ALL(Products[Category]),
    ORDERBY([Total Sales], DESC)
)
```

**Pattern 2: New vs Returning Customers**
```dax
New Customers = 
CALCULATE(
    DISTINCTCOUNT(Sales[CustomerID]),
    FILTER(
        Sales,
        Sales[CustomerID] IN 
        VALUES(Customer[CustomerID]) &&
        Sales[OrderDate] = MIN(Customer[FirstPurchaseDate])
    )
)
```

### Power Query Tips

1. Always rename your query steps (descriptive names)
2. Use 'Remove Other Columns' instead of 'Remove Columns' (whitelist approach)
3. Keep data types set correctly (date, number, text)
4. Use native database queries (query folding) for large datasets
5. Avoid expanding entire columns (be selective)


### Useful DAX Patterns

**Pattern 1: Dynamic Ranking**
```dax
Dynamic Rank = 
RANK(
    ALL(Products[Category]),
    ORDERBY([Total Sales], DESC)
)
```

**Pattern 2: New vs Returning Customers**
```dax
New Customers = 
CALCULATE(
    DISTINCTCOUNT(Sales[CustomerID]),
    FILTER(
        Sales,
        Sales[CustomerID] IN 
        VALUES(Customer[CustomerID]) &&
        Sales[OrderDate] = MIN(Customer[FirstPurchaseDate])
    )
)
```

### Power Query Tips

1. Always rename your query steps (descriptive names)
2. Use 'Remove Other Columns' instead of 'Remove Columns' (whitelist approach)
3. Keep data types set correctly (date, number, text)
4. Use native database queries (query folding) for large datasets
5. Avoid expanding entire columns (be selective)


### Useful DAX Patterns

**Pattern 1: Dynamic Ranking**
```dax
Dynamic Rank = 
RANK(
    ALL(Products[Category]),
    ORDERBY([Total Sales], DESC)
)
```

**Pattern 2: New vs Returning Customers**
```dax
New Customers = 
CALCULATE(
    DISTINCTCOUNT(Sales[CustomerID]),
    FILTER(
        Sales,
        Sales[CustomerID] IN 
        VALUES(Customer[CustomerID]) &&
        Sales[OrderDate] = MIN(Customer[FirstPurchaseDate])
    )
)
```

### Power Query Tips

1. Always rename your query steps (descriptive names)
2. Use 'Remove Other Columns' instead of 'Remove Columns' (whitelist approach)
3. Keep data types set correctly (date, number, text)
4. Use native database queries (query folding) for large datasets
5. Avoid expanding entire columns (be selective)


### Useful DAX Patterns

**Pattern 1: Dynamic Ranking**
```dax
Dynamic Rank = 
RANK(
    ALL(Products[Category]),
    ORDERBY([Total Sales], DESC)
)
```

**Pattern 2: New vs Returning Customers**
```dax
New Customers = 
CALCULATE(
    DISTINCTCOUNT(Sales[CustomerID]),
    FILTER(
        Sales,
        Sales[CustomerID] IN 
        VALUES(Customer[CustomerID]) &&
        Sales[OrderDate] = MIN(Customer[FirstPurchaseDate])
    )
)
```

### Power Query Tips

1. Always rename your query steps (descriptive names)
2. Use 'Remove Other Columns' instead of 'Remove Columns' (whitelist approach)
3. Keep data types set correctly (date, number, text)
4. Use native database queries (query folding) for large datasets
5. Avoid expanding entire columns (be selective)


### Useful DAX Patterns

**Pattern 1: Dynamic Ranking**
```dax
Dynamic Rank = 
RANK(
    ALL(Products[Category]),
    ORDERBY([Total Sales], DESC)
)
```

**Pattern 2: New vs Returning Customers**
```dax
New Customers = 
CALCULATE(
    DISTINCTCOUNT(Sales[CustomerID]),
    FILTER(
        Sales,
        Sales[CustomerID] IN 
        VALUES(Customer[CustomerID]) &&
        Sales[OrderDate] = MIN(Customer[FirstPurchaseDate])
    )
)
```

### Power Query Tips

1. Always rename your query steps (descriptive names)
2. Use 'Remove Other Columns' instead of 'Remove Columns' (whitelist approach)
3. Keep data types set correctly (date, number, text)
4. Use native database queries (query folding) for large datasets
5. Avoid expanding entire columns (be selective)
