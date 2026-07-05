# Module 10: Conditional Formatting

## 📌 ဒီ Module မှာလေ့လာရမည့်အကြောင်းအရာများ
- Conditional Formatting ဆိုတာဘာလဲ
- Highlight Cell Rules
- Top/Bottom Rules
- Data Bars, Color Scales, Icon Sets
- Custom Formula Formatting

## Conditional Formatting အသုံးပြုနည်း
Home → Conditional Formatting → Rules များကိုရွေးချယ်ပါ

### 1. Highlight Cell Rules
```
Greater Than → 2000 → Light Red Fill
Less Than → 1000 → Light Green Fill
Between → 1000 and 2000 → Yellow Fill
Text that Contains → "IT" → Red Fill
Duplicate Values → Unique or Duplicate
```

### 2. Top/Bottom Rules
```
Top 10 Items
Top 10 %
Bottom 10 Items
Above Average
Below Average
```

### 3. Data Bars
Cell ထဲမှာ Bar ပုံစံနဲ့ Value ကိုပြမယ်
- Gradient Fill / Solid Fill

### 4. Color Scales
Value အပေါ်မူတည်ပြီးအရောင်ပြောင်း
- 3-Color Scale (Red-Yellow-Green)
- 2-Color Scale (White-Red)

### 5. Icon Sets
```
Traffic Lights (Red/Yellow/Green)
3 Arrows (Up/Sideways/Down)
3 Flags
5 Quarters
```

### 6. Custom Formula
```excel
=AND($D2>2000, $C2="IT")
// IT Department နဲ့ လစာ 2000 အထက်ဆိုရင် format ချယ်မယ်
```

## ✅ Key Takeaways
- Conditional Formatting က data pattern တွေကို visually မြင်ရတယ်
- Data Bars က ranking အတွက်ကောင်းတယ်
- Icon Sets က KPI dashboard အတွက်သုံး
- Custom Formula နဲ့ complex logic သတ်မှတ်လို့ရ
