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
| Organization     | [**Edrak for Ai**](https://edrak4ai.com/en)                         |

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

المشروع مبني ليعمل على Kaggle Notebooks (مع تفعيل GPU). لتشغيله:
1. ارفع ملفات البيانات (العقود، القوانين، ملف التقييم) كـ Kaggle Dataset
2. افتح النوتبوك `notebook1da9bd1f92.ipynb`
3. اربط الداتاست بالنوتبوك من "+ Add Input"
4. شغّل الخلايا بالترتيب

---

# 🚀 Usage

1. افتح رابط الواجهة (Gradio) الذي يظهر بعد تشغيل آخر خلية في النوتبوك
2. ارفع ملف العقد (PDF, TXT, أو DOCX)
3. اضغط "حلل العقد"
4. استعرض النتيجة: نوع العقد، درجة الخطورة الإجمالية، وتحليل تفصيلي لكل بند مع السبب والصياغة البديلة المقترحة
5. حمّل تقرير التحليل الكامل بصيغة JSON

---

# 📸 Demo

(أضيفي هنا سكرين شوت من الواجهة وهي شغالة)

---

# 📈 Results

تم تقييم النظام على 6 عقود موسومة (Ground Truth) موزعة بين إيجار وعمل وتوريد:

| المقياس | القيمة |
|---|---|
| Precision | 0.83 |
| Recall | 0.71 |
| F1-Score | 0.77 |

كما تم اختبار النظام على عقد جديد كليًا لم يشارك في بناء المعرفة القانونية، وأظهر قدرة جيدة على التعميم (Generalization) في كشف البنود التعسفية مثل حق الفسخ الأحادي والتنازل عن حق التقاضي.

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
