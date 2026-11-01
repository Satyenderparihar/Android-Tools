# 📱 Android Media Hiding Guide: Dot (`.`) & `.nomedia` Architecture

> Comprehensive Developer & Power-User Notes for Android Storage, Gallery Privacy & MediaStore Indexing.

---

> [!IMPORTANT]
> **मूल उद्देश्य (Core Purpose):**
> Phone की **Gallery / Photos app** को अनचाहे कचरे (AI Stickers, Raw Assets, Private Videos) से 100% साफ़ रखना, जबकि **File Manager** में सारा Data पूरी तरह सुरक्षित, व्यवस्थित और इस्तेमाल के लिए उपलब्ध रहे।

---

## 📑 विषय-सूची (Table of Contents)
1. [Dot (`.`) Hidden File Feature](#1-dot--hidden-file-feature)
2. [`.nomedia` Shield File Feature](#2-nomedia-shield-file-feature)
3. [Quick Comparison (तुलना सारणी)](#3-quick-comparison-तुलना-सारणी)
4. [Android Pro-Tips & Troubleshooting](#4-android-pro-tips--troubleshooting)
5. [Quick Cheatsheet](#5-quick-cheatsheet-शॉर्टकट-सारांश)

---

## 1. Dot (`.`) Hidden File Feature

### 📌 यह क्या है? (Definition)
किसी भी फ़ाइल या फ़ोल्डर के नाम के सबसे आगे बिना किसी स्पेस के एक डॉट यानी फुल-स्टॉप `.` लगा देना।

```text
📁 साधारण फ़ोल्डर   ➜   My_Private_Videos
📁 डॉट वाला फ़ोल्डर ➜   .My_Private_Videos
```

### ⚙️ यह कैसे काम करता है? (Mechanism)
Android का ऑपरेटिंग सिस्टम **Linux Kernel** पर बना है। Linux फ़ाइल सिस्टम का यूनिवर्सल मानक नियम है:
> *"Any file or folder starting with a leading period (`.`) is strictly treated as a hidden system entry."*

जब Android का Media Scanner स्टोरेज को स्कैन करता है, तो वह डॉट `.` से शुरू होने वाले फ़ोल्डर्स को सीधे बाईपास (Skip) कर देता है।

> [!NOTE]
> **सिस्टम व्यवहार (System Behavior):**
> - **Gallery / Photos:** ❌ पूरी तरह अदृश्य (कभी स्कैन नहीं होगा)।
> - **File Manager:** 👁️ सामान्यतः छिपा रहेगा। इसे देखने के लिए File Manager की Settings में जाकर `Show hidden files` चालू करना होता है।

```bash
# Terminal / Bash उदाहरण
mkdir -p /storage/emulated/0/.Private_Vault
mv my_video.mp4 /storage/emulated/0/.Private_Vault/
```

---

## 2. `.nomedia` Shield File Feature

### 📌 यह क्या है? (Definition)
किसी भी साधारण फ़ोल्डर के अंदर रखी जाने वाली **0-Byte की एक खाली फ़ाइल**, जिसका नाम केवल `.nomedia` होता है।

```text
📁 Deepesh_Studio/
└── 📁 Dopamine_Trap/
    ├── 📄 .nomedia              <-- [यह शील्ड मीडिया स्कैनर को ब्लॉक करती है]
    ├── 🎬 Video_Master_9x16.mp4
    ├── 🎙️ Voiceover.wav
    └── 📦 Stickers.zip
```

### ⚙️ यह कैसे काम करता है? (Mechanism)
Android में एक बैकग्राउंड सर्विस चलती है जिसे **`MediaStore` (Android Media Scanner)** कहते हैं। इसका काम पूरे फोन में नए मीडिया (JPG, PNG, MP4, MP3) को ढूँढकर Gallery और Music Player के SQLite डेटाबेस में रजिस्टर करना होता है।

जब Media Scanner किसी फ़ोल्डर में प्रवेश करता है और उसे वहाँ `.nomedia` फ़ाइल मिलती है:
1. वह उस फ़ोल्डर की स्कैनिंग तुरंत रोक देता है।
2. वह उस फ़ोल्डर के अंदर मौजूद सभी Sub-folders को भी गैलरी में जोड़ने से मना कर देता है।

> [!TIP]
> **सबसे बड़ा फ़ायदा (Key Advantage):**
> `.nomedia` फ़ोल्डर का नाम साधारण रखता है। इसलिए यह **File Manager में हमेशा 100% साफ़-साफ़ दिखता रहता है**, लेकिन Gallery इसे कभी छू भी नहीं पाती!

---

## 3. Quick Comparison (तुलना सारणी)

| फ़ीचर (Feature) | Dot (`.`) फ़ीचर | `.nomedia` फ़ाइल फ़ीचर |
| :--- | :--- | :--- |
| **लागू करने का तरीका** | फ़ोल्डर के नाम के आगे डॉट लगाना (`.MyFolder`) | फ़ोल्डर के अंदर खाली फ़ाइल रखना (`.nomedia`) |
| **Gallery में दिखेगा?** | ❌ कभी नहीं (100% Blocked) | ❌ कभी नहीं (100% Blocked) |
| **File Manager में दिखेगा?** | 👁️ केवल `Show Hidden Files` ऑन करने पर | ✅ हमेशा सामान्य रूप से साफ़-साफ़ दिखेगा |
| **Sub-folders पर असर** | अंदर के सभी सब-फ़ोल्डर्स भी छिप जाते हैं | अंदर के सभी सब-फ़ोल्डर्स भी गैलरी से छिप जाते हैं |
| **फ़ाइलों की सुरक्षा** | 100% सुरक्षित (Original Quality) | 100% सुरक्षित (Original Quality) |
| **सर्वश्रेष्ठ उपयोग (Best For)** | पर्सनल सीक्रेट डेटा / सिस्टम फ़ाइलें | वीडियो प्रोजेक्ट्स, स्टिकर्स, रॉ इमेज व आर्काइव |

---

## 4. Android Pro-Tips & Troubleshooting

### ⚠️ समस्या: `.nomedia` डालने के बाद भी पुरानी फ़ाइलें Gallery में क्यों दिखती हैं?
> [!WARNING]
> **कारण (Root Cause):**
> अगर किसी फ़ोल्डर की फ़ाइलें `.nomedia` डालने से पहले ही गैलरी में रजिस्टर हो चुकी थीं, तो Android MediaStore अपने SQLite डेटाबेस में उस पुराने रिकॉर्ड को तब तक बनाए रखता है जब तक उसे रिफ्रेश न किया जाए।

### 🛠️ 2-सेकंड समाधान: "Rename-and-Restore" ट्रिक
जब किसी पुराने फ़ोल्डर में `.nomedia` काम न करे, तो यह जादुई ट्रिक अपनाएँ:
1. File Manager में उस फ़ोल्डर का नाम बदलकर कुछ भी कर दें (जैसे: `Instagram` ➜ `Instagram_Temp`)।
2. इससे Android का पुराना डेटाबेस टूट जाता है और गैलरी से फ़ाइलें तुरंत हट जाती हैं।
3. अब फ़ोल्डर का नाम वापस वही पुराना कर दें (`Instagram_Temp` ➜ `Instagram`)।
4. चूँकि अब `.nomedia` पहले से अंदर मौजूद है, गैलरी इसे दोबारा कभी स्कैन नहीं करेगी!

- [x] `.nomedia` फ़ाइल हमेशा फ़ोल्डर के अंदर रखें।
- [x] नया फ़ोल्डर बनाते ही शुरुआत में `.nomedia` डाल दें ताकि डेटाबेस में पुराना रिकॉर्ड बने ही नहीं।
- [x] ढेरों फ़ोटो/स्टिकर्स को खुले रखने के बजाय `.zip` आर्काइव में रखें।

---

## 5. Quick Cheatsheet (शॉर्टकट सारांश)

```text
┌─────────────────────────────────────────────────────────────┐
│                      ANDROID MEDIA SHIELD                   │
├──────────────────────────┬──────────────────────────────────┤
│ अगर File Manager +       │  फ़ोल्डर के नाम के आगे '.' लगाएँ │
│ Gallery दोनों से छिपाना  │  उदाहरण: .SecretFolder           │
│ हो                       │                                  │
├──────────────────────────┼──────────────────────────────────┤
│ अगर File Manager में     │  फ़ोल्डर के अंदर '.nomedia'      │
│ देखना हो, पर Gallery में │  फ़ाइल कॉपी करें                 │
│ नहीं                     │                                  │
└──────────────────────────┴──────────────────────────────────┘
```

---

## 👤 Maintainer
- Curated & Maintained by [@Satyenderparihar](https://github.com/Satyenderparihar)
