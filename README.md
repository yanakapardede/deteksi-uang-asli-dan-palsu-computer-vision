# Deteksi Uang Kertas Asli dan Palsu Menggunakan Computer Vision Klasik

## Deskripsi Proyek

Mini Project Pengolahan Citra Digital (PCD) ini bertujuan untuk mengembangkan sistem sederhana yang dapat membedakan citra uang kertas asli dan uang palsu berdasarkan karakteristik visual menggunakan pendekatan **Computer Vision klasik**.

Penelitian ini menerapkan beberapa teknik ekstraksi fitur untuk memperoleh informasi penting dari citra, meliputi distribusi warna (*Color Histogram*), karakteristik tekstur (*Local Binary Pattern*), dan struktur tepi (*Canny Edge Detection*).

Proses klasifikasi dilakukan menggunakan pendekatan berbasis aturan (*rule-based*) dengan menghitung jarak Euclidean (*Euclidean Distance*) antara fitur citra dan rata-rata fitur dari masing-masing kelas. Selain itu, dilakukan penggabungan beberapa fitur (*Feature Combination*) untuk mengetahui pengaruh kombinasi karakteristik visual terhadap hasil klasifikasi.

Project ini juga membandingkan hasil klasifikasi berdasarkan penggunaan fitur secara individual maupun kombinasi untuk mengetahui pendekatan yang memberikan performa terbaik.

## Tujuan Proyek

Tujuan dari mini project ini adalah:

1. Menerapkan konsep pengolahan citra digital dalam proses identifikasi uang kertas.
2. Melakukan preprocessing untuk mempersiapkan citra sebelum proses ekstraksi fitur.
3. Mengekstraksi karakteristik citra menggunakan Color Histogram, Local Binary Pattern, dan Canny Edge Detection.
4. Mengimplementasikan klasifikasi berbasis aturan menggunakan Euclidean Distance tanpa menggunakan model Machine Learning.
5. Membandingkan performa setiap metode ekstraksi fitur.
6. Menganalisis pengaruh kombinasi fitur terhadap hasil klasifikasi.
7. Mengevaluasi hasil klasifikasi menggunakan akurasi dan confusion matrix.

## Dataset

Dataset yang digunakan merupakan dataset citra uang kertas yang dikumpulkan secara mandiri.

Dataset terdiri dari dua kelas utama:

- **Uang Asli:** Citra uang kertas asli.
- **Uang Palsu:** Citra uang mainan yang digunakan sebagai representasi uang palsu dalam penelitian ini.

Dataset memiliki total **120 citra**, dengan pembagian sebagai berikut:

| Kategori | Jumlah Citra |
|---|---:|
| Uang Asli | 60 |
| Uang Palsu | 60 |
| **Total** | **120** |

Citra mencakup tiga pecahan uang, yaitu Rp20.000, Rp50.000, dan Rp100.000.

Pengambilan gambar dilakukan dengan variasi kondisi pencahayaan, orientasi, dan jarak. Oleh karena itu, beberapa citra memiliki kemungkinan gangguan seperti bayangan, blur, dan latar belakang yang tidak seragam.

Seluruh citra diseragamkan ukurannya menjadi **256 × 256 piksel** sebelum diproses lebih lanjut.

## Metodologi

Tahapan pengolahan citra dalam project ini meliputi beberapa proses berikut.

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

Color Histogram digunakan untuk memperoleh informasi distribusi warna pada citra.

Metode ini merepresentasikan frekuensi kemunculan intensitas warna sehingga dapat digunakan untuk mengidentifikasi perbedaan karakteristik warna antara uang asli dan uang palsu.

#### b. Local Binary Pattern (LBP)

Local Binary Pattern digunakan untuk mengekstraksi karakteristik tekstur pada citra.

Metode ini bekerja dengan membandingkan intensitas piksel pusat dengan piksel tetangganya untuk menghasilkan pola biner. Pola tersebut kemudian direpresentasikan dalam bentuk histogram sebagai fitur tekstur.

#### c. Canny Edge Detection

Canny Edge Detection digunakan untuk mendeteksi struktur tepi pada citra berdasarkan perubahan intensitas piksel.

Hasil deteksi tepi kemudian direpresentasikan menggunakan nilai densitas tepi (*edge density*), yaitu perbandingan jumlah piksel tepi terhadap total piksel citra.

### 4. Classification (Euclidean Distance)

Proses klasifikasi menggunakan pendekatan *rule-based* dengan metode Euclidean Distance.

Tahapan klasifikasi meliputi:

1. Memisahkan fitur berdasarkan label kelas uang asli dan uang palsu.
2. Menghitung nilai rata-rata fitur (*class mean*) dari masing-masing kelas.
3. Melakukan standardisasi fitur menggunakan StandardScaler.
4. Menghitung jarak Euclidean setiap fitur terhadap rata-rata fitur kedua kelas.
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

Berdasarkan implementasi metode penggabungan fitur (*Feature Combination*), diperoleh hasil sebagai berikut:

### Hasil Klasifikasi Feature Combination

| Keterangan | Hasil |
|---|---:|
| Akurasi | 95% |
| True Positive / True Negative | 55 |
| Kesalahan klasifikasi kelas 0 ke kelas 1 | 5 |
| Kesalahan klasifikasi kelas 1 ke kelas 0 | 1 |
| Prediksi benar pada kelas 1 | 59 |
| Total data | 120 |

### Confusion Matrix

Hasil confusion matrix menunjukkan bahwa:

- Sebanyak 55 citra uang asli berhasil diklasifikasikan dengan benar.
- Sebanyak 59 citra uang palsu berhasil diklasifikasikan dengan benar.
- Sebanyak 5 citra uang asli salah diklasifikasikan sebagai uang palsu.
- Sebanyak 1 citra uang palsu salah diklasifikasikan sebagai uang asli.

Hasil tersebut menunjukkan bahwa kombinasi fitur warna, tekstur, dan tepi menghasilkan akurasi sebesar **95%** pada pengujian yang dilakukan.

Penggabungan fitur memberikan representasi karakteristik citra yang lebih beragam karena setiap metode memiliki kemampuan dalam menangkap informasi visual yang berbeda.

**Catatan evaluasi:** Implementasi klasifikasi yang digunakan menghitung rata-rata kelas dan melakukan evaluasi pada kumpulan fitur serta label yang sama. Belum terdapat pemisahan data latih dan data uji secara independen. Oleh karena itu, nilai akurasi 95% merupakan hasil evaluasi pada data yang digunakan dalam perhitungan, bukan estimasi performa generalisasi pada data baru.

## Instalasi Library

Sebelum menjalankan program, pastikan library yang diperlukan telah tersedia.

Gunakan perintah berikut untuk menginstal library:

```bash
pip install numpy opencv-python matplotlib scikit-image scikit-learn seaborn
```

## Cara Menjalankan Project

1. Clone repository ini ke komputer lokal.

```bash
git clone https://github.com/USERNAME/REPOSITORY-NAME.git
```

2. Buka file notebook menggunakan Google Colab atau Jupyter Notebook.

3. Siapkan dataset dengan struktur folder sesuai bagian Struktur Direktori.

4. Jika menggunakan Google Colab, hubungkan Google Drive.

5. Sesuaikan `base_path` dengan lokasi dataset.

```python
base_path = "/content/drive/Shareddrives/DATASET MINI PROJECT PCD KEL 3"
```

6. Jalankan setiap tahapan kode secara berurutan, mulai dari dataset loading, preprocessing, feature extraction, classification, hingga evaluation.

7. Amati hasil ekstraksi fitur, proses klasifikasi, dan confusion matrix untuk memahami performa sistem.

## Keterbatasan Penelitian

Beberapa keterbatasan dalam project ini meliputi:

1. Jumlah dataset masih terbatas, yaitu 120 citra.
2. Uang mainan digunakan sebagai representasi uang palsu, sehingga belum merepresentasikan seluruh karakteristik uang palsu yang sebenarnya.
3. Perbedaan pencahayaan, orientasi, dan kualitas citra dapat memengaruhi hasil ekstraksi fitur.
4. Metode Euclidean Distance memiliki sensitivitas terhadap representasi dan skala fitur.
5. Evaluasi yang dilakukan belum menggunakan pemisahan data latih dan data uji secara independen.

## Pengembangan Selanjutnya

Beberapa pengembangan yang dapat dilakukan pada penelitian berikutnya adalah:

1. Menambah jumlah dan variasi dataset.
2. Menggunakan dataset uang asli dan uang palsu dengan karakteristik yang lebih beragam.
3. Menerapkan pemisahan data latih dan data uji untuk memperoleh evaluasi yang lebih objektif.
4. Mencoba metode ekstraksi fitur lainnya.
5. Membandingkan pendekatan rule-based dengan metode Machine Learning atau Deep Learning.
