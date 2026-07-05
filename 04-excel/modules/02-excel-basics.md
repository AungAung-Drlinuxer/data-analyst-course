# Module 02: Excel အခြေခံ (Excel Basics)

## 📌 ဒီ Module မှာလေ့လာရမည့်အကြောင်းအရာများ
- Data Entry Techniques
- Cell Formatting (Number, Text, Date)
- Freeze Panes
- Navigation Shortcuts
- Multiple Sheets အလုပ်လုပ်ခြင်း

## 1. Data Entry

### Cell တစ်ခုထဲ Data ထည့်နည်း
1. Cell ကိုရွေးပါ (Click)
2. Data ရိုက်ထည့်ပါ
3. Enter (အောက်ဆင်း) / Tab (ညာဘက်) နှိပ်ပါ

### Data Types
| Data Type | ဥပမာ | Note |
|-----------|-------|------|
| **Text** | "Yangon", "Aung" | Left-aligned |
| **Number** | 100, 25.5, -50 | Right-aligned |
| **Date** | 1/15/2025, 15-Jan-2025 | Right-aligned |
| **Formula** | =A1+B1 | = နဲ့စတယ် |

## 2. Cell Formatting

### Shortcut Keys
| Shortcut | Action |
|----------|--------|
| **Ctrl + 1** | Format Cells Dialog |
| **Ctrl + B** | Bold |
| **Ctrl + I** | Italic |
| **Ctrl + C / V** | Copy / Paste |
| **Ctrl + Z** | Undo |
| **Ctrl + Y** | Redo |
| **Ctrl + S** | Save |
| **Ctrl + Arrow** | Jump to edge of data |

## 3. Freeze Panes (အရေးကြီးဆုံး Basic)

**ဘာအတွက်လဲ:** Header Row တွေကို Scroll လုပ်ရင်မပျောက်အောင်

**အသုံးပြုနည်း:**
1. View Tab → Freeze Panes
2. Freeze Top Row (Row 1 ကိုမပျောက်အောင်)
3. Freeze First Column (Column A ကိုမပျောက်အောင်)
4. Freeze Panes (Cursor အောက်က row & column တွေကိုပါ freeze)

### Step-by-Step:
```
1. Cell B2 ကိုရွေးပါ (Row 1, Column A အောက်)
2. View → Freeze Panes → Freeze Panes
3. ခု Scroll လုပ်ကြည့်ပါ — Header တွေမပျောက်တော့ဘူး
```

## 4. Navigation Shortcuts

| Shortcut | Function |
|----------|----------|
| Ctrl + Home | Go to Cell A1 |
| Ctrl + End | Go to last used cell |
| Ctrl + Page Down | Next Sheet |
| Ctrl + Page Up | Previous Sheet |
| F5 | Go To Dialog |
| Ctrl + Shift + End | Select to last cell |

## 📝 လက်တွေ့စမ်းသပ်ရန်

**Exercise: Employee List တစ်ခုဆောက်ပါ**

1. Row 1 မှာ Header တွေရိုက်ပါ:
   - A1: "Employee ID" | B1: "Name" | C1: "Department" | D1: "Salary"

2. Data ၅ ကြောင်းလောက်ထည့်ပါ:
```
EMP001  Aung     IT      1500
EMP002  Mya      HR      1200
EMP003  Tun      Sales   1800
EMP004  Hla      Finance 2000
EMP005  Kyaw     IT      1600
```

3. Freeze Panes လုပ်ပါ (View → Freeze → Freeze Top Row)
4. Ctrl + Arrow keys သုံးပြီးလေ့ကျင့်ပါ
5. Ctrl + S နဲ့သိမ်းပါ

## ✅ Key Takeaways
- Data Type ၃ မျိုး: Text, Number, Date
- Ctrl + Shortcuts များကိုအလွတ်ကျက်ပါ
- Freeze Panes က report တွေမှာအမြဲသုံးပါ
- Ctrl + Arrow က navigation အတွက်အမြန်ဆုံးလမ်း
