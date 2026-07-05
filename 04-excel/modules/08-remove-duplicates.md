# Module 08: Remove Duplicates

## 📌 ဒီ Module မှာလေ့လာရမည့်အကြောင်းအရာများ
- Duplicate Data ဆိုတာဘာလဲ
- Remove Duplicates သုံးနည်း
- Conditional Formatting နဲ့ Duplicate ရှာနည်း
- COUNTIF နဲ့ Duplicate စစ်နည်း

## Remove Duplicates အသုံးပြုနည်း
1. Data Tab → Remove Duplicates
2. Column(s) ရွေးပါ
3. OK

### Column Selection သတိထားရန်
```
✓ Select ALL columns → Exact duplicate rows ကိုဖယ်
✓ Select specific columns → ရွေးထားတဲ့ column တူရင် duplicate လို့သတ်မှတ်
```

## Conditional Formatting နဲ့ Duplicate ရှာနည်း
1. Range ကိုရွေးပါ
2. Home → Conditional Formatting → Highlight Cells Rules → Duplicate Values
3. Duplicate တွေကိုအရောင်ခြယ်ပေးမယ်

## COUNTIF နဲ့ Duplicate စစ်နည်း
```excel
=COUNTIF(A:A, A2)>1
// TRUE ဆိုရင် Duplicate ရှိတယ်
// FALSE ဆိုရင် Unique

=IF(COUNTIF(A:A, A2)>1, "Duplicate", "Unique")
```

## လက်တွေ့: dirty_data.csv က Duplicates ရှာပါ
1. Open dirty_data.csv (IDs 3 & 13 are duplicates of ID 1)
2. Select All → Remove Duplicates → 2 duplicates removed
3. Use Conditional Formatting to verify

## ✅ Key Takeaways
- Remove Duplicates က clean data အတွက်ပထမဆုံးလုပ်ရန်
- Exact duplicate vs Partial duplicate ကိုခွဲခြားနားလည်ပါ
- COUNTIF နဲ့ duplicate detection ကိုလက်လုပ်ထားလို့ရ
