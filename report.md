# Retail Product Recommendation System Report

## Domain Proyek

Di era digital saat ini, data menjadi aset yang sangat berharga bagi perusahaan, terutama di sektor ritel. Perusahaan retail mengumpulkan berbagai jenis data pelanggan, transaksi, dan produk yang mereka jual. Dengan memanfaatkan data ini secara efektif, perusahaan dapat meningkatkan pengalaman pelanggan, mengoptimalkan penjualan, dan mendorong loyalitas pelanggan. Kepuasan pelanggan yang lebih tinggi akan menghasilkan keuntungan yang lebih tinggi di masa depan, pembelian berulang, dan promosi dari mulut ke mulut yang positif [1]. Salah satu cara untuk mencapai tujuan ini adalah dengan membangun sistem rekomendasi yang dapat memberikan saran produk yang relevan kepada pelanggan berdasarkan perilaku dan preferensi mereka. Sistem rekomendasi ritel sangat penting untuk meningkatkan pengalaman pelanggan dan meningkatkan penjualan dengan memberikan saran produk yang dipersonalisasi berdasarkan data transaksi. Sistem ini memanfaatkan berbagai teknik penggalian data untuk menganalisis perilaku dan preferensi pelanggan, yang bertujuan untuk memprediksi dan merekomendasikan produk yang kemungkinan besar akan dibeli oleh pelanggan.

Salah satu tantangan utama dalam sistem rekomendasi adalah ketika data transaksi pelanggan sangat sedikit atau tidak seimbang. Misalnya, jika seorang pelanggan hanya membeli sedikit produk, atau jika beberapa produk lebih sering dibeli daripada yang lain. Untuk mengatasi masalah ini, para peneliti sedang mengembangkan metode canggih seperti probabilistik dan teknik pengelompokan yang bisa membantu memberikan rekomendasi yang lebih akurat meskipun data yang tersedia terbatas. Salah satu teknik yang sering digunakan dalam sistem rekomendasi adalah Collaborative Filtering, yang berfokus pada menghitung minat atau preferensi pengguna dengan cara mengumpulkan informasi tentang selera pelanggan lain [2]. Teknik ini bekerja dengan membandingkan pengguna atau produk yang serupa, kemudian memprediksi produk yang mungkin disukai oleh pengguna berdasarkan preferensi pengguna lain yang memiliki pola pembelian serupa. Neural Networks atau jaringan saraf tiruan dapat diterapkan untuk meningkatkan teknik Collaborative Filtering. Dengan menggunakan jaringan saraf, model bisa lebih mendalam dalam mempelajari pola-pola yang lebih kompleks dalam data pelanggan dan produk, serta memberikan rekomendasi yang lebih tepat dan personal.

Proyek ini meneliti penggunaan Neural Network dalam Sistem Rekomendasi dengan data ritel. Rekomendasi dibuat agar memberikan saran produk yang tepat.

[1] Kalia, P., Kaur, N., & Singh, T., 2017. Consumer Satisfaction in e-Shopping: An Overview. _Indian Journal of Economics and Development_, 13, pp. 569-576. [https://doi.org/10.5958/2322-0430.2017.00132.9](https://doi.org/10.5958/2322-0430.2017.00132.9).

[2] Iftikhar, A., Ghazanfar, M., Ayub, M., Mehmood, Z., & Maqsood, M., 2020. An Improved Product Recommendation Method for Collaborative Filtering. _IEEE Access_, 8, pp. 123841-123857. [https://doi.org/10.1109/ACCESS.2020.3005953](https://doi.org/10.1109/ACCESS.2020.3005953).

## Business Understanding

### Problem Statements

- Bagaimana cara membangun sistem rekomendasi menggunakan Neural Network yang dapat memberikan saran produk secara akurat dan andal berdasarkan preferensi pelanggan ritel ?

- Bagaimana performa Neural Network dalam memprediksi produk ritel ?

### Goals

- Mengembangkan sistem rekomendasi menggunakan Neural Network yang dapat saran produk untuk pelanggan ritel
- Menggunakan dan melihat performa Neural Network dalam memberikan saran produk pelanggan ritel

### Solution statements

- Melakukan tuning hyperparameter pada kedua model untuk mencapai performa terbaik, dengan tujuan mendapatkan hasil prediksi yang lebih akurat dan konsisten.
- Memberikan evaluasi yang tepat sehingga dapat memberikan rekomendasi model yang dapat membantu produsen wine dalam proses kontrol kualitas produk sebelum dipasarkan.

## Data Understanding

Data yang digunakan dalam proyek ini bersumber dari Kaggle yaitu [Retail Transactional Dataset](https://www.kaggle.com/datasets/bhavikjikadara/retail-transactional-dataset). Dataset ini merupakan data transaksi konsumen bisnis ritel, terdiri dari 30 kolom yang berisikan data kustomer, detail transaksi, informasi produk dan feedback kustomer.

### Variabel-variabel yang digunakan dalam analsis adalah sebagai berikut:

-  **Customer ID**: Id kustomer

-  **Product_Category**: Kategori produk.

-  **Product_Brand**: Merek produk

-  **Product_Type**: Tipe produk

-  **products**: nama produk

-  **Ratings**: Rating konsumen terhadap produk yang dibeli

## Data Exploration and Preparation

### Data Exploration

Dataset terdiri 302009 data, terdiri dari 30 fitur. Untuk membentuk sistem rekomendasi fitur yang dipilih adalah Customer_ID, Product_Category, Product_Brand, Product_Type, products dan Ratings. Berdasarkan eksplorasi data, terdapat 86.740 pelanggan unik dan 318 produk unik dalam dataset. Selain itu, dataset mencakup 5 kategori produk unik, 18 merek produk unik, dan 33 tipe produk unik. Informasi ini memberikan gambaran tentang variasi pelanggan dan produk yang dapat dimanfaatkan untuk mengembangkan sistem rekomendasi yang efektif.
https://drive.google.com/file/d/1Mk-ITlxuKI--Sf3ryCd7TR-sRRveHNxD/view?usp=sharing
![Image Text](http://drive.google.com/uc?export=view&id=1Mk-ITlxuKI--Sf3ryCd7TR-sRRveHNxD)

Data terdiri dari berbagai rentang dan memiliki banyak outliers, maka dari itu perlu dilakukan transformasi agar seluruh data menjadi dalam satu rentang.

  

![Gambar Distribusi target](https://github.com/alfitoptr/Wine-Detection-Using-Tree-ensemble/blob/main/wine/results/distribusi%20target.png?raw=true)

Variabel target yaitu kualitas wine merupakan data dengan rentang kualitas 0 - 10. Namun, hanya terdapat 5 kualitas yang berbeda dalam data, yaitu kualitas 3 - 8. Untuk membuat model yang dapat mendeteksi kualitas wine tidak bisa menggunakan metode klasifikasi dikarenakan belum semua jenis kualitas tercatat, metode yang dapat digunakan yaitu metode regresi dimana model dapat memprediksi data kontinu.

[![Correlation Heatmap](https://github.com/alfitoptr/Wine-Detection-Using-Tree-ensemble/blob/main/wine/results/corr.png?raw=true)](https://github.com/alfitoptr/Wine-Detection-Using-Tree-ensemble/blob/main/wine/results/corr.png)

Terlihat dari gambar heatmap korelasi, variabel yang dianalisis memiliki korelasi satu sama lain. Walaupun tidak banyak yang memiliki nilai korelasi tinggi, hal ini menunjukkan adanya hubungan yang mungkin signifikan di antara beberapa variabel, yang bisa memberikan wawasan tentang interaksi mereka dalam konteks model yang dibangun.

  
### Data Preprocessing

Data dibagi menjadi 80% untuk data pelatihan dan 20% untuk data pengujian. Setelah itu, data juga ditransformasi menggunakan `StandardScaler` agar rentang data menjadi seimbang.

```python

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

scaler = StandardScaler()

X_train_scaled = scaler.fit_transform(X_train)

X_test_scaled = scaler.fit_transform(X_test)

```
  
## Modeling
 

Data dilatih terhadap dua model yaitu Random Forest Regressor (RFR) dan Extreeme Gradient Boosting Regressor (XGBR). Data pertama dilatih menggunakan parameter defaulth untuk dilihat performanya

  

Model pertama yang dianalisis adalah RFR. Langkah prediksi RFR dapat dilihat dalam gambar berikut:

![Random Forest](https://images.squarespace-cdn.com/content/v1/5acbdd3a25bf024c12f4c8b4/1595966947020-S5K62U9VB451NX3KOA9C/Random+Forest.jpg)

RFR bekerja dengan membentuk kumpulan pohon prediksi yang disebut "hutan." Setiap pohon dibangun dari data yang ada, dan masing-masing pohon memberikan hasil prediksinya sendiri. Dalam kasus regresi, prediksi akhir diperoleh dengan menghitung rata-rata dari seluruh prediksi pohon. Sementara itu, dalam kasus klasifikasi, prediksi akhir ditentukan melalui voting, dengan memilih kelas yang paling sering diprediksi oleh pohon-pohon tersebut. Berikut merupakan code untuk RFR dengan parameter defaulth:
```python

rf = RandomForestRegressor(random_state=42)

rf.fit(X_train_scaled, y_train)

y_pred = rf.predict(X_test_scaled)

```
  
Untuk mendapatkan performa terbaik model akan dilakukan tuning terhadap beberapa parameter berikut:


-  **n_estimators**: Ini adalah jumlah pohon dalam hutan. Semakin banyak pohon, semakin stabil dan akurat hasil model karena rata-rata dari lebih banyak pohon cenderung mengurangi variabilitas. Rentang nilai yang dipilih (100 hingga 1000) memberikan variasi yang cukup untuk menemukan keseimbangan antara kinerja dan efisiensi.

-  **max_depth**: Ini menentukan kedalaman maksimum setiap pohon dalam hutan. Semakin dalam pohon, semakin kompleks model, sehingga dapat menimbulkan overfitting (terlalu menyesuaikan data pelatihan). `None` (artinya tanpa batas) memungkinkan pohon berkembang penuh, sedangkan rentang dari 5 hingga 100 memberikan fleksibilitas untuk pohon yang tidak terlalu dalam dan tidak terlalu kompleks.

-  **min_samples_split**: Ini adalah jumlah minimum sampel yang dibutuhkan untuk membagi node. Semakin tinggi nilai ini, semakin banyak data yang diperlukan untuk membagi node, sehingga pohon menjadi lebih sederhana dan mengurangi risiko overfitting. Nilai 2, 3, dan 5 dipilih untuk memberikan keseimbangan antara kompleksitas dan generalisasi.

-  **min_samples_leaf**: Ini adalah jumlah minimum sampel yang diperlukan untuk menjadi daun (leaf) di pohon. Semakin tinggi nilai ini, semakin sedikit daun, yang membuat pohon lebih sederhana dan mencegah overfitting. Nilai 1, 2, dan 5 dipilih untuk memungkinkan variasi dalam ukuran daun, sehingga bisa memberikan keseimbangan yang baik antara kompleksitas dan performa.

-  **max_features**: Ini adalah jumlah maksimum fitur yang dipertimbangkan untuk pemisahan di setiap node. Dengan memilih 'sqrt' (akar kuadrat dari jumlah fitur) atau 'log2' (logaritma basis 2 dari jumlah fitur), model mencoba mengurangi korelasi antar pohon dan meningkatkan generalisasi. None memungkinkan semua fitur digunakan pada setiap pemisahan.

```python

rf  =  RandomForestRegressor(random_state=42)

  

param_grid  = {

'n_estimators': [int(x) for  x  in  np.linspace(start=100, stop=1000, num=10)],

'max_depth': [None] + [int(x) for  x  in  np.linspace(5, 100, num=10)],

'min_samples_split': [2, 3, 5],

'min_samples_leaf': [1, 2, 5],

'max_features': ['sqrt', 'log2', None]

}

  
random_search  =  RandomizedSearchCV(estimator  =  rf, param_distributions  =  param_grid,

n_iter  =  100, cv  =  5, verbose=0, random_state=42, n_jobs  =  -1)

```
Tuning model dilakukan menggunakan `RandomizedSearchCV` pencarian parameter dilakukan secara acak dar dari `param_distributions`. Dalam kode ini, `n_iter=100` artinya `RandomizedSearchCV` akan mencoba 100 kombinasi parameter yang dipilih secara acak dari `param_grid`. Parameter `n_jobs` menentukan jumlah core CPU yang akan digunakan untuk komputasi paralel.

Dalam kode ini, `n_jobs=-1` berarti RandomizedSearchCV akan menggunakan semua core yang tersedia pada CPU, sehingga proses training bisa berjalan lebih cepat dengan menggunakan komputasi paralel.
 
Model kedua yang dianalisis adalah XGBR. Langkah prediksi XGR adalah sebagai berikut:
![XGBR](https://www.researchgate.net/publication/348025909/figure/fig2/AS:1020217916416002@1620250314481/Simplified-structure-of-XGBoost.ppm?raw=true)

XGBR bekerja dengan membentuk pohon prediksi, namun berbeda dengan RFR, pohon selanjutnya dibentuk menggunakan residual dari pohon sebelumnya. Proses tersebut dilakukan terus menerus sehingga pohon terakhir menghasilkan prediksi dengan mempelajari dari seluruh pohon sebelumnya. Berikut merupakan code untuk XGBR dengan parameter defaulth:

```python

from xgboost import XGBRegressor

xgb = XGBRegressor(random_state=42)

xgb.fit(X_train_scaled, y_train)
```

Untuk mendapatkan performa terbaik model akan dilakukan tuning terhadap beberapa parameter berikut:

  
- n_estimators: Ini adalah jumlah pohon yang akan dibuat dalam model. Sama seperti pada Random Forest, semakin banyak pohon, semakin baik model dapat belajar, namun terlalu banyak pohon bisa mengarah pada overfitting dan waktu komputasi yang lebih tinggi. Rentang 100 hingga 1000 memungkinkan pencarian jumlah pohon yang optimal dengan keseimbangan antara akurasi dan efisiensi.

- learning_rate: Ini adalah laju pembelajaran (learning rate) yang mengontrol seberapa banyak model menyesuaikan bobot pada setiap iterasi. Nilai yang lebih kecil (0.01, 0.05) memungkinkan model belajar secara bertahap untuk hasil yang lebih stabil, sementara nilai yang lebih besar (0.1, 0.2) dapat mempercepat konvergensi tetapi dengan risiko overfitting. Kombinasi ini memungkinkan pengaturan laju belajar yang optimal.

- max_depth: Ini membatasi kedalaman maksimal dari setiap pohon dalam ensemble. Kedalaman yang lebih besar meningkatkan kompleksitas model, namun juga meningkatkan risiko overfitting. Pilihan nilai dari 5 hingga 100, serta None (tanpa batas), memberi fleksibilitas dalam memilih kedalaman optimal.

- min_child_weight: Ini menentukan jumlah minimum bobot untuk menciptakan node baru. Nilai ini mencegah pembagian yang tidak berarti dengan data yang sedikit, yang dapat menyebabkan overfitting. Nilai 1, 3, dan 5 memungkinkan fleksibilitas dalam mengontrol pertumbuhan pohon.

- subsample: Ini adalah rasio sampel data yang dipilih untuk melatih setiap pohon. Nilai yang lebih rendah seperti 0.6 dan 0.8 membantu mengurangi overfitting dengan menggunakan sebagian kecil data pada setiap iterasi, sementara nilai 1.0 menggunakan seluruh data.

- colsample_bytree: Ini adalah rasio fitur yang diambil secara acak untuk membangun setiap pohon. Pengaturan ini mengurangi korelasi antar pohon dalam ensemble, sehingga meningkatkan generalisasi model. Nilai 0.6, 0.8, dan 1.0 memberi variasi yang cukup untuk menjaga keakuratan sambil mengurangi risiko overfitting.

- gamma: Ini adalah nilai ambang batas untuk pemisahan node baru. Semakin tinggi gamma, semakin tinggi batas untuk membagi node, sehingga model lebih konservatif dalam menambah kompleksitas, yang mencegah overfitting. Rentang dari 0 hingga 0.3 memungkinkan variasi yang cukup untuk mencapai keseimbangan yang optimal.

- reg_alpha : Ini adalah regularisasi untuk mencegah overfitting dengan memaksa beberapa bobot menjadi nol, yang membuat model lebih sederhana dan teratur. Nilai 0, 0.01, 0.1, dan 1 memberi fleksibilitas untuk berbagai tingkat regularisasi.

- reg_lambda : Ini adalah regularisasi yang menambahkan penalti pada bobot besar, mengurangi overfitting. Nilai 1, 1.5, 2, dan 5 memberikan pilihan tingkat regularisasi yang lebih besar atau lebih kecil, memungkinkan model untuk menyeimbangkan bias dan varians.


```python
xgboost  = XGBRegressor(objective='reg:squarederror', random_state=42)

param_distributions  = {

'n_estimators': [int(x) for  x  in  np.linspace(100, 1000, num=10)],

'learning_rate': [0.01, 0.05, 0.1, 0.2],

'max_depth': [None] + [int(x) for  x  in  np.linspace(5, 100, num=10)],

'min_child_weight': [1, 3, 5],

'subsample': [0.6, 0.8, 1.0],

'colsample_bytree': [0.6, 0.8, 1.0],

'gamma': [0, 0.1, 0.2, 0.3],

'reg_alpha': [0, 0.01, 0.1, 1],

'reg_lambda': [1, 1.5, 2, 5]

} 

random_search  =  RandomizedSearchCV(

estimator=xgboost,

param_distributions=param_distributions,

n_iter=50,

scoring='neg_mean_squared_error',

cv=5,

verbose=0,

random_state=42,

n_jobs=-1

)

random_search.fit(X_train_scaled, y_train)
```

  Tuning model XGBR juga dilakukan menggunakan `RandomizedSearchCV`  

## Evaluation

Setelah proses modeling selesai, langkah berikutnya adalah mengevaluasi model untuk melihat performa dan menentukan model yang paling optimal. Model dievaluasi menggunakan dua metrik kesalahan berikut:

1. MSE (Mean Squared Error): mengukur rata-rata dari kuadrat kesalahan antara nilai prediksi dan nilai aktual. MSE memberi bobot lebih besar pada kesalahan yang besar, sehingga sangat berguna untuk mendeteksi model dengan kesalahan besar yang signifikan. Nilai MSE yang lebih rendah menunjukkan model yang lebih akurat.

2. MAE (Mean Absolute Error): mengukur rata-rata dari nilai absolut perbedaan antara prediksi dan nilai aktual. MAE lebih intuitif karena memberi bobot yang sama pada setiap kesalahan, tanpa menekankan kesalahan besar seperti pada MSE. Nilai MAE yang lebih rendah menunjukkan model yang lebih baik dalam memprediksi dengan rata-rata kesalahan yang lebih kecil.

  

![bar chart error model](https://github.com/alfitoptr/Wine-Detection-Using-Tree-ensemble/blob/main/wine/results/error.png?raw=true)

 
Model yang memiliki performa paling baik dengan error terendah adalah model random forest yang telah di tuning dengan nilai MSE 0.30 dan nilai MAE 0.43. Parameter model setelah tuning adalah sebagai berikut:

 ```

Best Parameters: {'n_estimators': 1000, 'min_samples_split': 2, 'min_samples_leaf': 1, 'max_features': 'log2', 'max_depth': 36}

MSE Random Forest Regressor: 0.303405423580786

MAE Random Forest Regressor: 0.4346637554585152

```

Setelah tuning model memberikan performa yang lebih baik, MSE turun menjadi 0.30 dan MAE menjadi 0.43
 
 Karena target merupakan skor dengan rentang 0 - 10, maka perlu evaluasi lain. Model terbaik random forest diukur kemampuan prediksi nya dengan menggunakan akurasi khusus.

  

Pertama ditentukan tingkat toleransi ±1. Ini berarti prediksi dianggap “benar” jika berada dalam satu poin dari skor aktual.

  

Contoh:

  

Skor aktual (y_test): [5, 3, 8, 6, 7]

Skor prediksi: [4.5, 3.2, 9.1, 6.5, 8.8]

Prediksi yang dibulatkan: [5, 3, 9, 7, 9]

  

* Untuk skor pertama (5): |5 - 5| = 0 → Benar (dalam toleransi)

* Untuk skor kedua (3): |3 - 3| = 0 → Benar

* Untuk skor ketiga (8): |9 - 8| = 1 → Benar

* Untuk skor keempat (6): |7 - 6| = 1 → Benar

* Untuk skor kelima (7): |7 - 9| = 2 → Tidak benar


  
Maka nilai akurasi dapat dihitung sebagai berikut:

$$  \text{Custom Accuracy} = \frac{\text{Number of Correct Predictions}}{\text{Total Predictions}} = \frac{4}{5} = 0.8  $$

  

Akurasi khusus ini dapat digunakan untuk melihat performa model dalam memprediksi skor kualitas wine yang sebenarnya dalam bentuk bilangan cacah (bilangan positif dimulai dari 0). Model dengan kasus regresi memberikan hasil prediksi dalam bentuk bilangan desimal sehingga membutuhkan akurasi khusus untuk menilai performa model.

  

```python

tolerance = 1  # Allowable error

  

prediksi = best_rf.predict(X_test)

prediksi_rounded = np.round(prediksi) # Round predictions

  

correct_predictions = np.sum(np.abs(prediksi_rounded - y_test) <= tolerance)

  

custom_accuracy = correct_predictions / len(y_test)

print(f"Custom accuracy (within tolerance of {tolerance}): {custom_accuracy:.2f}")

```

```

Custom accuracy (within tolerance of 1): 0.97

```

  
Akurasi khusus sebesar 0,97 mengindikasikan bahwa prediksi model sangat akurat dalam hal kedekatannya dengan nilai aktual, dengan hanya sebagian kecil (3%) prediksi yang berada di luar rentang toleransi.

  

## Conclusion

Proyek ini bertujuan untuk mengembangkan model machine learning yang mampu memprediksi kualitas wine "Vinho Verde" varian merah berdasarkan berbagai variabel fisikokimia. Dua model regresi dibandingkan, yaitu Gradient Boosting Regressor dan Random Forest Regressor, guna menentukan model yang paling efektif untuk memberikan prediksi yang akurat.

  

Setelah melakukan evaluasi terhadap model yang telah dituning, Random Forest Regressor berhasil mencapai tingkat error terendah dengan, menjadikannya model terbaik dalam proyek ini. Model ini juga memberikan nilai performa yang baik dalam akurasai khusus sebesar 0.97 sehingga mampu memberikan prediksi yang lebih konsisten dan akurat dibandingkan Gradient Boosting Regressor dalam memprediksi kualitas wine berdasarkan variabel fisikokimia yang tersedia.

  

Dengan performa yang kuat ini, Random Forest Regressor dapat direkomendasikan sebagai alat bantu dalam proses kontrol kualitas bagi produsen wine, sehingga dapat meningkatkan efisiensi pengujian produk dan membantu memastikan kualitas wine yang konsisten bagi konsumen

## Referensi:

[1] [D’Alessandro, S., & Pecotich, A. (2013). Evaluation of wine by expert and novice consumers in the presence of variations in quality, brand and country of origin cues. _Food Quality and Preference_, 28, 287-303](https://doi.org/10.1016/J.FOODQUAL.2012.10.002)

[2] [Dahal, K., Dahal, J., Banjade, H., & Gaire, S. (2021). Prediction of Wine Quality Using Machine Learning Algorithms. _Open Journal of Statistics_, 11, 278-289]([https://doi.org/10.4236/OJS.2021.112015](https://doi.org/10.4236/OJS.2021.112015))
