# Perbandingan Metode K-Means dan Hierarchical Clustering dalam Pengelompokan Kabupaten/Kota di Jawa Tengah Berdasarkan Indikator Kesenjangan Digital
# Tujuan Bisnis :

Project ini bertujuan untuk mengelompokkan 35 kabupaten/kota di Provinsi Jawa Tengah
berdasarkan empat indikator kesenjangan digital tahun 2020, yaitu:
1. Persentase penduduk menggunakan HP
2. Persentase penduduk mengakses internet
3. Persentase desa/kelurahan dengan penerimaan sinyal internet 4G
4. Persentase rumah tangga yang memiliki komputer/laptop

Data yang digunakan merupakan data sekunder dari Badan Pusat Statistik (BPS)
Provinsi Jawa Tengah tahun 2020. Proses analisis meliputi validasi dan standardisasi
data (Z-score) sebelum dilakukan clustering.

Dua metode clustering yang diterapkan dan dibandingkan adalah:
- K-Means Clustering, dengan penentuan jumlah cluster menggunakan Elbow Method
  dan Silhouette Method
- Hierarchical Clustering (agglomerative) dengan Ward linkage

Hasil pengelompokan kedua metode dievaluasi dan dibandingkan menggunakan Silhouette Score dan Adjusted Rand Index (ARI), untuk mengetahui kualitas serta tingkat kesesuaian antar hasil clustering. Interpretasi cluster dilakukan berdasarkan pola rata-rata nilai indikator pada masing-masing kelompok, yang kemudian diurutkan dan diberi label tingkat akses dan pemanfaatan TIK (Rendah, Sedang, Tinggi, Sangat Tinggi) berdasarkan skor rata-rata terstandardisasi, tanpa memberikan penilaian kualitatif (baik/buruk) terhadap wilayah tertentu.
## Deskripsi Project

### Latar Belakang
Perkembangan teknologi informasi dan komunikasi (TIK) telah mengubah berbagai aspek kehidupan masyarakat, mulai dari komunikasi, pendidikan, pekerjaan, pelayanan publik, hingga aktivitas ekonomi. Namun, kemajuan ini tidak merata di setiap wilayah karena terdapat variasi dalam penggunaan perangkat telekomunikasi, akses internet, ketersediaan jaringan, maupun kepemilikan komputer atau laptop. Variasi ini mencerminkan adanya **kesenjangan digital** antarwilayah. Provinsi Jawa Tengah, yang terdiri atas 35 kabupaten/kota dengan karakteristik wilayah dan kondisi sosial yang beragam, berpotensi mengalami perbedaan kondisi digital antarwilayahnya. Oleh karena itu, diperlukan pendekatan analitik berupa *clustering* untuk memetakan kemiripan dan perbedaan kondisi digital di antara kabupaten/kota tersebut.

### Tujuan Project
Project ini bertujuan untuk mengelompokkan 35 kabupaten/kota di Provinsi Jawa Tengah berdasarkan empat indikator kesenjangan digital tahun 2020 menggunakan **K-Means Clustering** dan **Hierarchical Clustering**, kemudian membandingkan kinerja kedua metode tersebut menggunakan ukuran evaluasi clustering (Silhouette Score dan Adjusted Rand Index).

### Rumusan Masalah
1. Bagaimana karakteristik indikator kesenjangan digital pada 35 kabupaten/kota di Jawa Tengah berdasarkan data tahun 2020?
2. Bagaimana hasil pengelompokan menggunakan metode K-Means Clustering?
3. Bagaimana hasil pengelompokan menggunakan metode Hierarchical Clustering?
4. Bagaimana perbandingan hasil kedua metode berdasarkan ukuran evaluasi clustering?

### Target Analisis
Project ini bersifat *unsupervised learning*, sehingga tidak terdapat variabel target. Hasil pengelompokan kemudian diberi label interpretatif **tingkat akses dan pemanfaatan TIK**, yaitu:
- **Rendah**
- **Sedang**
- **Tinggi**
- **Sangat Tinggi**

Label tersebut ditentukan berdasarkan urutan skor rata-rata terstandardisasi setiap cluster, dan bukan merupakan indeks baru maupun penilaian baik/buruk terhadap wilayah tertentu.

### Gambaran Umum Alur Pengerjaan
Project ini dikerjakan melalui beberapa tahapan utama, yaitu:
1. Import library yang dibutuhkan
2. Input dan pemeriksaan awal dataset
3. Validasi data (penghapusan data agregat provinsi, pemeriksaan missing value dan data duplikat)
4. Statistik deskriptif variabel clustering
5. Standardisasi data menggunakan Z-score
6. Penentuan jumlah cluster menggunakan Elbow Method dan Silhouette Score
7. Pembentukan cluster dengan K-Means (K = 4)
8. Pembentukan cluster dengan Hierarchical Clustering (Ward linkage) beserta dendrogram
9. Profiling cluster, pengurutan cluster, dan pemberian label tingkat TIK
10. Evaluasi dan perbandingan hasil menggunakan Silhouette Score dan Adjusted Rand Index (ARI)
11. Visualisasi spasial hasil K-Means dalam bentuk peta kabupaten/kota Jawa Tengah

## Anggota Tim

| No | Nama | NIM |
|----|------|-----|
| 1 | Faza Hamdi Yogaswara | K1D024011|
| 2 | Ardika Wahyu Fariz | K1D024013 |
| 3 | Muhammad Alief Badrudin | K1D024030 |

## Dataset

- **Nama Dataset**: Data Indikator Kesenjangan Digital Kabupaten/Kota Jawa Tengah (`data_gabungan cluster.xlsx`)
- **Sumber Data**: Data sekunder dari Badan Pusat Statistik (BPS) Provinsi Jawa Tengah tahun 2020, dimuat melalui Google Colab (`/content/data_gabungan cluster.xlsx`)
- **Data Spasial**: `kab_kota.geojson` (batas wilayah kabupaten/kota) untuk visualisasi peta
- **Jumlah Observasi**: 36 baris pada dataset awal, menjadi **35 baris** (29 kabupaten dan 6 kota) setelah data agregat Provinsi Jawa Tengah dihapus
- **Jumlah Variabel**: 5 kolom (1 kolom identitas wilayah dan 4 kolom indikator)

### Daftar Variabel
| Kode | Variabel | Satuan | Keterangan |
|------|----------|--------|------------|
| X1 | Persentase penduduk menggunakan HP | Persen (%) | Proporsi penduduk yang menggunakan perangkat HP |
| X2 | Persentase penduduk mengakses internet | Persen (%) | Proporsi penduduk yang mengakses internet |
| X3 | Persentase desa/kelurahan dengan penerimaan sinyal internet 4G | Persen (%) | Kondisi penerimaan jaringan internet 4G pada wilayah desa/kelurahan |
| X4 | Persentase rumah tangga yang memiliki komputer/laptop | Persen (%) | Proporsi rumah tangga yang memiliki komputer atau laptop |

Kolom `Kabupaten_Kota` digunakan sebagai identitas objek dan tidak dilibatkan dalam perhitungan jarak.

### Karakteristik Dataset
- Dataset **tidak memiliki missing value** pada seluruh variabel (dikonfirmasi melalui `df.isnull().sum()`)
- Dataset **tidak memiliki data duplikat** (`df.duplicated().sum()` = 0)
- Baris data agregat **3300 PROVINSI JAWA TENGAH** dikeluarkan karena unit analisis adalah kabupaten/kota (nilai sinyal 4G pada baris agregat sebesar 158,56 jauh berbeda dari nilai kabupaten/kota)
- Statistik deskriptif keempat indikator (N = 35):

| Statistik | Penggunaan HP (%) | Akses Internet (%) | Sinyal 4G | Komputer/Laptop (%) |
|-----------|-------------------|--------------------|-----------|---------------------|
| Rata-rata | 76,3703 | 55,9403 | 4,5303 | 17,2100 |
| Standar deviasi | 5,1960 | 8,9119 | 2,1106 | 8,5456 |
| Minimum | 68,9300 | 46,3600 | 0,3400 | 6,4200 |
| Kuartil 1 (25%) | 72,7000 | 49,5150 | 3,5350 | 11,6800 |
| Median (50%) | 75,5700 | 52,5100 | 4,8600 | 15,1300 |
| Kuartil 3 (75%) | 78,8900 | 59,4650 | 5,5150 | 18,7150 |
| Maksimum | 87,0300 | 76,2400 | 8,4800 | 43,4500 |

## Metodologi

### 1. Import Library
Mengimpor library untuk pengolahan data (Pandas, NumPy), visualisasi (Matplotlib, Seaborn, GeoPandas), pemodelan clustering dan evaluasi (Scikit-learn), serta pembuatan dendrogram (SciPy).

### 2. Input Data
Dataset dibaca dari file Excel menggunakan `pandas.read_excel()`, kemudian diperiksa menggunakan `df.head()`, `df.shape`, dan `df.columns.tolist()`.

### 3. Validasi Data
- Penghapusan baris data agregat Provinsi Jawa Tengah (kode 3300) sehingga tersisa 35 kabupaten/kota
- Pemeriksaan daftar kabupaten/kota yang digunakan
- Pemeriksaan missing value dan data duplikat

### 4. Statistik Deskriptif
Menggunakan `X.describe()` pada empat variabel clustering untuk mengetahui rata-rata, standar deviasi, minimum, kuartil, dan maksimum setiap indikator.

### 5. Standardisasi Data
Standardisasi dilakukan dengan **Z-score** menggunakan `StandardScaler` agar keempat indikator memiliki skala yang sebanding dan tidak ada variabel yang mendominasi perhitungan jarak Euclidean:

$$Z_{ij} = \frac{X_{ij} - \bar{X}_j}{s_j}$$

Setelah standardisasi, rata-rata seluruh variabel mendekati 0 (orde 10⁻¹⁶) dan standar deviasi sebesar 1,014599. Nilai tersebut berbeda dari 1 karena `.std()` pada pandas menggunakan standar deviasi sampel, sedangkan `StandardScaler` menggunakan standar deviasi populasi.

### 6. Penentuan Jumlah Cluster
- **Elbow Method**: nilai inertia dihitung untuk K = 2 sampai 10 (`random_state=42`, `n_init=10`)
- **Silhouette Score**: dihitung untuk K = 2 sampai 10 pada data terstandardisasi
- Jumlah cluster yang digunakan adalah **K = 4** (alasan pemilihan dijelaskan pada bagian Hasil dan Temuan Utama)

### 7. K-Means Clustering
K-Means diterapkan pada data terstandardisasi dengan `n_clusters=4`, `random_state=42`, dan `n_init=10`.

### 8. Hierarchical Clustering
Menggunakan pendekatan *agglomerative* dengan **Ward linkage** pada data terstandardisasi. Dendrogram dibuat dengan `scipy.cluster.hierarchy`, sedangkan label cluster dibentuk menggunakan `AgglomerativeClustering(n_clusters=4, linkage="ward")` agar dapat dibandingkan pada jumlah cluster yang sama dengan K-Means.

### 9. Profiling dan Pelabelan Cluster
- Profil setiap cluster dihitung dari rata-rata keempat indikator
- Nomor cluster asli dari algoritma bersifat teknis, sehingga cluster diurutkan berdasarkan **skor rata-rata terstandardisasi** dari rendah ke tinggi, lalu dipetakan ulang dan diberi label tingkat TIK (Rendah, Sedang, Tinggi, Sangat Tinggi)

### 10. Evaluasi Model
Evaluasi dilakukan menggunakan:
- **Silhouette Score** untuk menilai kekompakan dan pemisahan cluster pada masing-masing metode
- **Adjusted Rand Index (ARI)** untuk mengukur tingkat kesamaan hasil pengelompokan antara K-Means dan Hierarchical Clustering

### 11. Visualisasi Spasial
Hasil K-Means digabungkan dengan data GeoJSON berdasarkan nama wilayah (`Nama_Wilayah`) dan divisualisasikan dalam bentuk peta cluster kabupaten/kota di Jawa Tengah. Data GeoJSON memuat seluruh kabupaten/kota di Indonesia, sehingga hanya 35 wilayah Jawa Tengah yang terhubung dengan hasil cluster.

## Metode yang Digunakan

| Metode | Penjelasan Singkat |
|--------|---------------------|
| **K-Means Clustering** | Metode clustering berbasis partisi yang mengelompokkan objek ke dalam K cluster berdasarkan kedekatan terhadap centroid, dengan tujuan meminimalkan jarak kuadrat dalam cluster |
| **Hierarchical Clustering (Agglomerative, Ward)** | Metode clustering yang membentuk kelompok secara bertahap dari setiap objek sebagai satu cluster, lalu menggabungkan cluster dengan peningkatan variasi dalam cluster terkecil. Hasilnya divisualisasikan melalui dendrogram |

Ukuran pendukung yang digunakan:

| Ukuran | Kegunaan |
|--------|----------|
| **Elbow Method (Inertia)** | Membantu menentukan kandidat jumlah cluster dari titik siku penurunan inertia |
| **Silhouette Score** | Menentukan jumlah cluster dan mengevaluasi kualitas hasil clustering (rentang -1 sampai 1) |
| **Adjusted Rand Index (ARI)** | Membandingkan kesamaan dua hasil pengelompokan dengan memperhitungkan kemungkinan kesamaan secara acak |

## Cara Menjalankan Project

### 1. Clone Repository
```bash
git clone https://github.com/username/clustering-kesenjangan-digital-jateng.git
cd clustering-kesenjangan-digital-jateng
```

### 2. Install Dependencies
```bash
pip install pandas numpy seaborn matplotlib scikit-learn scipy geopandas openpyxl
```

### 3. Menyiapkan Dataset
Letakkan file `data_gabungan cluster.xlsx` dan `kab_kota.geojson` pada folder `data/`, atau sesuaikan path pada notebook jika menjalankan melalui Google Colab:
```python
df = pd.read_excel("/content/data_gabungan cluster.xlsx")
jateng = gpd.read_file("/content/kab_kota.geojson")
```

### 4. Menjalankan Notebook/Script
```bash
jupyter notebook notebook/Project_Analisis_Clustering.ipynb
```
Atau jika dijalankan di Google Colab, unggah notebook beserta kedua file data, kemudian jalankan seluruh sel secara berurutan (Run All).

## Struktur Folder Project

```
clustering-kesenjangan-digital-jateng/
│
├── data/
│   ├── data_gabungan cluster.xlsx
│   └── kab_kota.geojson
│
├── notebook/
│   └── Project_Analisis_Clustering.ipynb
│
├── laporan/
│   └── project_clustering_fix_harusnya.docx
│
├── README.md
└── requirements.txt
```

## Hasil dan Temuan Utama

### Kondisi Dataset
- Dataset bersih, tanpa missing value dan tanpa data duplikat setelah data agregat provinsi dikeluarkan
- Penggunaan HP dan akses internet relatif merata antarwilayah, sedangkan kepemilikan komputer/laptop (rentang 6,42% sampai 43,45%) dan penerimaan sinyal 4G menunjukkan variasi yang lebih besar antarwilayah

### Penentuan Jumlah Cluster

**Elbow Method**: inertia menurun dari sekitar 53 pada K = 2 menjadi sekitar 26 pada K = 4, kemudian melandai hingga sekitar 11 pada K = 10. Titik siku berada pada kisaran K = 3 sampai 4.

**Silhouette Score** untuk berbagai jumlah cluster:

| Jumlah Cluster (K) | Silhouette Score |
|--------------------|------------------|
| 2 | **0,5723** |
| 3 | 0,4581 |
| 4 | 0,4102 |
| 5 | 0,3307 |
| 6 | 0,3309 |
| 7 | 0,3021 |
| 8 | 0,3042 |
| 9 | 0,2564 |
| 10 | 0,2594 |

Silhouette Score tertinggi berada pada K = 2, namun analisis dilanjutkan dengan **K = 4**. Pemilihan ini mengikuti titik siku pada Elbow Method (K = 3 sampai 4) dan memberikan granularitas yang lebih terperinci sehingga wilayah dapat dibedakan ke dalam empat tingkat TIK: Rendah, Sedang, Tinggi, dan Sangat Tinggi.

### Hasil K-Means Clustering (K = 4)

Urutan cluster berdasarkan skor rata-rata terstandardisasi (pemetaan cluster asli ke cluster urut: 2→1, 1→2, 4→3, 3→4):

| Cluster | Tingkat TIK | Jumlah Wilayah | Skor Rata-Rata Terstandardisasi | HP (%) | Internet (%) | Sinyal 4G | Komputer/Laptop (%) |
|---------|-------------|----------------|---------------------------------|--------|--------------|-----------|---------------------|
| 1 | Rendah | 20 | -0,4096 | 72,89 | 50,61 | 4,91 | 12,70 |
| 2 | Sedang | 5 | 0,2516 | 80,39 | 62,89 | 2,27 | 21,58 |
| 3 | Tinggi | 6 | 0,3359 | 78,27 | 54,70 | 7,28 | 15,45 |
| 4 | Sangat Tinggi | 4 | 1,2299 | 85,88 | 75,78 | 1,34 | 36,92 |

Anggota setiap cluster:
- **Rendah (20)**: Cilacap, Purbalingga, Banjarnegara, Wonosobo, Magelang, Boyolali, Wonogiri, Karanganyar, Sragen, Grobogan, Blora, Rembang, Jepara, Demak, Temanggung, Batang, Pekalongan, Pemalang, Tegal, Brebes
- **Sedang (5)**: Sukoharjo, Kudus, Kabupaten Semarang, Kota Pekalongan, Kota Tegal
- **Tinggi (6)**: Banyumas, Kebumen, Purworejo, Klaten, Pati, Kendal
- **Sangat Tinggi (4)**: Kota Magelang, Kota Surakarta, Kota Salatiga, Kota Semarang

### Hasil Hierarchical Clustering (Ward, K = 4)

Urutan cluster berdasarkan skor rata-rata terstandardisasi (pemetaan cluster asli ke cluster urut: 1→1, 2→2, 4→3, 3→4):

| Cluster | Tingkat TIK | Jumlah Wilayah | Skor Rata-Rata Terstandardisasi | HP (%) | Internet (%) | Sinyal 4G | Komputer/Laptop (%) |
|---------|-------------|----------------|---------------------------------|--------|--------------|-----------|---------------------|
| 1 | Rendah | 23 | -0,3127 | 73,68 | 51,71 | 4,97 | 13,37 |
| 2 | Sedang | 4 | 0,2191 | 80,84 | 63,17 | 1,71 | 21,72 |
| 3 | Tinggi | 4 | 0,3490 | 77,88 | 53,18 | 8,01 | 15,04 |
| 4 | Sangat Tinggi | 4 | 1,2299 | 85,88 | 75,78 | 1,34 | 36,92 |

Anggota setiap cluster:
- **Rendah (23)**: sebagian besar kabupaten, termasuk Banyumas, Kabupaten Semarang, dan Kendal
- **Sedang (4)**: Sukoharjo, Kudus, Kota Pekalongan, Kota Tegal
- **Tinggi (4)**: Kebumen, Purworejo, Klaten, Pati
- **Sangat Tinggi (4)**: Kota Magelang, Kota Surakarta, Kota Salatiga, Kota Semarang

### Perbandingan K-Means dan Hierarchical Clustering

| Ukuran Evaluasi | K-Means | Hierarchical (Ward) |
|-----------------|---------|---------------------|
| Silhouette Score | **0,4102** | 0,3738 |
| Selisih Silhouette Score | 0,0364 | |
| Adjusted Rand Index (ARI) | 0,7454 | |

Distribusi wilayah berdasarkan tingkat TIK:

| Tingkat TIK | K-Means | Hierarchical Clustering |
|-------------|---------|--------------------------|
| Rendah | 20 | 23 |
| Sedang | 5 | 4 |
| Tinggi | 6 | 4 |
| Sangat Tinggi | 4 | 4 |
| **Total** | **35** | **35** |

Dari 35 kabupaten/kota, **32 wilayah** memperoleh tingkat TIK yang sama pada kedua metode. Tiga wilayah yang berbeda hasilnya:

| Kabupaten | K-Means | Hierarchical |
|-----------|---------|--------------|
| Kabupaten Banyumas | Tinggi | Rendah |
| Kabupaten Semarang | Sedang | Rendah |
| Kabupaten Kendal | Tinggi | Rendah |

### Metode dengan Performa Terbaik
**K-Means Clustering** terpilih sebagai metode terbaik dalam penelitian ini karena memiliki Silhouette Score yang lebih tinggi (0,4102) dibandingkan Hierarchical Clustering (0,3738).

### Insight Utama
- Keempat wilayah dengan tingkat TIK **Sangat Tinggi** konsisten sama pada kedua metode, yaitu **Kota Magelang, Kota Surakarta, Kota Salatiga, dan Kota Semarang**, dengan penggunaan HP 85,88%, akses internet 75,78%, dan kepemilikan komputer/laptop 36,92%
- Sebagian besar wilayah (20 dari 35 pada K-Means, 23 dari 35 pada Hierarchical) berada pada tingkat TIK **Rendah**
- Karakteristik digital tidak ditentukan oleh satu indikator saja. Cluster Sangat Tinggi unggul pada penggunaan HP, akses internet, dan kepemilikan komputer/laptop, tetapi memiliki rata-rata penerimaan sinyal 4G terendah (1,34), sedangkan cluster Tinggi memiliki rata-rata sinyal 4G tertinggi (7,28 pada K-Means dan 8,01 pada Hierarchical)
- Nilai ARI sebesar 0,7454 menunjukkan kedua metode menghasilkan pola pengelompokan yang cukup serupa, dengan perbedaan hanya pada beberapa wilayah
- Peta K-Means menunjukkan bahwa kedekatan geografis tidak selalu berarti kesamaan karakteristik kesenjangan digital, karena pengelompokan didasarkan pada kemiripan empat indikator dan bukan pada lokasi

## Library yang Digunakan

- `pandas`: manipulasi dan pengelolaan dataset
- `numpy`: operasi komputasi numerik
- `matplotlib`: visualisasi data (grafik Elbow, Silhouette, dendrogram, peta)
- `seaborn`: visualisasi data statistik
- `geopandas`: pembacaan data GeoJSON dan pembuatan peta cluster
- `openpyxl`: pembacaan file Excel melalui `pandas.read_excel()`
- `scikit-learn`: meliputi:
  - `StandardScaler`
  - `KMeans`, `AgglomerativeClustering`
  - `silhouette_score`, `adjusted_rand_score`
- `scipy`: `linkage` dan `dendrogram` pada `scipy.cluster.hierarchy`

## Kesimpulan

Berdasarkan keseluruhan proses analisis, 35 kabupaten/kota di Jawa Tengah memiliki karakteristik indikator kesenjangan digital yang berbeda, terutama pada penggunaan HP, akses internet, penerimaan sinyal 4G, dan kepemilikan komputer/laptop. Penentuan jumlah cluster dilakukan dengan mempertimbangkan Elbow Method (titik siku pada K = 3 sampai 4) dan Silhouette Score, dan analisis dilanjutkan dengan 4 cluster agar pengelompokan menggambarkan empat tingkat TIK.

K-Means menghasilkan 20 wilayah pada tingkat Rendah, 5 pada Sedang, 6 pada Tinggi, dan 4 pada Sangat Tinggi, sedangkan Hierarchical Clustering menghasilkan 23, 4, 4, dan 4 wilayah. Kedua metode sepakat bahwa Kota Magelang, Kota Surakarta, Kota Salatiga, dan Kota Semarang berada pada tingkat Sangat Tinggi. Berdasarkan Silhouette Score, **K-Means (0,4102)** menghasilkan pengelompokan yang lebih baik dibandingkan Hierarchical Clustering (0,3738), sementara Adjusted Rand Index sebesar 0,7454 menunjukkan kesesuaian yang cukup tinggi antara kedua metode. Perbedaan hasil hanya terdapat pada Kabupaten Banyumas, Kabupaten Semarang, dan Kabupaten Kendal.

### Saran
- Menggunakan data tahun yang lebih baru agar kondisi kesenjangan digital lebih menggambarkan kondisi terkini
- Menambah indikator lain seperti kualitas jaringan internet, penggunaan internet untuk kegiatan ekonomi, atau literasi digital
- Mencoba metode clustering lain seperti K-Medoids, DBSCAN, atau Hierarchical Clustering dengan jenis linkage berbeda
- Menambah ukuran evaluasi seperti Davies-Bouldin Index dan Calinski-Harabasz Index
- Mengembangkan analisis spasial dan visualisasi peta secara lebih mendalam

## Referensi

- Badan Pusat Statistik. (2021). *Statistik Telekomunikasi Indonesia 2020*. Jakarta: Badan Pusat Statistik.
- Badan Pusat Statistik Provinsi Jawa Tengah. (2022). *Persentase Penduduk Berumur 5 Tahun ke Atas yang Menggunakan Telepon Seluler (HP)/Nirkabel dalam 3 Bulan Terakhir menurut Kabupaten/Kota dan Jenis Kelamin, 2020*. BPS Provinsi Jawa Tengah.
- Badan Pusat Statistik Provinsi Jawa Tengah. (2022). *Persentase Penduduk Laki-laki dan Perempuan Berumur 5 Tahun ke Atas yang Mengakses Internet dalam 3 Bulan Terakhir menurut Kabupaten/Kota dan Alat yang Digunakan untuk Mengakses Internet, 2020*. BPS Provinsi Jawa Tengah.
- Hidayati, R., Indana, L., Karyudi, M. D. P., & Sasongko, R. Z. (2024). Analisis Cluster dengan K-Means untuk Pengelompokan Kabupaten/Kota di Provinsi Jawa Timur Berdasarkan Pembangunan TIK Tahun 2021–2022. *Jurnal JTIK (Jurnal Teknologi Informasi dan Komunikasi), 8*(2), 405–411. https://doi.org/10.35870/jtik.v8i2.1815
- Rahmawatin, R., Permatasari, N. P., Wijayanto, A. W., & Marsisno, W. (2024). Analisis Cluster Kondisi Keterampilan, Akses dan Fasilitas Teknologi Informasi dan Komunikasi di Indonesia. *Komputika: Jurnal Sistem Komputer, 13*(1), 83–92. https://doi.org/10.34010/komputika.v13i1.10796
- Rahmati, R. (2021). Analisis Cluster dengan Algoritma K-Means, Fuzzy C-Means dan Hierarchical Clustering (Studi Kasus: Indeks Pembangunan Manusia Tahun 2019). *JIKO (Jurnal Informatika dan Komputer), 5*(2). https://dx.doi.org/10.26798/jiko.v5i2.422
- Zulfikar, A. A., & Amidi, A. (2022). Perbandingan Analisis Klaster K-Means dan Average Linkage untuk Mengelompokkan Provinsi di Indonesia Berdasarkan Penerimaan Sinyal Telepon. *PRISMA, Prosiding Seminar Nasional Matematika, 5*, 731–739.
