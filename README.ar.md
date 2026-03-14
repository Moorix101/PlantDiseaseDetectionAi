<div align="center">

<a href="README.md"><img src="https://img.shields.io/badge/🇬🇧_English-555?style=for-the-badge" /></a>
<a href="README.fr.md"><img src="https://img.shields.io/badge/🇫🇷_Français-555?style=for-the-badge" /></a>
<a href="README.ar.md"><img src="https://img.shields.io/badge/🇲🇦_العربية-2d6a2d?style=for-the-badge" /></a>

<br/><br/>

<img src="assets/performance_comparison.png" width="720"/>

<h1>🌿 PlantDoc AI System</h1>

<p dir="rtl">تشخيص تلقائي لأمراض أوراق النباتات — SVM+LBP مقابل CNN MobileNetV2، مع واجهة ويب للتشخيص الفوري.</p>

**DUT Génie Informatique · Module : Python / AI · 2025–2026**

*عبد الرحمان أبو طالب · أنس المريحي · محمد بزيز*
*تحت إشراف الأستاذ Al Semaa — EST سيدي بنور، جامعة شعيب الدكالي*

</div>

---

<div dir="rtl">

## نظرة عامة

يقوم هذا المشروع ببناء ومقارنة نموذجَين من نماذج التعلم الآلي لتصنيف أمراض أوراق النباتات، باستخدام مجموعة البيانات [PlantVillage](https://www.kaggle.com/datasets/abdallahalidev/plantvillage-dataset) المُصفَّاة على نوعَي **الطماطم** و**التفاح** (14 صنفاً). يُنشر النموذج الأفضل أداءً بعد ذلك كـ REST API ويُستهلك من واجهة ويب أحادية الصفحة.

| النموذج | الأسلوب | دقة التحقق |
|---|---|---|
| SVM | خصائص LBP (مدرّج تكراري 26 بُعداً) | 34.77% |
| **CNN** | MobileNetV2 + التعلم بالنقل (5 دورات) | **91.48%** |

---

## هيكل المستودع

</div>

```
PlantDoc-AI/
├── colab/
│   ├── plantdoc_pipeline.ipynb   ← دفتر Google Colab الكامل
│   └── plantdoc_pipeline.py      ← جميع الخلايا مدمجة (للمرجعية)
├── web/
│   └── index.html                ← واجهة PlantVision أحادية الصفحة
├── report/
│   └── PlantDoc_AI_Report.pdf
├── presentation/
│   └── PlantDoc_AI_Slides.pptx
├── assets/
│   └── performance_comparison.png
└── README.md
```

<div dir="rtl">

---

## طريقة التشغيل

> كل شيء يعمل على **Google Colab** — لا حاجة لأي تثبيت محلي.

**1 — فتح الدفتر**
ارفع `colab/plantdoc_pipeline.ipynb` إلى [Google Colab](https://colab.research.google.com/) ونفّذ الخلايا بالترتيب.

**2 — الخلايا بإيجاز**

| الخلية | المهمة |
|---|---|
| 1 | ربط Google Drive · تنزيل مجموعة البيانات عبر Kaggle API |
| 2 | تصفية مجلدات الطماطم/التفاح · بناء `ImageDataGenerator` |
| 3 | استخراج خصائص LBP · تدريب نموذج SVM وحفظه |
| 4 | بناء CNN MobileNetV2 · 5 دورات تدريب · حفظ ملف `.h5` |
| 5 | رسم منحنيات الدقة · مقارنة SVM مقابل CNN |
| 6 | تشغيل خادم Flask + نفق ngrok → نسخ الرابط |

**3 — استخدام واجهة الويب**
1. افتح `web/index.html` في أي متصفح
2. الصق رابط ngrok في حقل **COLAB URL** أعلى الصفحة
3. أسقط صورة `.jpg` أو `.png` لورقة نبات ← **Analyze Leaf**

> ⚠️ يتغير رابط ngrok عند كل إعادة تشغيل لجلسة Colab.

---

## التقنيات المستخدمة

`Python` · `TensorFlow / Keras` · `scikit-learn` · `scikit-image` · `OpenCV` · `Flask` · `pyngrok` · `Matplotlib` · `Google Colab` · `HTML / CSS / JS`

---

## النتائج الرئيسية

- **فارق +56.7 نقطة** بين SVM (34.77%) وCNN (91.48%)
- تم تدريب CNN في ~10–20 دقيقة على GPU T4 المجاني بـ **17,934 معامل قابل للتدريب** فقط
- يُتيح التعلم بالنقل من ImageNet الحصول على دقة عالية في 5 دورات فقط
- دقة التحقق قريبة جداً من دقة التدريب — لا إفراط في التخصيص

---

## ملاحظة .gitignore

ملفات النماذج (`.h5`، `.pkl`) ومجلدات البيانات الخام مستبعدة من المستودع لكبر حجمها. يمكن إعادة توليدها بتشغيل الدفتر من الخلية 1.

</div>