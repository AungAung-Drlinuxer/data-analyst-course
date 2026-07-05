# Module 04: Lookup Functions (VLOOKUP, HLOOKUP, XLOOKUP)

## 📌 ဒီ Module မှာလေ့လာရမည့်အကြောင်းအရာများ
- VLOOKUP — Vertical Lookup
- HLOOKUP — Horizontal Lookup
- XLOOKUP — Excel 365 ရဲ့ Lookup အသစ်
- လက်တွေ့အသုံးချပုံများ

## 1. VLOOKUP — ဒေါင်လိုက်ရှာဖွေခြင်း

### Syntax
```excel
=VLOOKUP(lookup_value, table_array, col_index_num, [range_lookup])
```

| Parameter | အဓိပ္ပာယ် |
|-----------|-----------|
| `lookup_value` | ရှာချင်တဲ့တန်ဖိုး (e.g., "EMP001") |
| `table_array` | ရှာရမည့် Table Range (e.g., A:D) |
| `col_index_num` | ထုတ်ချင်တဲ့ Column နံပါတ် (1, 2, 3...) |
| `range_lookup` | FALSE=Exact match, TRUE=Approximate match |

### ဥပမာ
```excel
=VLOOKUP("EMP001", A:D, 4, FALSE)
// EMP001 ရဲ့ လစာ (4th column) ကိုထုတ်မယ်

=VLOOKUP(E2, Products!A:E, 3, FALSE)
// Product ID နဲ့ Unit Price ကိုထုတ်မယ် (အခြား Sheet ကနေ)
```

### VLOOKUP အရေးကြီးအချက်များ
1. **Lookup value က ပထမဆုံး Column မှာရှိရမယ်**
2. **Exact match အတွက် FALSE ထည့်ပါ**
3. **#N/A Error** — တန်ဖိုးမတွေ့ရင် Error ပြမယ်

## 2. HLOOKUP — အလျားလိုက်ရှာဖွေခြင်း

### Syntax
```excel
=HLOOKUP(lookup_value, table_array, row_index_num, [range_lookup])
```

VLOOKUP နဲ့တူတူပါပဲ — ဒါပေမယ့် Column မဟုတ်ဘဲ Row ကနေရှာတယ်။

## 3. XLOOKUP — ခေတ်သစ် Lookup (Excel 365 / 2021)

### Syntax
```excel
=XLOOKUP(lookup_value, lookup_array, return_array, [if_not_found], [match_mode], [search_mode])
```

| Parameter | အဓိပ္ပာယ် |
|-----------|-----------|
| `if_not_found` | တန်ဖိုးမတွေ့ရင် ပြမယ့်စာသား |
| `match_mode` | 0=Exact, -1=Next smaller, 1=Next larger, 2=Wildcard |
| `search_mode` | 1=First to last, -1=Last to first |

### XLOOKUP ရဲ့အားသာချက်များ
```excel
=XLOOKUP(E2, A:A, D:D)
// VLOOKUP လိုပထမဆုံး Column မှာရှိစရာမလိုဘူး
// ဘယ် Column ကမဆိုရှာလို့ရ

=XLOOKUP(E2, A:A, D:D, "Not Found")
// #N/A အစား "Not Found" ဆိုပြီးပြမယ်

=XLOOKUP(E2, A:A, C:C,,, -1)
// နောက်ဆုံးတွေ့တာကိုရှာမယ် (Search Mode -1)
```

## 📝 လက်တွေ့စမ်းသပ်ရန်

### Exercise 1: VLOOKUP with Products Dataset
```excel
Dataset: datasets/raw/sales_2025.csv + datasets/raw/products.csv

1. Sales Sheet မှာ Product Price ကိုရှာမယ်
   =VLOOKUP(C2, Products!A:E, 4, FALSE)

2. Product Category ကိုရှာမယ်
   =VLOOKUP(C2, Products!A:E, 3, FALSE)
```

### Exercise 2: XLOOKUP
```excel
= XLOOKUP(C2, Products!A:A, Products!D:D, "Price Not Found")
```

## ✅ Key Takeaways
- VLOOKUP: Old standard — lookup column must be first
- HLOOKUP: Horizontal version (rarely used)
- XLOOKUP: Best choice if available — flexible, no column restriction
- Always use FALSE for exact match with VLOOKUP
