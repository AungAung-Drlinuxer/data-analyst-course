# Module 19: Excel Macros & VBA

## 📌 Macros ဆိုတာဘာလဲ?
Excel ထဲမှာ ထပ်ခါထပ်ခါလုပ်နေရတဲ့အလုပ်တွေကို အလိုအလျောက်လုပ်ပေးတဲ့ Code ပါ။

## Macro ရိုက်ကူးနည်း (Record Macro)
1. View → Macros → Record Macro
2. Name ပေးပါ (e.g., "FormatReport")
3. Shortcut key (e.g., Ctrl + Shift + F)
4. Store in: This Workbook
5. OK → လုပ်ချင်တဲ့အလုပ်တွေလုပ်ပါ
6. View → Macros → Stop Recording

## VBA Editor ကိုဖွင့်နည်း
Alt + F11

## VBA အခြေခံ Code များ
```vba
' Message Box
MsgBox "Hello Excel!"

' Select Cell
Range("A1").Select

' Enter Value
ActiveCell.Value = "Hello"

' Loop Through Cells
For i = 1 To 10
    Cells(i, 1).Value = i
Next i

' If Statement
If Range("A1").Value > 100 Then
    MsgBox "High Value"
Else
    MsgBox "Low Value"
End If
```

## လက်တွေ့ဥပမာ: Auto Format Macro
```vba
Sub FormatReport()
    ' Format Header
    Range("A1:F1").Font.Bold = True
    Range("A1:F1").Interior.Color = RGB(0, 102, 204)
    Range("A1:F1").Font.Color = RGB(255, 255, 255)
    
    ' Auto-fit Columns
    Columns("A:F").AutoFit
    
    ' Add Borders
    Range("A1:F100").Borders.LineStyle = xlContinuous
    
    MsgBox "Formatting Complete!"
End Sub
```

## ✅ Key Takeaways
- Macro Record လုပ်ပြီး VBA Code ကိုလေ့လာနိုင်
- VBA နဲ့ Excel ကို fully automate လုပ်လို့ရ
- Alt + F11 က VBA Editor shortcut
- Security: Macro-enabled workbook (.xlsm) နဲ့သိမ်းပါ
