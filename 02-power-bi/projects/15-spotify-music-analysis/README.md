# Spotify Music Analysis 🎵

## Domain: Entertainment Streaming

---

## 📋 Project Overview

Spotify Music Data ကိုခွဲခြမ်းစိတ်ဖြာပြီး Top Artists, Genre Distribution, Listening Trends များကို Dashboard ဖြင့်ပြသခြင်း။

---

## 📂 Datasets

### `datasets/raw/` — spotify_tracks.csv (1000 rows)

| Column | Description | Data Type |
|--------|------------|-----------|
| `track_id` | သီချင်းနံပါတ် | Integer |
| `track_name` | သီချင်းအမည် | String |
| `artist_name` | အဆိုတော် | String |
| `artist_popularity` | လူကြိုက်မှုအဆင့် | Integer |
| `genre` | ဂီတအမျိုးအစား | String |
| `track_popularity` | သီချင်းလူကြိုက်မှု | Integer |
| `danceability` | ကခုန်နိုင်မှု | Float |
| `energy` | စွမ်းအင် | Float |
| `valence` | ပျော်ရွှင်မှု | Float |
| `tempo` | အရှိန် | Float |
| `duration_ms` | ကြာချိန် | Integer |


---

## 🔌 PowerBI Data Import

```
Get Data → Text/CSV → datasets/raw/*.csv
→ Transform Data (Power Query)
→ Create Relationships
→ Build DAX Measures
→ Design Dashboard
```

---

## 📐 Core DAX Measures

```dax
// Avg Popularity = AVERAGE(spotify[track_popularity])\n// Danceability Avg = AVERAGE(spotify[danceability])\n// Genre Count = DISTINCTCOUNT(spotify[genre])
```

---

## 📊 Dashboard Visuals & Tools

Scatter, Treemap, Radar, Bar Chart, KPI Cards

---

## 💼 Business Problem Solved

### Problem
```
Music label အတွက်: ဘယ် genre က trending လဲ? Audio features က popularity ကိုဘယ်လိုသက်ရောက်လဲ? Hit song ရဲ့ပုံစံကဘာလဲ?
```

### Solution
```diff
+ Scatter for Audio Features + Treemap for Genre + Audio Features Radar + Popularity Analysis
```

---

## 🧪 လက်တွေ့စမ်းသပ်ရန်

1. PowerBI Desktop ကိုဖွင့်ပါ → `Get Data` → CSV ကိုရွေးပါ
2. Power Query တွင် data cleaning လုပ်ပါ (remove nulls, change types)
3. Data model တွင် relationships တည်ဆောက်ပါ
4. DAX measures များကို ရိုက်ထည့်ပါ
5. Visuals များကို configure လုပ်ပါ
6. Dashboard ကို publish လုပ်ပါ (PowerBI Service)

---

## 📝 Dataset Notes
- Dataset သည် synthetic data ဖြစ်ပြီး real-world scenario ကိုအခြေခံထားပါသည်
- `datasets/raw/` တွင် full dataset, `datasets/sample/` တွင် sample data ရှိပါသည်
- PowerBI Desktop ဖြင့် လက်တွေ့စမ်းသပ်နိုင်ပါသည်
