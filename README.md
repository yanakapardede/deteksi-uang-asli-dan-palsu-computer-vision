# MINI PROJECT PENGOLAHAN CITRA DIGITAL (PCD)

# Deteksi Uang Kertas Asli dan Palsu Menggunakan Computer Vision Klasik

## Deskripsi Proyek

Proyek ini merupakan **Mini Project mata kuliah Pengolahan Citra Digital (PCD)** yang bertujuan untuk mengembangkan sistem sederhana dalam membedakan citra uang kertas asli dan uang palsu berdasarkan karakteristik visual menggunakan pendekatan *Computer Vision* klasik.

Penelitian ini menerapkan beberapa teknik ekstraksi fitur untuk memperoleh informasi penting dari citra, meliputi distribusi warna menggunakan *Color Histogram*, karakteristik tekstur menggunakan *Local Binary Pattern* (LBP), serta struktur tepi menggunakan *Canny Edge Detection*.

Proses klasifikasi dilakukan menggunakan pendekatan berbasis aturan (*rule-based*) dengan menghitung jarak Euclidean (*Euclidean Distance*) antara fitur citra dan rata-rata fitur dari masing-masing kelas. Selain itu, dilakukan penggabungan beberapa fitur (*Feature Combination*) untuk mengetahui pengaruh kombinasi karakteristik visual terhadap hasil klasifikasi.

Proyek ini juga membandingkan hasil klasifikasi berdasarkan penggunaan fitur secara individual maupun kombinasi untuk mengetahui pendekatan yang memberikan performa terbaik.

## Tujuan Proyek

Tujuan dari mini project ini adalah:

1. Menerapkan konsep pengolahan citra digital dalam proses identifikasi karakteristik visual uang kertas.
2. Melakukan preprocessing untuk mempersiapkan citra sebelum proses ekstraksi fitur.
3. Mengekstraksi karakteristik citra menggunakan Color Histogram, Local Binary Pattern (LBP), dan Canny Edge Detection.
4. Mengimplementasikan klasifikasi berbasis aturan menggunakan Euclidean Distance tanpa menggunakan model Machine Learning.
5. Membandingkan performa setiap metode ekstraksi fitur.
6. Menganalisis pengaruh kombinasi fitur terhadap hasil klasifikasi.
7. Mengevaluasi hasil klasifikasi menggunakan Accuracy dan Confusion Matrix.

## Dataset

Dataset yang digunakan merupakan dataset citra uang kertas yang dikumpulkan secara mandiri.

Dataset terdiri dari dua kelas utama:

- **Uang Asli:** Citra uang kertas asli.
- **Uang Palsu:** Citra uang mainan yang digunakan sebagai representasi uang palsu dalam penelitian ini.

Dataset memiliki total **120 citra**, dengan rincian sebagai berikut:

| Kategori | Jumlah Citra |
|---|---:|
| Uang Asli | 60 |
| Uang Palsu | 60 |
| **Total** | **120** |

Citra mencakup tiga pecahan uang, yaitu Rp20.000, Rp50.000, dan Rp100.000.

Pengambilan gambar dilakukan dengan variasi kondisi pencahayaan, orientasi, dan jarak. Oleh karena itu, beberapa citra memiliki kemungkinan gangguan seperti bayangan, blur, dan latar belakang yang tidak seragam.

Seluruh citra diseragamkan ukurannya menjadi **256 × 256 piksel** sebelum diproses lebih lanjut.

## Metodologi

Tahapan pengolahan citra dalam proyek ini meliputi beberapa proses berikut.

### 1. Dataset Loading

Tahap awal dilakukan dengan membaca seluruh citra dari direktori dataset yang telah dikelompokkan berdasarkan kategori uang asli dan uang palsu.

Setiap citra diberikan label sesuai kategorinya untuk digunakan dalam proses ekstraksi fitur dan klasifikasi.

### 2. Preprocessing

Preprocessing dilakukan untuk mempersiapkan citra sebelum proses ekstraksi fitur.

Tahapan ini meliputi:

- Penyeragaman ukuran citra menjadi 256 × 256 piksel.
- Konversi citra ke grayscale untuk proses ekstraksi fitur yang membutuhkan informasi intensitas.
- Pengurangan noise menggunakan Gaussian Blur.

Tahapan preprocessing bertujuan untuk mengurangi gangguan pada citra dan menghasilkan representasi data yang lebih sesuai untuk proses selanjutnya.

### 3. Feature Extraction

Ekstraksi fitur dilakukan untuk memperoleh karakteristik penting dari setiap citra. Terdapat tiga metode yang digunakan.

#### a. Color Histogram

*Color Histogram* digunakan untuk memperoleh informasi mengenai distribusi warna pada citra.

Metode ini merepresentasikan frekuensi kemunculan intensitas warna sehingga dapat digunakan untuk mengidentifikasi perbedaan karakteristik warna antara uang asli dan uang palsu.

#### b. Local Binary Pattern (LBP)

*Local Binary Pattern* digunakan untuk mengekstraksi karakteristik tekstur pada citra.

Metode ini bekerja dengan membandingkan intensitas piksel pusat dengan piksel tetangganya untuk menghasilkan pola biner. Pola tersebut kemudian direpresentasikan dalam bentuk histogram sebagai fitur tekstur.

#### c. Canny Edge Detection

*Canny Edge Detection* digunakan untuk mendeteksi struktur tepi pada citra berdasarkan perubahan intensitas piksel.

Hasil deteksi tepi kemudian direpresentasikan menggunakan nilai densitas tepi (*edge density*), yaitu perbandingan jumlah piksel tepi terhadap total piksel citra.

### 4. Classification Using Euclidean Distance

Proses klasifikasi menggunakan pendekatan *rule-based* dengan metode Euclidean Distance.

Tahapan klasifikasi meliputi:

1. Memisahkan fitur berdasarkan label kelas uang asli dan uang palsu.
2. Menghitung nilai rata-rata fitur (*class mean*) dari masing-masing kelas sebagai representasi karakteristik kelas.
3. Melakukan standardisasi fitur menggunakan StandardScaler.
4. Menghitung jarak Euclidean antara fitur citra dengan rata-rata fitur dari kedua kelas.
5. Menentukan hasil klasifikasi berdasarkan kelas dengan jarak terkecil.

Kelas dengan jarak Euclidean terkecil dianggap memiliki karakteristik yang paling mirip dengan citra yang sedang diklasifikasikan.

### 5. Feature Combination

Tahap ini dilakukan dengan menggabungkan tiga jenis fitur, yaitu:

- Color Histogram
- Local Binary Pattern (LBP)
- Canny Edge Detection

Penggabungan dilakukan menggunakan fungsi `np.hstack()` sehingga seluruh representasi fitur disusun menjadi satu vektor fitur gabungan.

Tujuannya adalah memanfaatkan informasi warna, tekstur, dan tepi secara bersamaan untuk memperoleh representasi citra yang lebih lengkap.

### 6. Evaluation

Evaluasi dilakukan untuk mengetahui performa klasifikasi menggunakan dua metrik utama:

- **Accuracy:** Mengukur proporsi jumlah prediksi yang benar terhadap keseluruhan data.
- **Confusion Matrix:** Menampilkan perbandingan hasil klasifikasi yang benar dan salah pada setiap kelas.

## Hasil dan Pembahasan

Berdasarkan implementasi metode penggabungan fitur (*Feature Combination*), diperoleh hasil evaluasi sebagai berikut.

### 1. Hasil Klasifikasi Feature Combination

| Keterangan | Hasil |
|---|---:|
| Akurasi | **95%** |
| Prediksi benar pada kelas uang asli | 55 |
| Prediksi benar pada kelas uang palsu | 59 |
| Uang asli salah diklasifikasikan sebagai uang palsu | 5 |
| Uang palsu salah diklasifikasikan sebagai uang asli | 1 |
| Total data | 120 |

### 2. Confusion Matrix

Dengan asumsi label kelas 0 merepresentasikan uang asli dan label kelas 1 merepresentasikan uang palsu, hasil confusion matrix adalah sebagai berikut.

| Aktual / Prediksi | Uang Asli (0) | Uang Palsu (1) |
|---|---:|---:|
| Uang Asli (0) | 55 | 5 |
| Uang Palsu (1) | 1 | 59 |

Berdasarkan hasil tersebut:

- Sebanyak 55 citra uang asli berhasil diklasifikasikan dengan benar.
- Sebanyak 59 citra uang palsu berhasil diklasifikasikan dengan benar.
- Sebanyak 5 citra uang asli salah diklasifikasikan sebagai uang palsu.
- Sebanyak 1 citra uang palsu salah diklasifikasikan sebagai uang asli.

Dengan demikian, terdapat 114 prediksi benar dari total 120 citra, sehingga diperoleh akurasi sebesar **95%**.

### 3. Analisis Hasil

Hasil pengujian menunjukkan bahwa kombinasi fitur warna, tekstur, dan tepi mampu memberikan representasi karakteristik visual yang lebih beragam dibandingkan penggunaan satu jenis fitur saja.

Setiap metode memiliki peran yang berbeda:

- **Color Histogram** memberikan informasi mengenai distribusi warna pada citra.
- **Local Binary Pattern (LBP)** menangkap karakteristik tekstur dan pola permukaan citra.
- **Canny Edge Detection** membantu mengidentifikasi struktur tepi dan pola batas objek.

Penggabungan ketiga fitur tersebut memungkinkan sistem mempertimbangkan beberapa karakteristik visual secara bersamaan dalam menentukan hasil klasifikasi.

### 4. Catatan Evaluasi

Implementasi klasifikasi yang digunakan menghitung rata-rata fitur dari masing-masing kelas dan melakukan evaluasi pada kumpulan fitur serta label yang sama.

Dengan demikian, belum terdapat pemisahan antara data latih dan data uji secara independen. Nilai akurasi sebesar 95% merupakan hasil evaluasi pada data yang digunakan dalam proses pembentukan rata-rata kelas, sehingga belum dapat dijadikan estimasi performa generalisasi sistem terhadap citra baru.

## Instalasi Library

Sebelum menjalankan program, pastikan library yang diperlukan telah tersedia.

Gunakan perintah berikut untuk menginstal seluruh library:

```bash
pip install numpy opencv-python matplotlib scikit-image scikit-learn seaborn
```

## Cara Menjalankan Proyek

Berikut langkah-langkah untuk menjalankan proyek ini:

### 1. Clone Repository

Unduh repository menggunakan perintah berikut:

```bash
git clone https://github.com/USERNAME/REPOSITORY-NAME.git
```

Masuk ke direktori proyek:

```bash
cd REPOSITORY-NAME
```

### 2. Buka Notebook

Buka file notebook menggunakan Google Colab atau Jupyter Notebook.

### 3. Siapkan Dataset

Siapkan dataset dengan struktur folder sesuai dengan direktori yang digunakan pada notebook.

Jika menggunakan Google Colab, hubungkan Google Drive terlebih dahulu.

### 4. Sesuaikan Path Dataset

Sesuaikan variabel `base_path` dengan lokasi dataset yang digunakan.

Contoh:

```python
base_path = "/content/drive/Shareddrives/DATASET MINI PROJECT PCD KEL 3"
```

### 5. Jalankan Program

Jalankan setiap sel notebook secara berurutan, mulai dari:

1. Dataset Loading
2. Preprocessing
3. Feature Extraction
4. Classification
5. Feature Combination
6. Evaluation

Amati hasil ekstraksi fitur, proses klasifikasi, dan Confusion Matrix untuk memahami performa sistem.
