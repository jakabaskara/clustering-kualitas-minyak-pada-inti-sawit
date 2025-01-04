# Laporan Proyek UAS Penggalian Data dan Perolehan Informasi - Jaka Adi Baskara dan Fakhri Andika

## Project Overview

**Latar Belakang Proyek**

Industri minyak sawit merupakan salah satu sektor yang memegang peran penting dalam ekonomi global, khususnya di negara-negara penghasil utama seperti Indonesia dan Malaysia. Proses pengolahan minyak sawit melibatkan berbagai tahapan, mulai dari ekstraksi hingga pemurnian, yang bertujuan untuk menghasilkan produk minyak sawit berkualitas tinggi. Salah satu aspek yang sangat penting dalam proses ini adalah pengelolaan kualitas inti sawit (kernel) yang menjadi bahan baku utama dalam produksi minyak inti sawit (palm kernel oil).

Untuk memastikan kualitas inti sawit yang konsisten, pengukuran parameter-parameter kimia dan fisik menjadi sangat diperlukan. Data seperti Oil Wet Matter (OWM), Volatile Matter (VM), Oil Dry Matter (ODM), Non-Oil Solids (NOS), dan Free Fatty Acid (FFA) menjadi indikator penting yang dapat digunakan untuk menentukan kualitas dan potensi hasil ekstraksi minyak dari inti sawit. Pengukuran data ini kini dapat dilakukan dengan menggunakan teknologi analitik canggih seperti Foss NIRS (Near Infrared Spectroscopy), yang mampu memberikan data yang akurat, cepat, dan non-destruktif.

Namun, data yang diperoleh dari Foss NIRS seringkali sangat kompleks dan dalam jumlah besar, sehingga memerlukan pendekatan analisis yang efektif untuk menginterpretasi pola-pola yang tersembunyi di dalamnya. Salah satu metode yang dapat digunakan adalah clustering, yaitu teknik analisis data yang bertujuan untuk mengelompokkan data ke dalam beberapa grup berdasarkan kesamaan karakteristiknya. Dalam konteks ini, clustering dapat membantu dalam mengidentifikasi kelompok inti sawit dengan karakteristik yang serupa, sehingga nantinya hasil clustering akan dapat membantu mengelompokan kualitas minyak dari inti sawit (kernel) tersebut.

**Pentingnya Proyek**

Proyek ini penting karena:

- Mempercepat proses klasifikasi kualitas inti sawit: Dengan menggunakan teknik clustering, proses pengelompokan kualitas inti sawit dapat dilakukan secara otomatis dan lebih cepat, tanpa harus menunggu seluruh sampel selesai diuji secara manual.
- Memberikan rekomendasi kualitas minyak sawit secara real-time: Proyek ini membantu mengidentifikasi minyak sawit dengan kualitas yang baik, serta memberikan wawasan tentang langkah-langkah yang dapat diambil untuk meningkatkan kualitas minyak yang berada di bawah standar.
- Mengidentifikasi minyak sawit berkualitas buruk lebih awal: Dengan clustering, kelompok inti sawit dengan karakteristik yang menunjukkan kualitas buruk dapat dideteksi lebih cepat, sehingga tindakan perbaikan dapat segera dilakukan.

## Business Understanding

### Problem Statements

- Bagaimana kita dapat melakukan clustering untuk mengelompokkan kualitas inti sawit (kernel) berdasarkan data yang disediakan oleh mesin Foss NIRS, sehingga membantu mengidentifikasi kualitas minyak lebih awal tanpa harus menunggu seluruh proses pengujian selesai
- Bagaimana kita dapat menganalisis dan membandingkan kualitas minyak secara keseluruhan di pabrik secara lebih efektif, sehingga memberikan wawasan tentang kualitas minyak baik, minyak yang masih bisa ditingkatkan, dan minyak berkualitas buruk?

### Goals

- Mengembangkan model clustering berbasis data dari mesin Foss NIRS untuk mengelompokkan kualitas inti sawit (kernel), sehingga membantu mempercepat proses pengelolaan dan pengambilan keputusan.
- Membuat sistem analitik yang dapat memberikan wawasan kualitas minyak sawit secara keseluruhan di pabrik, dengan fokus pada kualitas baik, potensi peningkatan, dan deteksi kualitas buruk.

### Solution statements

- Content-Based Clustering: Menggunakan data deskriptif dari mesin Foss NIRS, seperti Oil Wet Matter, Volatile Matter, Oil Dry Matter, Non-Oil Solids, dan Free Fatty Acid, untuk mengelompokkan inti sawit ke dalam kelompok dengan karakteristik kualitas yang serupa
- Collaborative Analysis: Menggunakan data clustering untuk membandingkan kualitas minyak sawit di seluruh proses produksi, sehingga memberikan rekomendasi tentang langkah perbaikan atau optimalisasi berdasarkan pola dari data serupa.

## Data Understanding

Dataset yang digunakan berisi informasi mengenai berbagai kadar dalam perkebunan kelapa sawit. Dataset ini dapat diperoleh menggunakan alat [FOSS NIRS](https://news.kharisma-sawit.com/berita-terkini-beginilah-cara-kerja-foss-nir-pabrik-sawit-efektif-untuk-pks-284#:~:text=Bisa%20dikatakan%20bahwa%20FOSS%20NIRS) [1].

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
| RILL_MUTU_KADAR_AIR      | 3205 non-null  | float64 |
| INC_MUTU_KADAR_AIR       | 3205 non-null  | object  |

Variabel-variabel pada dataset adalah sebagai berikut:

- `COMPANY`: ID Perusahan penghasil kelapa sawit
- `PKS_CODE`: Kode Perkebunan kelapa sawit.
- `INSTRUMENT_SERIAL_NUMBER`: serial number intrumen dari kelapa sawit.
- `OIL_WM`: Kandungan minyak dalam kondisi basah (Oil WetMatter).
- `VM`: Kandungan zat volatil (Volatile Matter).
- `OIL_DM`: Kandungan minyak dalam kondisi kering(OilDryMatter).
- `NOS`: Kandungan padatan bukan minyak(NonOilSolids).
- `FFA`: Asam lemak bebas(Free Fatty Acid).
- `RILL_MUTU_KADAR_AIR`: Kadar mutu air murni.
- `INC_MUTU_KADAR_AIR`: Kadar mutu air tidak murni.

## Data Preparation

**Teknik Data Preparation**

- Menggunakan beberapa kolom terlebih dahulu unutk melakukan pengclusteran yaitu `OIL_WM`, `VM`, `OIL_DM`, `NOS`, `FFA`
- Handling missing value
- Menghapus data yang memliki nilai _Outliers_
- Normalisai data

**Proses Data Preparation**

- Menggunakan kolom tertentu untuk dilanjutkan proses berikutnya
- Menghapus baris yang memiliki missing value `dropna`
- Mengeliminasi _outliers_ pada kolom `OIL_WM`, `VM`, `OIL_DM`, `NOS`, `FFA`

**Alasan Tahapan Data Preparation**

- Penggunaan kolom tertentu untuk melakukan _clustering_ terhadap kolom terkait yang kemudian akan dilakukan perhitungan persentasi pada masing-masing `PKS_CODE`

**Principal Component Analysis(PCA)**

- Pengolahan data menggunakan teknik PCA untuk mempertahankan data yang paling relevan

## Modeling

**K-Means Clustering**

Pada tahap ini akan membahas pendekatan K-Means Clustering. Berikut adalah penjelasan lebih lanjut mengenai parameter yang digunakan, kelebihan, dan kekurangan dari pendekatan tersebut.

Tahapan Proses K-Means Clustering :

1. Menggunakan Elbow Method untuk mencari nilai K

```python
inertia = []
K = range(1, 10)
for k in K:
    kmeans = KMeans(n_clusters=k, random_state=42)
    kmeans.fit(data_pca)
    inertia.append(kmeans.inertia_)

# Visualisasi
plt.figure(figsize=(8, 5))
plt.plot(K, inertia, 'bo-', markersize=8)
plt.xlabel('Jumlah Cluster (k)')
plt.ylabel('Inertia')
plt.title('Elbow Method untuk Menentukan Jumlah Cluster Optimal')
plt.grid(True)
plt.show()
```

Hasil Elbow method sperti berikut
![Elbow Method](https://github.com/jakabaskara/clustering-kualitas-minyak-pada-inti-sawit/blob/main/image/ElbowMethod.png)

dari gambar tersebut bisa diambil nilai K yang bagus adalah 2

Namun dalam case ini mencoba menggunakan 3 cluster karena mendekati standarisasi pembagian yang ada di lapangan yaitu kandungan buruk, kandungan baik, dan kandungan yang bisa ditingkatkan.

2. Menggunakan nilai K yang telah ditentukan untuk melakukan K-Means Clustering

Pada tahap menuggnakan K-Means Clustering dengan nilai K yang diambil dari perbantuan Elbow Method diatas dilakukan dua kali percobaan yaitu menggunakan nilai K = 2 dan K =3

Untuk Penggunakan nilai K = 2 pada K-Menas Clustering

```python
optimal_k = 2
kmeans = KMeans(n_clusters=optimal_k, random_state=42)
data_inliers['Cluster'] = kmeans.fit_predict(data_pca)

#Visualisasi Cluster
plt.figure(figsize=(10, 6))
for cluster in range(optimal_k):
    plt.scatter(data_pca[data_inliers['Cluster'] == cluster, 0],
                data_pca[data_inliers['Cluster'] == cluster, 1],
                label=f'Cluster {cluster}', alpha=0.7, s=100)
plt.xlabel('Principal Component 1')
plt.ylabel('Principal Component 2')
plt.title('Visualisasi Clustering setelah Penanganan Outliers, PCA, dan Normalisasi')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
```

Hasilnya seperti berikut :
![KMeansClusterKeq2](https://github.com/jakabaskara/clustering-kualitas-minyak-pada-inti-sawit/blob/main/image/KMeansClusterKeq2.png)

Untuk Penggunakan nilai K = 3 pada K-Menas Clustering

```python
optimal_k = 3
kmeans = KMeans(n_clusters=optimal_k, random_state=42)
data_inliers['Cluster'] = kmeans.fit_predict(data_pca)

#Visualisasi Cluster
plt.figure(figsize=(10, 6))
for cluster in range(optimal_k):
    plt.scatter(data_pca[data_inliers['Cluster'] == cluster, 0],
                data_pca[data_inliers['Cluster'] == cluster, 1],
                label=f'Cluster {cluster}', alpha=0.7, s=100)
plt.xlabel('Principal Component 1')
plt.ylabel('Principal Component 2')
plt.title('Visualisasi Clustering setelah Penanganan Outliers, PCA, dan Normalisasi')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
```

Hasilnya seperti berikut :
![KMeansClusterKeq3](https://github.com/jakabaskara/clustering-kualitas-minyak-pada-inti-sawit/blob/main/image/KMeansClusterKeq3.png)

**Kelebihan dan Kekurangan Pendekatan**

## Evaluation

**Metrik Evaluasi**

**Hasil Proyek**

## Kesimpulan

## Referensi

[1] [FOSS NIRS SAWIT](https://news.kharisma-sawit.com/berita-terkini-beginilah-cara-kerja-foss-nir-pabrik-sawit-efektif-untuk-pks-284#:~:text=Bisa%20dikatakan%20bahwa%20FOSS%20NIRS)
