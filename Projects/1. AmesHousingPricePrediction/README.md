# 📈 Predictive Modeling in Real Estate (Ames Housing)

Pada proyek ini, digunakan model regresi untuk memprediksi harga jual rumah (`SalePrice`) berdasarkan fitur-fitur seperti luas bangunan (`GrLivArea`), jumlah kamar (`TotRmsAbvGrd`), lokasi (`Neighborhood`), usia properti (`YearBuilt`), dst. menggunakan dataset **Ames Housing**.

Setelah training berbagai model, kita mengevaluasi performanya menggunakan metrik:

## 🔍 Metrik Evaluasi

| Model             | MAE   | RMSE  | R²   |
|-------------------|-------|-------|------|
| CatBoost          | rendah| rendah| tinggi|
| GradientBoosting  | rendah| rendah| tinggi|
| LightGBM          | rendah| rendah| tinggi|
| XGBoost           | rendah| rendah| tinggi|
| RandomForest      | rendah| rendah| tinggi|
| Lasso             | agak tinggi| agak tinggi| sedang|
| Ridge             | agak tinggi| agak tinggi| sedang|
| LinearRegression  | agak tinggi| agak tinggi| sedang|
| DecisionTree      | sangat tinggi| sangat tinggi| rendah|

_(Nilai persis dapat dilihat pada grafik MAE, RMSE, dan R² yang telah dibuat.)_

---

### 📏 Mean Absolute Error (MAE)

MAE mengukur rata-rata selisih absolut antara prediksi dengan nilai aktual.  
**Interpretasi:**  
> "Rata-rata kesalahan prediksi harga rumah sekitar beberapa ribu dolar."

MAE dipilih untuk melihat seberapa besar kesalahan *praktis* di unit harga rumah.

---

### ⚡ Root Mean Squared Error (RMSE)

RMSE mengkuadratkan error sebelum dihitung rata-ratanya, lalu diakar. Ini memperbesar penalti untuk error yang besar.  
**Interpretasi:**  
> "Model dihukum lebih berat jika melakukan kesalahan besar (outlier)."

RMSE digunakan ketika kita ingin sangat berhati-hati terhadap prediksi yang salah besar.

---

### 🎯 R² Score

R² menunjukkan seberapa besar variasi `SalePrice` bisa dijelaskan oleh model dibandingkan hanya menggunakan rata-rata.  
**Interpretasi:**  
> "Model ini menjelaskan sekitar X% variasi harga rumah di Ames."

Semakin mendekati 1, semakin baik model kita.

---

## ✨ Kesimpulan

- **CatBoost**, **GradientBoosting**, dan **LightGBM** menunjukkan performa terbaik dilihat dari MAE, RMSE, dan R² yang tinggi.
- **DecisionTree** overfitting pada training set dan gagal generalisasi di data test.
- MAE rendah → prediksi rata-rata cukup akurat.
- RMSE moderat → model lumayan tahan terhadap outlier besar.
- R² tinggi → model menjelaskan variasi harga rumah dengan baik.

> 📌 **Next Step:**  
> Menambahkan fine-tuning hyperparameter untuk meningkatkan akurasi model lebih lanjut.


