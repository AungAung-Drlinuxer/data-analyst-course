# Module 09: Data Validation

## 📌 ဒီ Module မှာလေ့လာရမည့်အကြောင်းအရာများ
- Data Validation ဆိုတာဘာလဲ
- Drop-down List ပြုလုပ်နည်း
- Input Restriction သတ်မှတ်နည်း
- Error Alert ပြသနည်း

## Data Validation ဆိုတာဘာလဲ?
Cell တွေထဲမှာ သတ်မှတ်ထားတဲ့ Data အမျိုးအစားပဲထည့်လို့ရအောင်လုပ်တာပါ။

## Drop-down List ပြုလုပ်ခြင်း
1. Cell(s) ကိုရွေးပါ
2. Data Tab → Data Validation
3. Allow: List
4. Source: "IT,HR,Sales,Finance,Marketing" (or select range)
5. OK

## Input Restriction
```excel
Allow: Whole Number
Data: between
Minimum: 18
Maximum: 65
→ အသက် 18-65 ကြားပဲထည့်လို့ရမယ်
```

## Error Alert
```
Style: Stop / Warning / Information
Title: "Invalid Input"
Error Message: "Please enter a value between 18 and 65"
```

## ✅ Key Takeaways
- Data Validation က data entry error တွေကိုကာကွယ်တယ်
- Drop-down List က standard data entry အတွက်သုံး
- Custom Formula validation နဲ့ complex rules သတ်မှတ်လို့ရ
