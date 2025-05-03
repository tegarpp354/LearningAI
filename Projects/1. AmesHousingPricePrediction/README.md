# 📈 Predictive Modeling in Real Estate (Ames Housing)

Pada proyek ini, digunakan model regresi untuk memprediksi harga jual rumah (`SalePrice`) berdasarkan fitur-fitur seperti luas bangunan (`GrLivArea`), jumlah kamar (`TotRmsAbvGrd`), lokasi (`Neighborhood`), usia properti (`YearBuilt`), dst. menggunakan dataset **Ames Housing**.

Dataset ini mencakup berbagai atribut properti seperti:
- Luas bangunan (`GrLivArea`)
- Jumlah kamar (`TotRmsAbvGrd`)
- Lokasi (`Neighborhood`)
- Tahun dibangun (`YearBuilt`)
- Kualitas material, tipe garasi, dan lainnya.

## 📁 Struktur Folder
├── AmesHousing.csv # Dataset utama
├── HousePricingPrediction.ipynb # Notebook utama proyek
├── environment.yml # File environment Conda
├── README.md # Dokumentasi proyek ini
├── best_model_catboost.pkl # Model terbaik final (CatBoost)
├── best_model_randomsearchcv_catboost.pkl # Model terbaik dari tuning RandomizedSearchCV
├── catboost_info/ # Output log CatBoost
└── coda.ipynb # Notebook catatan/eksperimen tambahan

## ⚙️ Tahapan Proyek

1. **Eksplorasi dan Praproses Data**
   - Analisis distribusi fitur
   - Menangani missing values
   - Encoding fitur kategorikal (Ordinal, Nominal, Binary)
   - Skewness correction

2. **Modeling Awal (tanpa Scaling & Tuning)**
   - Melatih berbagai model regresi:
     - LinearRegression, Ridge, Lasso
     - DecisionTree, RandomForest
     - GradientBoosting, XGBoost, LightGBM, CatBoost

   **Hasil Evaluasi Awal:**

   | Model             | MAE      | RMSE     | R²   |
   |-------------------|----------|----------|------|
   | CatBoost          | 14279.37 | 23617.23 | 0.93 |
   | GradientBoosting  | 16489.34 | 26423.67 | 0.91 |
   | XGBoost           | 17125.47 | 28244.53 | 0.90 |
   | LightGBM          | 16671.42 | 28937.96 | 0.90 |
   | RandomForest      | 17408.02 | 29641.50 | 0.89 |
   | Ridge             | 18732.10 | 30940.62 | 0.88 |
   | Lasso             | 18357.04 | 30944.52 | 0.88 |
   | LinearRegression  | 18349.39 | 30987.93 | 0.88 |
   | DecisionTree      | 25203.64 | 38032.05 | 0.82 |

3. **Scaling Data**
   - Model pohon (tree-based) tidak terpengaruh signifikan
   - Model linear menunjukkan hasil lebih stabil setelah scaling

   **Hasil Setelah Scaling:**

   | Model             | MAE      | RMSE     | R²   |
   |-------------------|----------|----------|------|
   | CatBoost          | 13639.84 | 23125.97 | 0.93 |
   | XGBoost           | 15556.92 | 24497.82 | 0.93 |
   | GradientBoosting  | 15016.91 | 25481.15 | 0.92 |
   | LightGBM          | 15111.08 | 27215.24 | 0.91 |
   | RandomForest      | 15827.26 | 26800.94 | 0.91 |
   | Ridge             | 18746.01 | 30943.37 | 0.88 |
   | Lasso             | 18380.92 | 30974.81 | 0.88 |
   | LinearRegression  | 18384.56 | 31043.54 | 0.88 |
   | DecisionTree      | 24056.92 | 36248.77 | 0.84 |

4. **Hyperparameter Tuning (3 Metode)**
   - Menggunakan:  
     ✅ `GridSearchCV`  
     ✅ `RandomizedSearchCV`  
     ✅ `BayesSearchCV` (scikit-optimize)

   - Model dituning dengan cross-validation (`KFold(n_splits=5)`), dengan hasil performa terbaik ditentukan berdasarkan **RMSE terendah**.

   **Top Performers Setelah Tuning:**

     | Rank | Tuning Method      | Model            | MAE      | RMSE         | R²   |
     | ---- | ------------------ | ---------------- | -------- | ------------ | ---- |
     | 1    | RandomizedSearchCV | CatBoost         | 13684.86 | **23111.24** | 0.93 |
     | 2    | GridSearchCV       | CatBoost         | 13427.96 | 23161.90     | 0.93 |
     | 3    | BayesSearchCV      | CatBoost         | 13692.51 | 23294.07     | 0.93 |
     | 4    | BayesSearchCV      | XGBoost          | 14256.74 | 23414.36     | 0.93 |
     | 5    | GridSearchCV       | XGBoost          | 14515.83 | 24257.77     | 0.93 |

   📦 Model terbaik disimpan dalam format `.pkl` menggunakan `joblib`:
   - `best_model_catboost.pkl` → pipeline CatBoost dengan tuning optimal
   - `best_model_randomsearchcv_catboost.pkl` → versi alternatif dari RandomizedSearchCV

---

## 📊 Metrik Evaluasi

- **MAE (Mean Absolute Error)**  
  Mengukur rata-rata selisih absolut antara prediksi dan data aktual.  
  → Interpretasi praktis: "rata-rata kesalahan prediksi harga rumah sekitar X dollar".

- **RMSE (Root Mean Squared Error)**  
  Penalti lebih besar untuk kesalahan prediksi besar (outliers).  
  Cocok saat kita ingin sangat berhati-hati terhadap outlier.

- **R² (R-squared Score)**  
  Menjelaskan seberapa besar variasi harga rumah yang bisa dijelaskan oleh model dibanding hanya menggunakan rata-rata.

---

## ✅ Kesimpulan Akhir

- 📌 **CatBoost** consistently memberikan performa terbaik dari semua model, baik sebelum maupun sesudah tuning.
- 🔍 **Hyperparameter tuning** signifikan menurunkan MAE pada hampir semua model, terutama ensemble methods.
- 🚀 Model boosting seperti **XGBoost**, **GradientBoosting**, dan **LightGBM** juga menunjukkan performa luar biasa setelah scaling dan tuning.
- 📉 Model linear (Ridge, Lasso) relatif stabil namun performanya tidak sebaik ensemble.
- 🌳 **DecisionTree** tetap underperforming dan cenderung overfit.
- Semua hasil dihasilkan secara **reproducible**, menggunakan pipeline yang dapat disimpan dan di-reload.

---

## 🧪 Environment

File `environment.yml` tersedia untuk memastikan reproducibility proyek ini.  
Untuk membuat environment:

```bash
conda env create -f environment.yml
conda activate house-pricing


