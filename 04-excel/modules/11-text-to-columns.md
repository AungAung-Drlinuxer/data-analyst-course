# Module 11: Text to Columns & Flash Fill

## 📌 ဒီ Module မှာလေ့လာရမည့်အကြောင်းအရာများ
- Text to Columns (Delimited / Fixed Width)
- Flash Fill
- လက်တွေ့အသုံးချပုံများ

## Text to Columns
Column တစ်ခုထဲက Data ကို Columns များစွာခွဲဖို့သုံးပါတယ်။

### Delimited (Separator နဲ့ခွဲ)
1. Column ကိုရွေးပါ
2. Data → Text to Columns
3. Delimited → Next
4. Separator: Comma, Tab, Semicolon, Space
5. Finish

### Fixed Width (နေရာအလိုက်ခွဲ)
1. Data → Text to Columns
2. Fixed Width → Next
3. Column break line တွေထားပါ (click to set)
4. Finish

### လက်တွေ့ဥပမာ
```excel
Input:  "Aung, 25, IT, Yangon"
Output: Aung | 25 | IT | Yangon
→ Delimiter: Comma
```

## Flash Fill (Ctrl + E)
Excel 2013+ မှာပါတဲ့အလွန်အသုံးဝင်တဲ့ Feature

### လက်တွေ့ဥပမာများ
```excel
1. Email ကနေ Username ထုတ်ခြင်း:
   "aung@gmail.com" → "aung"
   Type "aung" in next column → Ctrl + E

2. Full Name ကနေ First Name ထုတ်ခြင်း:
   "U Aung Lae" → "U"
   Type "U" → Ctrl + E → Auto Fill

3. Phone Format ပြောင်းခြင်း:
   "0912345678" → "09-123-456-78"
   Type format → Ctrl + E → Auto Fill
```

## ✅ Key Takeaways
- Text to Columns က CSV/System data ခွဲဖို့သုံး
- Flash Fill က pattern တွေကို auto-detect လုပ်တယ်
- Ctrl + E က Flash Fill ရဲ့ shortcut
