# مشروع التسويق المصرفي — التنبؤ بالاشتراك في الودائع لأجل

مشروع جماعي لمقرر **CSE352 – Data Science** يطبّق مراحل تحليل البيانات وبناء نماذج تصنيف للتنبؤ بما إذا كان العميل سيشترك في وديعة لأجل بعد حملة تسويقية مصرفية.

> **الهدف:** الاستفادة من بيانات الحملات السابقة لفهم العملاء وتحسين استهداف الحملات. النتائج تعليمية وليست توصية تشغيلية أو قرارًا ائتمانيًا.

## الملفات

| الملف | الوصف |
|---|---|
| [`bank_marketing_project.ipynb`](bank_marketing_project.ipynb) | دفتر Jupyter: الاستكشاف، التنظيف، تجهيز الخصائص، وبناء النماذج وتقييمها. |
| [`bank-full.csv`](bank-full.csv) | بيانات Bank Marketing الكاملة اللازمة لتشغيل الدفتر؛ مفصولة بفاصلة منقوطة. |
| [`presentation.pptx`](presentation.pptx) | نسخة PowerPoint من العرض التقديمي المرفق. |
| [`docs/course_assignment.pdf`](docs/course_assignment.pdf) | ملف متطلبات المشروع للمقرر. |

## روابط العرض والدفتر

- [مشاهدة العرض على Canva](https://www.canva.com/design/DAG80w25nWk/yRy2_kMG-sbzizxxhf9C-A/view?utm_content=DAG80w25nWk&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=h8d16597c7a)
- [فتح نسخة Google Colab](https://colab.research.google.com/drive/1KeQcz1L9QXra-GVRTcy8cWQCwmeInPSM?usp=sharing)

## البيانات

تتكون مجموعة البيانات من **45,211 سجلًا و17 عمودًا**، والهدف `y` يحدد ما إذا كان العميل قد اشترك (`yes`) أو لم يشترك (`no`). نسبة فئة الاشتراك في البيانات نحو **11.7%**، لذلك يجب مراعاة عدم توازن الفئات عند قراءة الدقة ومقاييس التقييم.

المصدر الأصلي: [UCI Machine Learning Repository — Bank Marketing](https://archive.ics.uci.edu/dataset/222/bank+marketing). أُدرج ملف `bank-full.csv` هنا لتسهيل تشغيل الدفتر دون تنزيله يدويًا.

## التشغيل محليًا

يتطلب Python 3.10 أو أحدث. من مجلد المشروع:

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook bank_marketing_project.ipynb
```

تأكد من وجود `bank-full.csv` بجانب الدفتر، ثم شغّل الخلايا بالترتيب. يقرأ الدفتر الملف باستخدام `pandas.read_csv('bank-full.csv', sep=';')`.

## منهجية المشروع

1. **الاستكشاف (EDA):** إحصاءات وصفية، توزيعات ورسوم، علاقات بين الخصائص، وتحليل المتغير المستهدف.
2. **تنظيف البيانات:** فحص القيم المفقودة والتكرارات والقيم الشاذة، وتحويل المتغيرات الفئوية.
3. **تجهيز الخصائص:** `StandardScaler` للخصائص الرقمية و`OneHotEncoder` للخصائص الفئوية ضمن `ColumnTransformer` و`Pipeline`.
4. **النمذجة والتقييم:** مقارنة الانحدار اللوجستي و`RandomForestClassifier` باستخدام تقسيم تدريب/اختبار مع `random_state=42` ومقاييس التصنيف ومنحنى ROC/AUC.

## النتائج المحفوظة في الدفتر والعرض

| النموذج | الدقة (Accuracy) | استدعاء فئة الاشتراك (Recall – yes) | ملاحظات |
|---|---:|---:|---|
| Logistic Regression | 89.33% | 18% | دقة كلية أعلى، لكنه يفوّت نسبة كبيرة من العملاء المشتركين. |
| Random Forest | 81.71% | 61% | يلتقط عددًا أكبر من المشتركين؛ ودرجة F1 الموزونة المعروضة 0.84. |

بسبب عدم توازن الفئات، لا تكفي الدقة وحدها لاختيار النموذج؛ ينبغي النظر خصوصًا إلى استدعاء وفئة F1 الخاصة بـ`yes` بحسب هدف الحملة.

## ملاحظات لإعادة الإنتاج

- الدفتر محفوظ مع مخرجات سابقة. أعد تشغيل جميع الخلايا في بيئتك للتحقق من النتائج باستخدام نسخ المكتبات المتاحة لديك.
- يوجد اختلاف بين بعض النصوص التوضيحية والتنفيذ: قسم التنظيف يذكر في وصفه قصّ القيم الشاذة (Winsorization)، بينما الخلايا التنفيذية تحسب القيم الشاذة وتُبقيها. راجع هذه النقطة قبل اعتبار المعالجة نهائية.
- ملف العرض موجود بصيغة PowerPoint، ويمكن مشاهدة نسخة Canva من الرابط أعلاه.

## أعضاء الفريق

- Omar Aljerbi
- Faraj Alarabi
- Abd Albari Abd Alsamad
- Ali Bie

---

**English summary:** An end-to-end CSE352 data-science project using the UCI Bank Marketing dataset to explore customer campaign data, prepare features with scikit-learn pipelines, and compare logistic regression with random forest for term-deposit subscription prediction.
