# Module 05: IF Formula အဆင့်မြင့် (Advanced IF Formulas)

## 📌 ဒီ Module မှာလေ့လာရမည့်အကြောင်းအရာများ
- Nested IF (အဆင့်ဆင့် IF)
- IFS Function (Excel 365)
- AND, OR, NOT with IF
- SWITCH Function
- လက်တွေ့အသုံးချပုံများ

## 1. Nested IF (အဆင့်ဆင့် IF)

```excel
=IF(condition1, result1,
    IF(condition2, result2,
        IF(condition3, result3, default)))
```

### ဥပမာ: Grade တွက်ခြင်း
```excel
=IF(A1>=80, "Distinction",
    IF(A1>=60, "Pass",
        IF(A1>=40, "Retake", "Fail")))
```

## 2. IFS Function (ပိုရှင်းတဲ့ Nested IF)

```excel
=IFS(A1>=80, "Distinction", A1>=60, "Pass", A1>=40, "Retake", TRUE, "Fail")
```

## 3. AND / OR / NOT

```excel
=IF(AND(A1>=60, B1>=60), "Pass", "Fail")
=IF(OR(A1>=80, B1>=80), "Excellent", "Good")
=IF(NOT(C1=""), "Has Data", "Empty")
```

### လက်တွေ့ဥပမာ: Bonus Calculation
```excel
=IF(AND(F2>3, G2>90%), "Full Bonus",
    IF(OR(F2>3, G2>90%), "Half Bonus", "No Bonus"))
```

## 4. SWITCH Function

```excel
=SWITCH(A1, "IT", "Tech", "HR", "People", "Finance", "Money", "Other")
// Department Code တွေကို Full Name ပြောင်းမယ်
```

## 📝 လက်တွေ့စမ်းသပ်ရန်

### Exercise: Employee Bonus Calculator
```excel
Dataset: employees.csv

IF(AND(F2>3, K2>=90), HIGH BONUS,
   IF(AND(F2>1, K2>=80), MEDIUM BONUS,
      IF(K2>=75, LOW BONUS, NO BONUS)))

Years Exp > 3 + Attendance >= 90% → High Bonus (100%)
Years Exp > 1 + Attendance >= 80% → Medium Bonus (50%)
Attendance >= 75% → Low Bonus (25%)
Otherwise → No Bonus
```
