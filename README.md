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
