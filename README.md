# Laporan Proyek UAS Penggalian Data dan Perolehan Informasi - Jaka Adi Baskara dan Fakhri Andika

## Project Overview

**Latar Belakang Proyek**

**Pentingnya Proyek**

## Business Understanding

### Problem Statements

### Goals

### Solution statements

## Data Understanding

Dataset yang digunakan berisi informasi mengenai berbagai kadar dalam perkebunan kelaa sawit. Dataset ini dapat diperoleh menggunakan alat [foss nirs](https://news.kharisma-sawit.com/berita-terkini-beginilah-cara-kerja-foss-nir-pabrik-sawit-efektif-untuk-pks-284#:~:text=Bisa%20dikatakan%20bahwa%20FOSS%20NIRS,cepat%20hanya%20dalam%20satu%20menit.).

| Column                   | Non-Null Count | Dtype   |
| ------------------------ | -------------- | ------- |
| COMPANY                  | 3205 non-null  | object  |
| PKS_CODE                 | 3205 non-null  | object  |
| INSTRUMENT_SERIAL_NUMBER | 674 non-null   | float64 |
| OIL_WM                   | 3205 non-null  | float64 |
| VM                       | 3205 non-null  | float64 |
| OIL_DM                   | 3205 non-null  | float64 |
| NOS                      | 3205 non-null  | float64 |
| FFA                      | 3205 non-null  | float64 |
| DOBI                     | 3205 non-null  | int64   |
| RILL_MUTU_KADAR_AIR      | 3205 non-null  | float64 |
| INC_MUTU_KADAR_AIR       | 3205 non-null  | object  |

**Principal Component Analysis(PCA)**

## Data Preparation

**Teknik Data Preparation**

**Proses Data Preparation**

**Alasan Tahapan Data Preparation**

## Modeling

**Model Sistem Rekomendasi Content Based Filtering**

**Top-N Recommendation Content Based Filtering**

Menampilkan hasil rekomendasi

- model_recommendations('iPhone XR')

| index | model              | brand | operating_system |
| ----- | ------------------ | ----- | ---------------- |
| 0     | iPhone 13 Pro Max  | Apple | iOS              |
| 1     | iPhone SE \(2022\) | Apple | iOS              |
| 2     | iPhone 13 Pro      | Apple | iOS              |
| 3     | iPhone 13          | Apple | iOS              |

- model_recommendations('Galaxy S22')

| index | model            | brand   | operating_system |
| ----- | ---------------- | ------- | ---------------- |
| 0     | Galaxy S22 Plus  | Samsung | Android          |
| 1     | Galaxy Z Fold 3  | Samsung | Android          |
| 2     | Galaxy S22 Ultra | Samsung | Android          |
| 3     | Galaxy A13       | Samsung | Android          |

**Model Sistem Rekomendasi Collaborative Filtering (Alternatif)**

Collaborative Filtering menggunakan interaksi pengguna-item (rating) untuk memberikan rekomendasi. Berikut adalah parameter untuk pendekatan ini.

Parameter yang Digunakan:

- loss = BinaryCrossentropy
- optimizer = Adam
- learning_rate = 0.001
- metrics = RootMeanSquaredError

Tahapan proses:

- Menggunakan dataframe rating (cellphones rating.csv)
- Membuat class RecommenderNet dengan keras Model class

```python
class RecommenderNet(tf.keras.Model):
  ...
  ...
```

- Inisialisasi model menggunakan RecommenderNet dengan nilai embedding 50
- Compile model menggunakan
  - loss = BinaryCrossentropy
  - optimizer = Adam
  - learning_rate = 0.001
  - metrics = RootMeanSquaredError
- Melakukan training model menggunakan
  - batch_size = 8
  - epochs = 100

Bagaimana Algoritma Bekerja:

- Collaborative Filtering menggunakan interaksi pengguna-item (rating) untuk memberikan rekomendasi. Algoritma ini bekerja dengan cara memprediksi rating item yang belum diulas pengguna berdasarkan rating item yang mirip oleh pengguna lain. Model ini mempelajari pola preferensi pengguna dari data rating yang ada dan menggunakan pola tersebut untuk merekomendasikan item yang mungkin disukai pengguna.

Interaksi dengan Sampel Input:
Misalkan pengguna dengan ID 237 memiliki beberapa ponsel dengan rating tinggi dan ingin mendapatkan rekomendasi. Algoritma akan:

1. Mengambil data rating dari pengguna lain yang memiliki preferensi serupa.
2. Menggunakan model yang dilatih untuk memprediksi rating ponsel yang belum diulas oleh pengguna 237.
3. Mengembalikan daftar ponsel dengan prediksi rating tertinggi.

**Top-N Recommendation Collaborative Filtering (Alternatif)**

```
Showing recommendations for users: 237
===========================
cellphone with high ratings from user
--------------------------------
Oppo : Find X5 Pro
OnePlus : Nord 2T
OnePlus : 10 Pro
Apple : iPhone 13
Xiaomi : 11T Pro
--------------------------------
Top 10 cellphone recommendation
--------------------------------
Apple : iPhone XR
Samsung : Galaxy S22
Samsung : Galaxy A53
Vivo : X80 Pro
Apple : iPhone 13 Pro
Apple : iPhone SE (2022)
Samsung : Galaxy S22 Ultra
Apple : iPhone 13 Mini
Google : Pixel 6 Pro
Apple : iPhone 13 Pro Max
```

**Kelebihan dan Kekurangan Pendekatan**

1. Content Based Filtering

- Kelebihan:

  - Independensi Data Pengguna: Tidak memerlukan data pengguna lain, hanya berdasarkan item itu sendiri.
  - Rekomendasi Baru: Dapat merekomendasikan item baru yang belum pernah diulas sebelumnya.

- Kekurangan:
  - Keterbatasan Fitur: Hanya dapat merekomendasikan item yang memiliki fitur serupa.
  - Overfitting: Terkadang terlalu fokus pada fitur tertentu dan tidak bisa merekomendasikan item yang berbeda secara radikal.

2. Collaborative Filtering

- Kelebihan:

  - Menggunakan Data Pengguna: Memanfaatkan interaksi pengguna-item sehingga dapat merekomendasikan item yang tidak mirip tetapi disukai oleh pengguna dengan preferensi serupa.
  - Menangani Data Besar: Dapat bekerja dengan data besar dan menemukan pola-pola kompleks.

- Kekurangan:
  - Cold Start Problem: Kesulitan merekomendasikan item baru atau kepada pengguna baru yang belum memiliki cukup interaksi.

_Untuk tahapan proses yang lebih lengkap silahkan baca [Dicoding_ModelSistemRekomendasi.ipynb](https://github.com/AbiyaMakruf/Dicoding-ModelSistemRekomendasi/blob/main/Dicoding_ModelSistemRekomendasi.ipynb)_

## Evaluation

Pada bagian ini, akan mengevaluasi model rekomendasi yang telah dibangun menggunakan metrik evaluasi yang tepat. Untuk model prediksi rating, kita akan menggunakan Root Mean Squared Error (RMSE) sebagai metrik evaluasi. Selain itu, akan mengevaluasi apakah proyek ini berhasil menjawab problem statement dan memberikan solusi yang diinginkan.

**Metrik Evaluasi**

Root Mean Squared Error (RMSE) adalah akar kuadrat dari rata-rata kuadrat kesalahan. Ini memberikan gambaran seberapa jauh prediksi model berbeda dari nilai sebenarnya dalam satuan yang sama dengan variabel yang diprediksi. RMSE sangat berguna karena memberikan penalti lebih besar untuk kesalahan yang lebih besar.

$$
\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}
$$

Di mana:

- $y_i$ adalah nilai sebenarnya
- $\hat y_i$ adalah nilai prediksi
- $n$ adalah jumlah observasi

- RMSE yang kecil mengindikasikan bahwa model memiliki performa yang baik karena kesalahan antara prediksi dan nilai aktual rendah.
- RMSE yang besar mengindikasikan bahwa model memiliki performa yang buruk karena kesalahan antara prediksi dan nilai aktual tinggi.

**Hasil Proyek**
| | Train | Test |
|------------|------- |-------|
| RMSE | 0.2063 | 0.6416|

![Grafik train vs test](https://raw.githubusercontent.com/AbiyaMakruf/Dicoding-ModelSistemRekomendasi/main/image/image6.png)

RMSE yang dihitung memberikan indikasi bahwa model prediksi rating memiliki tingkat kesalahan yang dapat diterima, sehingga memadai untuk tujuan rekomendasi.

**Evaluasi Terhadap Business Understanding**

- Menjawab Problem Statement: Model yang dibuat berhasil menjawab problem statement dengan memberikan rekomendasi ponsel berdasarkan model yang ada dan memprediksi rating ponsel yang belum diulas oleh pengguna. Pendekatan content-based filtering menggunakan model ponsel untuk memberikan rekomendasi yang relevan berdasarkan kesamaan model, brand, dan operating system, sementara collaborative filtering memanfaatkan interaksi pengguna-item (rating) untuk menemukan pola preferensi pengguna.

- Mencapai Goals: Model content-based filtering dengan cosine similarity dan collaborative filtering dengan RecommenderNet berhasil mencapai tujuan untuk memberikan rekomendasi ponsel yang relevan. Content-based filtering menggunakan data deskriptif yaitu model ponsel untuk membuat profil item, sehingga meningkatkan akurasi rekomendasi dengan memperhitungkan kesamaan fitur (model, brand, operating system). Di sisi lain, collaborative filtering memanfaatkan data rating dari pengguna untuk menemukan pola preferensi dan merekomendasikan ponsel yang sesuai dengan kesukaan pengguna.

- Dampak dari Solution Statement: Penggunaan beberapa pendekatan algoritma (content-based dan collaborative filtering) dan teknik evaluasi seperti RMSE memberikan dampak positif dengan meningkatkan relevansi dan akurasi rekomendasi. Content-based filtering memastikan bahwa model ponsel yang diberikan dapat memberikan rekomendasi yang relevan dengan ponsel lamanya karena mempertimbangkan kesamaan fitur (model, brand, operating system) bagi pengguna. Sementara itu, collaborative filtering memungkinkan sistem untuk memahami preferensi pengguna berdasarkan interaksi sebelumnya, memberikan rekomendasi yang dipersonalisasi. Solusi yang direncanakan memberikan hasil yang signifikan dalam mencapai tujuan proyek, memastikan bahwa rekomendasi yang diberikan sesuai dengan kebutuhan dan preferensi pengguna.

## Kesimpulan

Dengan menggunakan kedua pendekatan ini, kita dapat membangun sistem rekomendasi yang lebih robust dan fleksibel. Content-Based Filtering cocok untuk memberikan rekomendasi berdasarkan fitur-fitur item itu sendiri, sementara Collaborative Filtering efektif dalam menemukan pola-pola preferensi pengguna dari data interaksi yang ada. Memahami kelebihan dan kekurangan masing-masing pendekatan membantu kita memilih metode yang paling sesuai dengan kebutuhan dan konteks spesifik dari sistem rekomendasi yang sedang dibangun.

## Referensi
