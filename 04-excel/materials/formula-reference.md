# Excel Formula Reference 📘

## Lookup & Reference
```excel
=VLOOKUP(lookup, table, col, [exact])
=HLOOKUP(lookup, table, row, [exact])
=XLOOKUP(lookup, lookup_array, return, [if_not_found])
=INDEX(array, row, [col])
=MATCH(lookup, array, [match_type])
=INDEX(A:A, MATCH("value", B:B, 0))  // INDEX-MATCH
=CHOOSE(index, val1, val2, ...)
```

## Logical
```excel
=IF(logical_test, value_if_true, value_if_false)
=IFS(logical1, value1, logical2, value2, ...)
=AND(condition1, condition2, ...)
=OR(condition1, condition2, ...)
=NOT(condition)
=SWITCH(expression, val1, result1, ...)
```

## Math & Trig
```excel
=SUM(numbers)
=SUMIF(range, criteria, [sum_range])
=SUMIFS(sum_range, criteria_range1, criteria1, ...)
=SUMPRODUCT(array1, array2, ...)
=ROUND(number, num_digits)
=ROUNDUP(number, num_digits)
=ROUNDDOWN(number, num_digits)
=MOD(number, divisor)
```

## Statistical
```excel
=AVERAGE(numbers)
=AVERAGEIF(range, criteria, [avg_range])
=COUNT(values)
=COUNTA(values)
=COUNTIF(range, criteria)
=MAX(range) / MIN(range)
=LARGE(array, k) / SMALL(array, k)
=MEDIAN(range)
=MODE(range)
```

## Text
```excel
=LEFT(text, num_chars)
=RIGHT(text, num_chars)
=MID(text, start_num, num_chars)
=LEN(text)
=FIND(find_text, within_text)
=REPLACE(old_text, start, num, new)
=SUBSTITUTE(text, old, new, [n])
=TRIM(text)
=UPPER(text) / LOWER(text) / PROPER(text)
=TEXT(value, format_text)
=TEXTJOIN(delimiter, ignore_empty, text1, ...)
=CONCAT(text1, text2, ...)
```

## Date & Time
```excel
=TODAY()
=NOW()
=DATE(year, month, day)
=YEAR(date) / MONTH(date) / DAY(date)
=EDATE(start_date, months)
=EOMONTH(start_date, months)
=NETWORKDAYS(start, end, [holidays])
=WORKDAY(start, days, [holidays])
=DATEDIF(start, end, "Y")  // Years between
=DATEDIF(start, end, "M")  // Months between
=DATEDIF(start, end, "D")  // Days between
```
