# Power Query M Code Snippets

## Basic Structure

```m
let
    Source = ...,
    Step1 = ...,
    Step2 = ...
in
    Step2
```

## Common Transformations

### Merge Queries (JOIN)
```m
= Table.NestedJoin(
    Table1, {"Key"}, 
    Table2, {"Key"}, 
    "NewCol", JoinKind.LeftOuter
)
```

### Add Conditional Column
```m
= Table.AddColumn(Source, "Category", each 
    if [Amount] > 1000 then "High" 
    else if [Amount] > 500 then "Medium" 
    else "Low")
```

### Group and Aggregate
```m
= Table.Group(Source, {"Region"}, {
    {"Total", each List.Sum([Amount]), type number},
    {"Count", each Table.RowCount(_), type number}
})
```

### Unpivot Columns
```m
= Table.UnpivotOtherColumns(
    Source, {"ID", "Name"}, "Attribute", "Value"
)
```

## Useful Functions

```m
// Date functions
Date.Year([Date])
Date.Month([Date])
Date.Day([Date])
Date.DayOfWeek([Date], Day.Monday)

// Text functions
Text.Upper([Name]), Text.Lower([Name])
Text.Trim([Name])
Text.Replace([Text], "old", "new")
Text.Length([Name])

// List functions
List.Sum({1, 2, 3})
List.Average({1, 2, 3})
List.Distinct({1, 1, 2, 3})
```


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
