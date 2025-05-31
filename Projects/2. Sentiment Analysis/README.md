# 🧠 Sentiment Analysis Capres-Cawapres 2024

Proyek ini bertujuan untuk membangun sistem klasifikasi sentimen publik terhadap pasangan Capres-Cawapres 2024 dari data Twitter. Model dikembangkan secara bertahap: dari baseline (Naive Bayes, Logistic Regression), deep learning (LSTM, GRU), hingga transformer-based model (IndoBERTweet).

---

## 📂 Struktur Direktori

```
.
├── README.md
├── dataset
│   └── Dataset mentah & hasil pembersihan untuk tiap model
├── models
│   └── Semua model tersimpan (pkl, h5) + FastText + IndoBERTweet
├── notebooks
│   └── Eksplorasi, pelatihan, tuning & deployment tiap pendekatan
├── pretrained
│   └── cc.id.300.vec (FastText Bahasa Indonesia)
```

---

## 🔁 Flow Modeling

1. **Data Preparation**
   - Pembersihan teks, normalisasi, tokenisasi
   - Versi berbeda disiapkan untuk baseline dan deep learning

2. **Baseline Models**
   - `Logistic Regression`, `Naive Bayes` dengan `TF-IDF`
   - Disimpan sebagai `.pkl`, di-tune dengan `GridSearchCV`

3. **Deep Learning (LSTM/GRU)**
   - Versi awal tanpa FastText
   - Versi lanjutan pakai FastText embedding (cc.id.300.vec)
   - Disimpan sebagai `.h5` dan `.pkl`

4. **Transformer**
   - IndoBERTweet fine-tuning via HuggingFace
   - Evaluasi: accuracy, F1, confusion matrix

5. **Deployment**
   - Notebook demo

---

## 💻 Teknologi

- Python 3.10
- Scikit-Learn
- TensorFlow / Keras
- HuggingFace Transformers
- Gensim (FastText)
- Matplotlib & Seaborn

---

## 📊 Evaluasi Model

| Model               | Accuracy | F1 Macro |
|---------------------|----------|----------|
| Naive Bayes         | ~0.61    | ~0.61    |
| Logistic Regression | ~0.60    | ~0.60    |
| LSTM (tanpa FT)     | ~0.56    | ~0.55    |
| GRU (tanpa FT)      | ~0.57    | ~0.57    |
| LSTM + FastText     | ✅ 0.63   | ✅ 0.62   |
| GRU + FastText      | ✅ 0.60   | ✅ 0.60   |
| IndoBERTweet        | ✅ ~0.67  | ✅ ~0.67  |

---
