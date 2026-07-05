# Module 22: How To Use Python In Excel

## 📌 Python in Excel (Excel 365)
Excel 365 မှာ Python Code တွေကို Excel Formula လိုပဲရေးလို့ရပါပြီ။

## PY Function
```python
=PY(print("Hello from Python!"), "")
```

## လက်တွေ့ဥပမာများ

### 1. Basic Python in Cell
```python
=PY(x + y, "")
# x နဲ့ y က Excel range တွေဖြစ်နိုင်
```

### 2. Data Analysis with Pandas
```python
=PY(df.describe(), "")
# df က Excel table — statistics တွေထုတ်မယ်
```

### 3. Visualization
```python
=PY(
import matplotlib.pyplot as plt
plt.plot(df["Date"], df["Sales"])
plt.show()
, "")
```

## Python vs Excel Formulas

| Task | Excel Formula | Python |
|-----|---------------|--------|
| Sum | =SUM(A:A) | df['col'].sum() |
| Average | =AVERAGE(A:A) | df['col'].mean() |
| Filter | Filter button | df[df['col']>100] |
| Group By | Pivot Table | df.groupby().agg() |
| Chart | Insert Chart | matplotlib/plotly |

## Prerequisites
- Microsoft 365 (Excel for Windows, Beta Channel)
- Python in Excel preview enabled

## ✅ Key Takeaways
- =PY() function နဲ့ Excel ထဲမှာ Python ရေးလို့ရ
- Pandas, Matplotlib libraries တွေကို Excel မှာသုံးလို့ရ
- Complex analysis အတွက် Excel formulas ထက် Python ကပိုအဆင်ပြေ
