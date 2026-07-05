# Module 03: အခြေခံ Formula ၁၀ မျိုး (10 Important Excel Formulas)

## 📌 ဒီ Module မှာလေ့လာရမည့်အကြောင်းအရာများ
- Excel Formula တွေရဲ့အခြေခံ Syntax
- အရေးကြီးဆုံး Formula ၁၀ မျိုး
- လက်တွေ့အသုံးချပုံများ

## 🔢 Excel Formula Basics

**Formula Format:** `=FUNCTION(argument1, argument2, ...)`

| Symbol | အဓိပ္ပာယ် |
|--------|-----------|
| `=` | Formula စတယ်ဆိုတဲ့သင်္ကေတ |
| `+` | ပေါင်းခြင်း |
| `-` | နုတ်ခြင်း |
| `*` | မြှောက်ခြင်း |
| `/` | စားခြင်း |
| `( )` | အစဉ်လိုက်တွက်ချက်ခြင်း |

## 1. SUM — ပေါင်းခြင်း
```excel
=SUM(A1:A10)         // A1 မှ A10 အထိပေါင်းမယ်
=SUM(A1, B1, C1)     // A1, B1, C1 သီးခြားပေါင်းမယ်
=SUMIF(A1:A10, ">100", B1:B10)    // Condition နဲ့ပေါင်းမယ်
```

## 2. AVERAGE — ပျမ်းမျှတွက်ခြင်း
```excel
=AVERAGE(B2:B100)    // ပျမ်းမျှအဆင့်
=AVERAGEIF(A:A, "IT", B:B)    // IT Department ပျမ်းမျှလစာ
```

## 3. COUNT / COUNTA — အရေအတွက်ရေတွက်ခြင်း
```excel
=COUNT(A1:A100)      // Number ပါတဲ့ Cell အရေအတွက်
=COUNTA(A1:A100)     // Data ရှိတဲ့ Cell အရေအတွက် (Text အပါအဝင်)
=COUNTBLANK(A1:A100) // ဗလာ Cell အရေအတွက်
=COUNTIF(A:A, "IT")  // IT ဆိုတဲ့ Cell အရေအတွက်
```

## 4. MAX / MIN — အများဆုံး / အနည်းဆုံး
```excel
=MAX(D2:D100)        // အမြင့်ဆုံးလစာ
=MIN(D2:D100)        // အနိမ့်ဆုံးလစာ
=LARGE(D2:D100, 2)   // ဒုတိယအမြင့်ဆုံး
=SMALL(D2:D100, 3)   // တတိယအနိမ့်ဆုံး
```

## 5. IF — အခြေအနေစစ်ဆေးခြင်း
```excel
=IF(A1>=60, "Pass", "Fail")
=IF(AND(A1>=60, B1>=60), "Pass", "Fail")
=IF(OR(A1>=80, B1>=80), "Excellent", "Good")
```

## 6. VLOOKUP — ဒေတာရှာဖွေခြင်း
```excel
=VLOOKUP("EMP001", A:D, 4, FALSE)
// EMP001 ကိုရှာပြီး 4th column က လစာကိုထုတ်မယ်
```

## 7. SUMIF / SUMIFS — အခြေအနေနဲ့ပေါင်းခြင်း
```excel
=SUMIF(A:A, "IT", D:D)        // IT Dept လစာစုစုပေါင်း
=SUMIFS(D:D, A:A, "IT", C:C, ">2")  // IT + years>2 စစ်ပြီးပေါင်း
```

## 8. COUNTIF / COUNTIFS
```excel
=COUNTIF(B:B, "Male")         // အမျိုးသားအရေအတွက်
=COUNTIFS(A:A, "IT", B:B, "Male")  // IT ထဲက အမျိုးသားအရေအတွက်
```

## 9. LEFT / RIGHT / MID — Text ဖြတ်ထုတ်ခြင်း
```excel
=LEFT(A1, 3)         // ဘယ်ဘက်က ၃ လုံး
=RIGHT(A1, 4)        // ညာဘက်က ၄ လုံး
=MID(A1, 2, 5)       // ဒုတိယလုံးကနေ ၅ လုံး
```

## 10. CONCATENATE (CONCAT) — Text ဆက်ခြင်း
```excel
=CONCATENATE(A1, " ", B1)    // A1 + Space + B1
=A1 & " - " & B1             // & သင်္ကေတနဲ့လည်းဆက်လို့ရ
=TEXTJOIN(", ", TRUE, A1:A10) // Comma ခြားပြီးဆက်မယ်
```

## 📝 လက်တွေ့စမ်းသပ်ရန်

**Dataset:** `datasets/raw/employees.csv` ကိုသုံးပါ

### Exercise 1: Basic Formulas
```excel
1. =SUM(F2:F201)        → လစာစုစုပေါင်း
2. =AVERAGE(F2:F201)    → ပျမ်းမျှလစာ
3. =MAX(F2:F201)        → အမြင့်ဆုံးလစာ
4. =MIN(F2:F201)        → အနိမ့်ဆုံးလစာ
5. =COUNT(F2:F201)      → ဝန်ထမ်းဦးရေ
```

### Exercise 2: IF Formula
```excel
=IF(F2>=2000, "High Salary", "Standard Salary")
→ လစာ 2000 အထက်ဆိုရင် High, မဟုတ်ရင် Standard
```

## ✅ Key Takeaways
- Formula တွေက = နဲ့စတယ်
- Function တွေက arguments တွေကို () ထဲမှာထည့်
- SUM, AVERAGE, COUNT က အခြေခံအကျဆုံး
- IF က logic စစ်ဖို့သုံး
- VLOOKUP က data ရှာဖို့သုံး
