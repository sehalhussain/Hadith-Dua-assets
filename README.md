# 📚 Islamic Hadith & Dua Assets

A comprehensive collection of Hadith and Duas sourced from authentic Islamic texts. Open-sourced for developers to use in their projects.

> **Prepared while building Kitably • Open for the community**
> Built for [Kitably — Quran & Sunnah. Download on Google Play](https://play.google.com/store/apps/details?id=com.sehalhussain.kitably)

---

## 📖 Overview

This repository contains structured, machine-readable Islamic assets — **7 major Hadith collections** scraped from sunnah.com in SQLite databases and **300+ Duas & Adhkar** from Hisnul Muslim in JSON format. Each hadith includes Arabic text, English translation, narrator information, grading, and cross-references. 

✨ Why this exists

While building Kitably, I realised preparing Islamic content took more effort than building features.

This repo contains some of the structured assets prepared along the way so other students and developers can build faster.

---

## 🗂️ Repository Structure

```
Hadith-Dua-assets/
│
├── 📄 Hadith Databases (SQLite .db)
│   ├── sahih_al_bukhari.db                          # Sahih al-Bukhari (7,580 hadith)
│   ├── bukhari_hadith_db_with_reference.db           # Sahih al-Bukhari with references (7,580 hadith)
│   ├── sahih_al_muslim.db                            # Sahih Muslim (7,541 hadith)
│   ├── muslim_hadith_db_with_reference.db             # Sahih Muslim with references (7,541 hadith)
│   ├── jami_at_tirmidhi.db                           # Jami` at-Tirmidhi (4,063 hadith)
│   ├── sunan_abi_dawud.db                            # Sunan Abi Dawud (5,276 hadith)
│   ├── sunan_an_nasai.db                             # Sunan an-Nasai (5,687 hadith)
│   ├── sunan_ibn_majah.db                            # Sunan Ibn Majah (4,345 hadith)
│   ├── riyad_as_salihin.db                           # Riyad as-Salihin (1,896 hadith)
│   └── riyadassalihin_hadith_db_reference.db          # Riyad as-Salihin with references (1,896 hadith)
│
└── 📄 Duas & Adhkar
    └── duas-adhkar-hisnul-muslim.json                # Complete Hisnul Muslim collection
```

---

## 📕 Hadith Collections

### Included Collections

| Collection | Hadith Count | Database File |
|---|---|---|
| **Sahih al-Bukhari** | 7,580 | `sahih_al_bukhari.db` / `bukhari_hadith_db_with_reference.db` |
| **Sahih Muslim** | 7,541 | `sahih_al_muslim.db` / `muslim_hadith_db_with_reference.db` |
| **Jami` at-Tirmidhi** | 4,063 | `jami_at_tirmidhi.db` |
| **Sunan Abi Dawud** | 5,276 | `sunan_abi_dawud.db` |
| **Sunan an-Nasai** | 5,687 | `sunan_an_nasai.db` |
| **Sunan Ibn Majah** | 4,345 | `sunan_ibn_majah.db` |
| **Riyad as-Salihin** | 1,896 | `riyad_as_salihin.db` / `riyadassalihin_hadith_db_reference.db` |

### Two Database Formats

Each major collection (Bukhari, Muslim, Riyad as-Salihin) is available in two formats:

#### 1. Standard Format

Used by the base `.db` files (`sahih_al_bukhari.db`, etc.)

| Column | Type | Description |
|---|---|---|
| `sr_no` | INTEGER | Serial / Hadith number |
| `book_num` | INTEGER | Book number within the collection |
| `english_title` | TEXT | English name of the book/chapter |
| `arabic_title` | TEXT | Arabic name of the book/chapter |
| `local_num` | TEXT | Collection-prefixed reference (e.g., `Sahih al-Bukhari 1`) |
| `title` | TEXT | Hadith title / subject |
| `narrator` | TEXT | Narrator (isnad chain starter) |
| `english_text` | TEXT | English translation of the hadith |
| `arabic_text` | TEXT | Arabic text of the hadith |
| `grade` | TEXT | Authentication grade (e.g., Sahih, Hasan) |

**Table name:** `hadith_library`

#### 2. Reference Format

Used by the `_with_reference.db` files (`bukhari_hadith_db_with_reference.db`, etc.)

| Column | Type | Description |
|---|---|---|
| `raw_ref_key` | TEXT | International searchable reference key |
| `book_num` | INTEGER | Book number |
| `local_num` | TEXT | Collection-prefixed number (e.g., `Sahih al-Bukhari 1`) |
| `title` | TEXT | Hadith title / subject |
| `narrator` | TEXT | Narrator (isnad chain starter) |
| `english_text` | TEXT | English translation of the hadith |
| `arabic_text` | TEXT | Arabic text of the hadith |
| `in_book_reference` | TEXT | In-book reference (e.g., `Book 1, Hadith 1`) |
| `usc_msa_reference` | TEXT | USC-MSA reference (e.g., `Vol. 1, Book 1, Hadith 1`) |
| `grade` | TEXT | Authentication grade |

**Table name:** Matches the collection name (e.g., `sahih_bukhari`, `sahih_muslim`, `riyad_as_salihin`)

### Sample Query

```sql
-- Find hadith by reference
SELECT * FROM sahih_bukhari WHERE usc_msa_reference = 'Vol. 1, Book 1, Hadith 1';

-- Search hadith by keyword in English text
SELECT * FROM hadith_library WHERE english_text LIKE '%intention%';

-- Get all hadith from a specific book
SELECT * FROM hadith_library WHERE book_num = 1;
```

---

## 🤲 Duas & Adhkar (Hisnul Muslim)

The `duas-adhkar-hisnul-muslim.json` file contains a complete collection of daily supplications from **Hisnul Muslim** (Fortress of the Muslim), structured for easy access and integration.

### Structure

```json
{
  "segments": [
    {
      "segment_id": 1,
      "segment_name": "Daily Life",
      "categories": [
        {
          "category_id": 1,
          "category_name": "Waking & Sleeping",
          "titles": [
            {
              "title_id": 2,
              "title_name": "Before Sleeping",
              "duas": [
                {
                  "id": 4,
                  "arabic": "بِاسْمِكَ رَبِّي...",
                  "latin": "Bismika rabbee wadaAAtu janbee...",
                  "translation": "In Your name my Lord, I lie down...",
                  "source": "At-Tirmidhi: 3401",
                  "benefits": null
                }
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

### Dua Fields

| Field | Type | Description |
|---|---|---|
| `id` | INTEGER | Unique identifier for the dua |
| `arabic` | TEXT | Arabic text of the supplication |
| `latin` | TEXT | Transliteration in Latin script |
| `translation` | TEXT | English translation |
| `source` | TEXT | Source reference (e.g., hadith collection and number) |
| `benefits` | STRING or null | Benefits of reciting the dua (if available) |

### Segments

The collection is organized into **6 main segments**:

#### 📖 Daily Life
- **Waking & Sleeping** — Duas for before sleeping and upon waking
- **Toilet & Ablution** — Duas for entering/leaving toilet and performing wudu
- **Home & Travel** — Duas for leaving/entering home, travel, and accommodation
- **Food & Drink** — Duas for meals, drinks, milk, dining, fasting, and Iftar
- **Clothing & Appearance** — Duas for wearing clothes and looking in the mirror

#### 📖 Prayer
- **Adhan & Iqamah** — Duas during and after the call to prayer
- **Before Prayer** — Duas after Takbeer at start of prayer
- **During Prayer** — Duas for Ruku, Sujood, Tashahhud, Darood, and Qunoot
- **After Prayer** — Duas after Fajr, Tasbeeh, and remembrances
- **Masjid** — Duas for entering and leaving the mosque

#### 📖 Remembrance
- **Morning & Evening** — Morning and evening adhkar
- **Praising Allah** — Duas for glorification, thanking, and praising Allah
- **Seeking Forgiveness** — Duas for forgiveness, repentance, and Allah's mercy
- **Protection** — Duas for protection from evil, Satan, enemies, disasters, and more
- **Daily Needs** — Everyday duas, sustenance (Rizq), and success

#### 📖 Life Situations
- **Health & Sickness** — Duas for health, visiting the sick, pain, trials, and death
- **Family & Children** — Duas for parents, family blessings, and children
- **Hardship & Patience** — Duas for distress, patience, anger, trust in Allah, and more
- **Loss & Grief** — Duas when facing loss
- **Success & Rizq** — Duas for settling debts and financial matters

#### 📖 Faith & Hereafter
- **Strengthening Faith** — Duas to strengthen Imaan and for righteous company
- **Knowledge & Wisdom** — Duas for increasing knowledge, eloquence, and wisdom
- **Day of Judgment** — Duas for forgiveness and protection from Hell
- **Paradise & Hell** — Duas for Jannah

#### 📖 Special Occasions
- **Hajj & Umrah** — Talbiyah, Takbeer, Tawaf, Arafat, Jamarat, and more
- **Ramadan** — Duas for crescent moon sighting and Laylatul Qadr
- **Death & Funeral** — Duas for condolence, funeral prayer, and burial
- **Nature & Weather** — Duas for rain, thunder, and windstorms
- **Social Etiquette** — Duas for greeting, sneezing, marketplace, and gatherings
- **Guidance & Decisions** — Duas for Istikhara, justice, and seeking guidance

---

## 🚀 Getting Started

### Using Hadith Databases

These are standard SQLite databases. You can use them with any programming language or tool that supports SQLite.

**Python:**
```python
import sqlite3

conn = sqlite3.connect('sahih_al_bukhari.db')
cursor = conn.cursor()

# Search for a hadith
cursor.execute("SELECT title, english_text FROM hadith_library WHERE english_text LIKE ?", ('%intention%',))
for row in cursor.fetchall():
    print(f"Title: {row[0]}\nText: {row[1]}\n")

conn.close()
```

**JavaScript / Node.js:**
```javascript
const Database = require('better-sqlite3');
const db = new Database('sahih_al_bukhari.db');

const hadith = db.prepare('SELECT * FROM hadith_library WHERE sr_no = ?').get(1);
console.log(hadith);

db.close();
```

**Kotlin / Android:**
```kotlin
// Using Android's built-in SQLite support
val dbHelper = object : SQLiteOpenHelper(context, "sahih_al_bukhari.db", null, 1) {
    override fun onCreate(db: SQLiteDatabase) {}
    override fun onUpgrade(db: SQLiteDatabase, old: Int, new: Int) {}
}
val db = dbHelper.readableDatabase
val cursor = db.rawQuery("SELECT * FROM hadith_library WHERE sr_no = ?", arrayOf("1"))
```

### Using Duas JSON

```javascript
const duas = require('./duas-adhkar-hisnul-muslim.json');

// Access segments
duas.segments.forEach(segment => {
    console.log(segment.segment_name);
    segment.categories.forEach(category => {
        console.log(`  - ${category.category_name}`);
        category.titles.forEach(title => {
            console.log(`    • ${title.title_name}`);
            title.duas.forEach(dua => {
                console.log(`      Arabic: ${dua.arabic}`);
                console.log(`      Translation: ${dua.translation}`);
            });
        });
    });
});
```

---

## 📱 About Kitably

**[Kitably — Quran & Sunnah](https://play.google.com/store/apps/details?id=com.sehalhussain.kitably)** brings together the essential Islamic tools you use every day: Quran, Tafsir, Hadith, Prayer Times, Duas, and Qibla. All inside one beautifully designed experience. built using these very assets. It provides:

-  Personalized Quran experience with Translations, transliteration, reciters, font controls, and reading preferences

- Contextual Tafsir: Tap any ayah and instantly explore multiple Tafsir sources (Ibn Kathir, Maariful Quran, Tazkirul Quran), with offline access
-  Searchable Hadith collections with Arabic & English
-  Daily Duas with transliteration
-  Clean, easy-to-navigate interface
-  Offline access to all content

**[Download now on Google Play](https://play.google.com/store/apps/details?id=com.sehalhussain.kitably)**

---

## 📋 License & Attribution

This project is **open-source** and free for anyone to use in their projects.

**You are free to:**
- ✅ Use these assets in personal and commercial projects
- ✅ Modify and adapt the data for your needs
- ✅ Distribute the data in your applications

### Attribution (Appreciated, Not Required)

If these assets become useful in your project, credit is appreciated but never expected.

Example:

> Built using Islamic assets prepared by Sehal Hussain for Kitably — https://play.google.com/store/apps/details?id=com.sehalhussain.kitably

If not, please remember me in your duas 🤍

---

## 🤝 Contributing

Contributions, improvements, and corrections are welcome. If you find any errors in the hadith text, translations, or references, feel free to open an issue or submit a pull request.

---

*May Allah accept this effort and make it beneficial for the Ummah. Ameen.*
