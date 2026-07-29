# 🚀 [Tips Hindawi](https://www.tipshindawi.com/) Challenge (June–July) 2026

> 🏆 This repository is my official submission for the [ **Tips Hindawi** ](https://www.tipshindawi.com/) **Challenge (June–July) 2026**.

## 👤 Participant

| Field            | Value                                |
| ---------------- | ------------------------------------ |
| Full Name        | Mariam Essam                         |
| Project Name     | Legal Contract Risk Analyzer (المساعد القانوني الذكي لتحليل العقود) |
| GitHub Username  | 01097270331                          |
| Challenge Batch  | June–July 2026                       |
| Training Program | Large Language Models (LLMs) Program |
| Organization     | [**Edrak for Ai**](https://edrak4ai.com/en)   |

---

# 📖 Project Overview

نظام ذكاء اصطناعي يحلل العقود العربية (إيجار، عمل، توريد) تلقائيًا ويكتشف البنود المخالفة للقانون المصري. يقوم المستخدم برفع عقد (PDF, TXT, أو DOCX)، ويقوم النظام بـ:
1. تصنيف نوع العقد تلقائيًا
2. تقسيم العقد إلى بنود
3. مقارنة كل بند بقاعدة معرفة قانونية مبسطة عبر تقنية RAG (Retrieval-Augmented Generation)
4. كشف البنود الخطرة أو المخالفة للقانون مع شرح السبب
5. حساب درجة خطورة إجمالية للعقد (Risk Score)
6. اقتراح صياغة بديلة أعدل للبنود الخطرة

المشروع مبني بالكامل على بيانات مُعدّة خصيصًا (6 عقود بصياغة واقعية + قاعدة معرفة قانونية مبسطة + ملف تقييم Ground Truth)، مما يسمح بقياس دقة النظام فعليًا (Precision/Recall/F1) بدلاً من التقييم الذاتي فقط.

---

# ✨ Features

* تصنيف نوع العقد تلقائيًا (نظام هجين: كلمات مفتاحية + Zero-shot Classification)
* استخراج نص من PDF / DOCX / TXT تلقائيًا
* قاعدة معرفة قانونية بتقنية RAG (Embeddings + FAISS) لقوانين الإيجار والعمل والعقود التجارية المصرية
* كشف البنود الخطرة لكل بند على حدة مع شرح قانوني للسبب (باستخدام Chaining + Output Parser بصيغة JSON)
* حساب درجة خطورة إجمالية للعقد (Risk Score) بصيغة نسبية
* اقتراح صياغة بديلة أعدل للبنود الخطرة
* واجهة مستخدم تفاعلية (Gradio) لرفع أي عقد وتحليله مباشرة
* تقييم كمي للنظام مقابل بيانات موسومة (Ground Truth Evaluation)

---

# 🛠️ Technologies Used

* **Python 3**
* **Transformers (Hugging Face)** — للتصنيف (`facebook/bart-large-mnli`) والتوليد (`Qwen/Qwen2.5-1.5B-Instruct`)
* **Sentence-Transformers** — لتوليد الـ Embeddings (`paraphrase-multilingual-MiniLM-L12-v2`)
* **FAISS** — لفهرسة واسترجاع المستندات (RAG)
* **PyPDF / python-docx** — لاستخراج النصوص من ملفات PDF و Word
* **Gradio** — لبناء الواجهة التفاعلية
* **Pandas / NumPy** — لمعالجة البيانات
* **Kaggle Notebooks (GPU)** — بيئة التطوير والتشغيل

---

# ⚙️ Installation

```bash
pip install "transformers<5" sentence-transformers faiss-cpu torch accelerate gradio pypdf python-docx
```

هيكل المشروع:

legal-contract-risk-analyzer/
├── README.md
├── notebooks/
│ └── contract_risk_analyzer.ipynb
└── data/
├── contracts/ # 6 عقود (سليمة + بها مخالفات)
├── laws/ # مرجع قانوني مبسط (إيجار، عمل، عقود تجارية)
└── labels/
└── risk_labels.json # الحقيقة الأرضية (Ground Truth) للتقييم

المشروع مبني ليعمل على Kaggle Notebooks (مع تفعيل GPU). لتشغيله:
1. ارفع مجلد `data/` بالكامل (بمحتوياته: contracts, laws, labels) كـ Kaggle Dataset
2. افتح النوتبوك `notebooks/contract_risk_analyzer.ipynb`
3. اربط الداتاست بالنوتبوك من "+ Add Input"
4. عدّل مسار `DATA_DIR` في أول خلية ليطابق مسار الداتاست الفعلي على حسابك (يظهر عادة كـ `/kaggle/input/datasets/<username>/<dataset-name>`)
5. شغّل الخلايا بالترتيب

---

# 🚀 Usage

1. افتح رابط الواجهة (Gradio) الذي يظهر بعد تشغيل آخر خلية في النوتبوك
2. ارفع ملف العقد (PDF, TXT, أو DOCX)
3. اضغط "حلل العقد"
4. استعرض النتيجة: نوع العقد، درجة الخطورة الإجمالية، وتحليل تفصيلي لكل بند مع السبب والصياغة البديلة المقترحة
5. حمّل تقرير التحليل الكامل بصيغة JSON

---

# 📸 Demo

Screen Recording 2026-07-27 221914.mp4

---

# 📈 Results

تم تقييم النظام على 6 عقود موسومة (Ground Truth) موزعة بين إيجار وعمل وتوريد، بإجمالي 19 بندًا خطرًا حقيقيًا موزعة عليها. تم استخدام مقياس **Micro-averaged** (يجمّع كل البنود من كل العقود قبل حساب المقياس) لأنه يعطي صورة أعدل لأداء النظام الكلي، بدلاً من متوسط بسيط لكل عقد على حدة قد يُعاقب بشدة أي إيجابية كاذبة واحدة في عقد سليم بالكامل.

| المقياس | القيمة |
|---|---|
| Precision (Micro) | 0.62 |
| Recall (Micro) | 0.79 |
| F1-Score (Micro) | 0.70 |
| البنود المكتشفة صحيحًا (TP) | 15 من 19 |
| إيجابيات كاذبة (FP) | 9 |
| سلبيات كاذبة فائتة (FN) | 4 |

كما تم اختبار النظام على عقود جديدة كليًا (إيجار وعمل) لم تشارك في بناء المعرفة القانونية، وأظهر قدرة جيدة على التعميم (Generalization) في كشف البنود التعسفية مثل حق الفسخ الأحادي والتنازل عن حق التقاضي، حتى مع اختلاف الصياغة اللغوية عن أمثلة التدريب.

### أهم تحسينين رفعا الدقة بشكل ملحوظ
1. **فلترة قاعدة المعرفة القانونية (RAG) حسب نوع العقد المكتشف** بدلاً من البحث في كل القوانين معًا — قلّل الخلط بين قانون الإيجار وقانون العمل بشكل كبير.
2. **شبكة أمان بالكلمات المفتاحية (Rule-Based Safety Net)** تكتشف عبارات مخالفة معروفة (كالتنازل عن حق التقاضي) بغض النظر عن رد النموذج، مما رفع الـ Recall بشكل ملحوظ.

### القيود الحالية (Known Limitations)
النموذج المستخدم محليًا (`Qwen2.5-1.5B-Instruct`) هو نموذج صغير نسبيًا لتوفير التشغيل على GPU محدود الموارد، وهو أحيانًا يُنتج تفسيرات غير دقيقة (إيجابيات كاذبة) خصوصًا في البنود التي تحتوي غموضًا لغويًا. تحسين هذا مستقبلًا ممكن عبر نموذج أكبر أو Fine-tuning مخصص (انظر قسم Future Improvements).

---

# 🔮 Future Improvements

* مقارنة أداء Fine-tuning مقابل RAG على نفس مهمة كشف البنود الخطرة
* تطبيق Quantization على نموذج التوليد لتقليل زمن الاستجابة وحجم النموذج
* دعم مقارنة نسختين من نفس العقد (Diff) لتوضيح التغييرات
* إضافة شات تفاعلي (Follow-up Q&A) بعد التحليل
* دعم تحويل الملخص إلى صوت (Text-to-Speech) لسهولة الوصول
* توسيع قاعدة البيانات لتغطية عقود شراكة، توكيل، وبيع عقارات

---

# 📚 About the Challenge

This project was developed as part of the [**Tips Hindawi**](https://www.tipshindawi.com/) **Challenge (June–July) 2026**.

[Tips Hindawi](https://www.tipshindawi.com/) is the internships department of [**Edrak for Ai**](https://edrak4ai.com/en), and the challenge encourages participants to build real-world projects, apply practical skills, and showcase their work through GitHub.

For more information about the challenge, training programs, and upcoming batches, visit the official [Tips Hindawi](https://www.tipshindawi.com/) website.

---

# 📄 License

This project is shared for educational and portfolio purposes.

---

# ⚠️ Disclaimer

الملخصات القانونية المستخدمة في هذا المشروع مبسطة لأغراض تعليمية وتجريبية فقط، وليست بديلاً عن استشارة محامٍ مختص. العقود المستخدمة في التدريب والتقييم مكتوبة خصيصًا لهذا المشروع ولا تمثل عقودًا حقيقية لأي طرف.
