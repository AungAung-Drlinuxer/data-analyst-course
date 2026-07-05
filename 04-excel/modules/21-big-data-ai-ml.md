# Module 21: Big Data, AI, ML Basics

## 📌 Big Data ဆိုတာဘာလဲ?
သမားရိုးကျနည်းနဲ့ manage လုပ်လို့မရတဲ့ ကြီးမားရှုပ်ထွေးတဲ့ Data အစုအဝေးပါ။

## 3Vs of Big Data

```
1. Volume (ပမာဏ) — Data ပမာဏကြီးမားခြင်း
   → TB, PB, EB အဆင့်

2. Velocity (အမြန်နှုန်း) — Data ထုတ်လုပ်မှုမြန်ဆန်ခြင်း
   → Real-time, Streaming Data

3. Variety (အမျိုးအစား) — Data အမျိုးအစားစုံလင်ခြင်း
   → Structured (Tables)
   → Semi-structured (JSON, XML)
   → Unstructured (Text, Images, Video)
```

### 3Vs → 7Vs → 10Vs
နောက်ထပ် V တွေလည်းရှိပါသေးတယ်:
- Veracity (မှန်ကန်မှု)
- Value (တန်ဖိုး)
- Variability (ပြောင်းလဲနိုင်မှု)
- Visualization
- Validity

## Structured vs Semi-structured vs Unstructured

| Type | ဥပမာ | Excel နဲ့ဖွင့်လို့ရလား |
|------|-------|----------------------|
| **Structured** | Excel Table, SQL Table | ✓ Yes |
| **Semi-structured** | JSON, XML, CSV | ✓ Partial |
| **Unstructured** | Images, Videos, Text | ✗ No |

## AI vs ML vs Deep Learning

```
AI (Artificial Intelligence)
├── ML (Machine Learning)
│   ├── Deep Learning
│   │   ├── Neural Networks
│   │   └── Transformers (GPT)
│   ├── Regression
│   ├── Classification
│   └── Clustering
└── Expert Systems
```

### Machine Learning Green Apple Case
```python
# ပန်းသီးအစိမ်း vs ပန်းသီးမှည့် ခွဲခြားခြင်း
Features: Color (Green→Red), Firmness (Hard→Soft), Size
Label: Ripe (Yes/No)

ML Model က ဒီ features တွေကိုကြည့်ပြီး ဘယ်ဟာမှည့်ပြီလဲဆိုတာခန့်မှန်းတယ်
```

## ✅ Key Takeaways
- Big Data = Volume + Velocity + Variety
- Data type 3 မျိုး: Structured, Semi-structured, Unstructured
- AI › ML › Deep Learning — အဆင့်ဆင့်ပါဝင်
- ML က data ကနေ learn လုပ်ပြီး predict လုပ်တယ်
